# PHP: Can I set up a sandbox environment to compile and execute C++ or Java?

Yes, you can absolutely build an online compiler and execution sandbox using PHP, but you must never execute untrusted C++ or Java code directly on your host operating system. If a user submits malicious code (like an infinite loop, massive memory allocations, or a command to erase files), it can crash or compromise your entire server.

To achieve this safely, you have two primary options: use an open-source execution API or build your own isolated multi-layer sandbox container.


## Option 1: The Easiest Way (Use Judge0 API)

Instead of building, configuring, and securing a compilers infrastructure yourself, you can deploy Judge0, which is the industry standard, open-source robust online code execution system.

You can run your own local instance of Judge0 via Docker and communicate with it using a clean, secure API from your PHP application:

```php
<?php
// Example using PHP cURL to submit C++ code to a local Judge0 sandbox instance
\$ch = curl_init("http://localhost:2358/submissions?wait=true");

\$data = [
    "source_code" => base64_encode('#include <iostream>\nint main() { std::cout << "Hello World"; return 0; }'),
    "language_id" => 54, // 54 is C++ (GCC 9.2.0) in Judge0
    "stdin" => base64_encode("")
];

curl_setopt(\$ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt(\$ch, CURLOPT_POST, true);
curl_setopt(\(ch, CURLOPT_POSTFIELDS, json_encode(\)data));
curl_setopt(\$ch, CURLOPT_HTTPHEADER, ['Content-Type: application/json']);

\(response = json_decode(curl_exec(\)ch), true);
curl_close(\$ch);

// Echo back the sandboxed compilation or output result safely
echo base64_decode(\$response['stdout']);
```


## Option 2: The Custom Way (Docker + PHP `proc_open`)

If you prefer to build a custom solution, you can use PHP's `proc_open()` function to spin up ephemeral, highly restricted Docker containers on demand whenever a user submits code.

### Step 1: Create a Strict Docker Sandbox Image
You need a base image containing `g++` and `openjdk`. Crucially, you must drop privileges and isolate resources. Create a `Dockerfile`:

```dockerfile
FROM ubuntu:24.04

# Install compilers
RUN apt-get update && apt-get install -y g++ openjdk-21-jdk-headless && rm -rf /var/lib/apt/lists/*

# Create an unprivileged user (Never run untrusted code as root!)
RUN useradd -m sandboxuser
USER sandboxuser
WORKDIR /home/sandboxuser
```

### Step 2: Invoke the Compilation via PHP
In your PHP backend, write the user's code to a temporary file, mount it strictly as read-only to your Docker container, and run it with heavy runtime limitations:

```php
<?php
// 1. Save user C++ code safely to a temporary local folder
\$sandboxFolder = '/tmp/php_sandbox_jobs/' . uniqid();
mkdir(\$sandboxFolder, 0777, true);
file_put_contents("sandboxFolder/main.cpp", userSubmittedCode);

// 2. Build a highly defensive Docker run command
\$command = [
    'docker', 'run', '--rm',
    '--network', 'none',                       // Block all internet access (stops data exfiltration)
    '--memory', '256m',                        // Kill the script if it abuses RAM
    '--cpus', '0.5',                           // Max out at half a CPU core to avoid server lag
    '--read-only',                             // Freeze container filesystem changes
    '-v', "\$sandboxFolder:/home/sandboxuser:ro", // Mount the code folder strictly as READ-ONLY
    'my-sandbox-compiler-image',               // Your custom image name
    'bash', '-c', 'g++ main.cpp -o app && ./app' // Compile AND execute inside the sandbox
];

// 3. Securely execute using process controls
\$descriptors = [
    1 => ['pipe', 'w'], // stdout
    2 => ['pipe', 'w']  // stderr
];

\(process = proc_open(\)command, descriptors, pipes);

if (is_resource(\$process)) {
    // Prevent infinite loops by enforcing a hard timeout (e.g., 5 seconds)
    \$timeout = 5;
    \$start = time();
    
    while (proc_get_status(\$process)['running']) {
        if ((time() - start) > timeout) {
            proc_terminate(\$process); // Violently kill hanging infinite loops
            echo "Error: Execution Timed Out!";
            exit;
        }
        usleep(100000); // 100ms
    }

    \(stdout = stream_get_contents(\)pipes[1]);
    \(stderr = stream_get_contents(\)pipes[2]);
    
    fclose(\$pipes[1]);
    fclose(\$pipes[2]);
    proc_close(\$process);

    // Output results to user
    echo !empty(\$stderr) ? "Compiler/Runtime Error: stderr" : stdout;
}

// 4. Cleanup the temporary host file
unlink("\$sandboxFolder/main.cpp");
rmdir(\$sandboxFolder);
```

