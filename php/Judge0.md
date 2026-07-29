# PHP: Can I set up a sandbox environment to compile and execute C++ or Java?

Yes, you can absolutely build an online compiler and execution sandbox using PHP, but you must never execute untrusted C++ or Java code directly on your host operating system. If a user submits malicious code (like an infinite loop, massive memory allocations, or a command to erase files), it can crash or compromise your entire server.

To achieve this safely, you have two primary options: use an open-source execution API or build your own isolated multi-layer sandbox container.

---

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

---

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

---

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
