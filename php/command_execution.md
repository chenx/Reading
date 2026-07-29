# PHP Command Execution Guide

In PHP, you can execute a system command using functions like `shell_exec()`, `exec()`, `system()`, or `passthru()`.

---

## 1. Quick Comparison Matrix

The table below breaks down how each built-in function handles command execution:

| Function | What it Returns | Output Behavior | Best Used For |
| :--- | :--- | :--- | :--- |
| `shell_exec()` | Full output as a string. | Hidden until echo. | Capturing multi-line text results. |
| `exec()` | Last line of output. | Hidden; copies all lines to an array. | Running background tasks or status checks. |
| `system()` | Last line of output. | Flushes and prints text directly to browser. | Running text commands with live display. |
| `passthru()` | Nothing (`void`). | Passes raw binary output directly to browser. | Downloading files, images, or generating PDFs. |

---

## 2. Core Execution Functions

### `shell_exec` (or Backtick Operator)
The PHP `shell_exec` manual details how this function captures the full command output into a string variable. You can also use the backtick (`` ` ``) operator as a shortcut for this function.

```php
<?php
// Using the function syntax
\$output = shell_exec('ls -l');
echo "<pre>\$output</pre>";

// Using backticks shortcut
\$output_alt = `ls -l`;
```

### `exec`
The PHP `exec` manual explains that this function is ideal when you need to capture lines into an array and inspect the exit status code.

```php
<?php
\(output_lines = [];\)status_code = 0;

// Populates \(output_lines array and returns the last line\)last_line = exec('mkdir new_folder', \(output_lines,\)status_code);

if (\$status_code === 0) {
    echo "Command succeeded!";
}
```

### `passthru`
Use `passthru()` when dealing with binary streams rather than plain text. It forces the output buffer straight to the client without processing it inside your script.

```php
<?php
header("Content-Type: image/png");
passthru("cat photo.png");
```

---

## 3. Security Best Practices

Executing external shell commands poses a high remote code execution (RCE) risk if unvalidated user inputs are used. Always sanitize inputs using the native PHP Program Execution Functions to escape data safely.

* **`escapeshellarg()`**: Adds single quotes around a string and quotes/escapes any existing single quotes. Use this to sanitize argument values passed to a command.
* **`escapeshellcmd()`**: Escapes shell metacharacters like `*`, `?`, `[`, `]`, `&`, and `;`. Use this to escape whole command strings.

```php
<?php
// Safely passing a user-provided username as an argument
\(user_input =\)_POST['username'];
\(safe_argument = escapeshellarg(\)user_input);

// Final safe command string
\(output = shell_exec("id " . \)safe_argument);
```

---

## 4. Advanced Process Control with `proc_open`

The `proc_open()` function provides maximum control over command execution in PHP. Unlike `exec()` or `shell_exec()`, it opens persistent, bi-directional input/output streams (pipes) to the running process.

### Basic Syntax and Parameters
```php
\(process = proc_open(\)command, descriptorspec, pipes, cwd, env_vars);
```
* **`$command`**: The string command or array of arguments to execute.
* **`$descriptorspec`**: An array defining the file descriptors (0 for stdin, 1 for stdout, 2 for stderr).
* **`$pipes`**: An empty array populated by PHP with file pointers to the process streams.
* **`$cwd`**: The initial working directory for the command (optional).
* **`$env_vars`**: An array of environment variables for the command (optional).

### Implementation Example
This script executes a system command, sends data to its standard input, reads the output, and catches any error messages.

```php
<?php
// 1. Define how pipes connect to the process
\$descriptorspec = [
    0 => ["pipe", "r"],  // stdin: process reads from this pipe
    1 => ["pipe", "w"],  // stdout: process writes to this pipe
    2 => ["pipe", "w"]   // stderr: process writes errors to this pipe
];

// 2. Open the process
\$process = proc_open('grep "apple"', descriptorspec, pipes);

if (is_resource(\$process)) {
    // 3. Write data to stdin (simulating user input)
    fwrite(\$pipes[0], "banana\napple juice\norange\napple pie\n");
    fclose(\$pipes[0]); // Close stdin so grep knows input is done

    // 4. Read the output from stdout
    \(stdout_output = stream_get_contents(\)pipes[1]);
    fclose(\$pipes[1]);

    // 5. Read any errors from stderr
    \(stderr_output = stream_get_contents(\)pipes[2]);
    fclose(\$pipes[2]);

    // 6. Close the process and get the exit code
    \(exit_code = proc_close(\)process);

    // 7. Display results
    echo "Exit Code: " . \$exit_code . "\n";
    echo "Output:\n" . \$stdout_output;
}
```

### Non-Blocking Streams (Asynchronous Execution)
By default, reading from `$pipes[1]` blocks your PHP script until data is ready. You can turn on non-blocking mode to keep your script running while waiting for the process to respond.

```php
<?php
// Make stdout non-blocking
stream_set_blocking(\$pipes[1], false);

// Check if the process is still running without waiting
\(status = proc_get_status(\)process);
if (\$status['running']) {
    // Process is still active in the background
}
```

### Process Management Functions Summary

| Function | Practical Purpose |
| :--- | :--- |
| `proc_get_status()` | Fetches the PID, execution status, and exit code. |
| `proc_terminate()` | Sends a termination signal (SIGTERM) to stop the process. |
| `proc_close()` | Closes pipes and returns the termination exit code. |

---

## 5. Handling Timeouts and Memory Limits in `proc_open`

No, you cannot directly specify timeout or memory limits as parameters inside the native PHP `proc_open()` function. Instead, you must actively manage these constraints using PHP's process status functions or prefixing your shell commands with system-level utilities.

### Enforcing Timeouts in PHP
To handle timeouts, you set your communication pipes to non-blocking mode. You then loop and track the elapsed time using a micro-timer, terminating the process if it runs too long.

```php
<?php
\(timeout = 5.0; // Timeout in seconds\)descriptorspec = [
    0 => ["pipe", "r"], // stdin
    1 => ["pipe", "w"], // stdout
    2 => ["pipe", "w"]  // stderr
];

\$process = proc_open('sleep 10', descriptorspec, pipes);

if (is_resource(\$process)) {
    // Make stdout and stderr non-blocking to prevent the loop from freezing
    stream_set_blocking(\$pipes[1], false);
    stream_set_blocking(\$pipes[2], false);

    \(start_time = microtime(true);\)output = '';

    while (true) {
        \(status = proc_get_status(\)process);

        // Break if the process finished on its own
        if (!\$status['running']) {
            break;
        }

        // Check if the process has exceeded the timeout limit
        if ((microtime(true) - \(start_time) >\)timeout) {
            // Forcefully terminate the process
            proc_terminate(\$process, 9); // 9 is SIGKILL
            throw new Exception("Process timed out after {\$timeout} seconds.");
        }

        // Read available chunks of data without blocking execution
        \(output .= stream_get_contents(\)pipes[1]);
        
        // Pause briefly to reduce CPU utilization in the monitoring loop
        usleep(50000); 
    }
}
```