### Essential Security Checklist for Custom Sandboxes
* **Network Isolation (`--network none`)**: Always cut off web access. Untrusted scripts could otherwise be weaponized to launch spam relays or DDOS attacks.
* **No Privilege Escalation**: Ensure the user inside the container does not map to root or have access to the host's `/var/run/docker.sock`.
* **Strict Memory Limits (`--memory`)**: If omitted, a simple C++ loop continuously pushing to a `std::vector` will trigger an Out-Of-Memory error on your entire host server, crashing your PHP app.


## Choosing the Right Approach

Which approach fits your project architecture best—the pre-built Judge0 API engine or building a custom Docker container workflow?

### Choosing the Pre-built Judge0 API
Choosing the pre-built Judge0 API is the right choice for rapid deployment. It saves you from maintaining low-level sandbox isolation while natively handling C++ and Java dependencies right out of the box.

You can integrate Judge0 into your PHP application using two primary deployment architectures:

* **Architecture Option A: Cloud Hosted (RapidAPI / Judge0 Cloud)**
  The easiest way to start is by using the managed Judge0 CE API on RapidAPI. You do not have to host or install anything. You simply register for an API key and send your PHP cURL payloads directly to their servers.
* **Architecture Option B: Self-Hosted Sandbox (Docker Compose)**
  If you want total control, zero latency, and no request limits, you can host your own private instance of Judge0 on your own Linux server or VPS.

### Step 1: Install Judge0 on Your Server
Connect via SSH to your server and initialize the stack using the official Judge0 GitHub repository:

```bash
# Clone the repository
git clone https://github.com/judge0/judge0.git
cd judge0

# Start the sandbox services via Docker Compose
docker-compose up -d
```

This instantly spins up an isolated sandbox environment complete with an API worker, a PostgreSQL database, and a Redis queue manager. By default, the API will listen locally on port `2358`.

### Step 2: The PHP Implementation Workflow
Because executing code takes time, Judge0 provides two submission workflows. For small snippets, you can use the synchronous Wait Workflow which processes the request immediately and sends back the result in the HTTP response.

Here is how you handle C++ and Java execution from your PHP application:

```php
<?php

/**
 * Submits source code to the Judge0 Sandbox API.
 * 
 * @param string \$sourceCode The raw, unencoded program code.
 * @param int \$languageId Judge0 ID (54 for C++ GCC, 62 for Java OpenJDK).
 * @param string \$stdin Optional input parameters to feed into the program.
 * @return array The compiled/executed output status and payload.
 */
function runCodeInSandbox(string \$sourceCode, int languageId, string stdin = ""): array 
{
    // Define your endpoint (Change to the RapidAPI URL if using the cloud version)
    \$url = "http://localhost:2358/";
    // ... complete implementation logic
}
```


## What if the C++ or Java code is malicious?

If a user submits malicious C++ or Java code, Judge0's sandbox layers completely isolate the execution so that your host system and PHP application remain safe. Because Judge0 runs code inside a stateless, heavily restricted container controlled by Linux cgroups and system call filters, the attack vectors are blocked right at the boundary.

Here is exactly how Judge0 handles the most common types of malicious attacks:

### 1. Infinite Loops and Fork Bombs (CPU Exhaustion)
* **The Attack**: A user runs `while(true){}` or a recursion loop designed to hit 100% CPU usage and freeze your server.
* **Judge0 Defense**: Every submission has a hard `cpu_time_limit` (defaulting to 5 seconds if not overridden). Once that exact millisecond is breached, the sandbox process is instantly killed, and the API returns a status code of **Time Limit Exceeded**.

### 2. Allocation Floods (Memory Exhaustion / OOM)
* **The Attack**: A C++ script aggressively pushes data into a vector, or Java continuously spawns objects to consume all system RAM, attempting to crash the host operating system.
* **Judge0 Defense**: Judge0 enforces a strict process-level `memory_limit` via Linux control groups (cgroups). If the program tries to allocate memory beyond this limit, the process is forcefully terminated by the kernel, returning a **Memory Limit Exceeded** status.

### 3. File System Damage (e.g., `rm -rf /`)
* **The Attack**: A user tries to run system commands from inside code (like using `std::system("rm -rf /")` in C++ or `Runtime.getRuntime().exec()` in Java) to delete server configuration files.
* **Judge0 Defense**: The code executes inside an isolated Docker container where the underlying host file system is completely unmapped and inaccessible. Furthermore, Judge0 drops root privileges and runs the process as an unprivileged user. The user can only write to a temporary, space-limited sandbox folder that is completely destroyed the moment execution finishes.

### 4. Network Attacks and Botnets (Data Exfiltration)
* **The Attack**: A hacker writes a script to scan your local network, attempt to connect to your internal databases, or use your server infrastructure to launch a DDOS attack or mine cryptocurrency.
* **Judge0 Defense**: Network access is entirely disabled inside the execution environment by default. The isolated code cannot resolve domain names, send HTTP requests, or open network sockets. It will instantly throw a connection error or a network unreachable exception inside the runtime.

## What Your PHP Application Receives

When malicious activity is blocked, your PHP script does not crash. Judge0 safely intercepts the failure and returns a structured JSON response identifying the exact nature of the blocked attack via its status field:

| Attack Outcome | Judge0 Status Code | Description Returned to PHP |
| :--- | :--- | :--- |
| Infinite Loop / Lag | 3 | Time Limit Exceeded |
| RAM Drain | 4 | Memory Limit Exceeded |
| Compilation Hack | 11 | Compilation Error |
| Segmentation Fault | 5 | Runtime Error (SIGSEGV) |
| Illegal System Call | 12 | Runtime Error (SIGXFSZ) or Runtime Error (other) |


## Configure Judge0

Would you like to look at the security configuration file (`judge0.conf`) to see how to fine-tune these resource walls even further?

To configure these security walls, you need to edit the `judge0.conf` file, which is located in your Judge0 installation directory on your server. Below are the most critical parameters you should check and adjust to maximize security against malicious code.

### Key Security Options in `judge0.conf`

Open the configuration file and locate or modify the following default settings:

```ini
# Max CPU time allowed for execution (in seconds)
# Set this low to stop infinite loops quickly.
max_cpu_time_limit = 5.0

# Max wall time allowed (in seconds)
# This includes time spent waiting for I/O. Prevents processes from hanging.
max_wall_time_limit = 10.0

# Max memory allowed (in kilobytes)
# 256000 KB is ~250MB. Stops RAM drain attacks completely.
max_memory_limit = 256000

# Max stack size allowed (in kilobytes)
# Prevents stack overflow attacks from crashing the environment.
max_stack_limit = 64000

# Max processes/threads a submission can spawn
# Crucial for blocking C++ fork bombs (e.g., fork(); fork();)
max_number_of_processes = 20

# Max file size the submission can create (in kilobytes)
# Blocks malicious scripts from generating massive files to fill your disk.
max_file_size = 1024
```

### Applying Changes

Whenever you modify your `judge0.conf` file, you must restart your Docker containers for the new resource limits to take effect:

```bash
docker-compose down
docker-compose up -d
```

### Next Steps for Your Project

Now that your security boundaries and PHP back-end logic are planned out, you can focus on building the system. If you want, I can help you with:

* **Designing the database schema** to store user submissions, execution times, and memory logs.
* **Creating the HTML/JavaScript code editor interface** (using tools like Monaco Editor or CodeMirror) to pass code directly to your PHP script.
