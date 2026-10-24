# Error Handling in Bash

Error handling helps a script notice when a command fails, explain what
happened, and choose whether to continue or stop.

## Exit codes

Every command finishes with an exit status (also called an exit code):

- `0` conventionally means success.
- A non-zero value means failure or another result.

The exact meaning of a non-zero code depends on the command. A script can
return an exit code to the shell that started it.

## Two useful categories of errors

### 1. Expected errors you know how to handle

These are situations your script can predict and respond to, such as:

- A required argument was not provided.
- A file does not exist.
- A package installation command failed.
- A search found no matching text.

Check these cases explicitly and provide a useful message or alternative
action. For example, a missing package installation can be reported before
the script exits:

```bash
if dnf install nginx -y; then
    echo "Nginx installation succeeded."
else
    echo "Error: Nginx installation failed." >&2
    exit 1
fi
```

### 2. Unexpected errors you did not plan for

These are failures the script cannot predict in advance, such as an
unavailable network, a full disk, or a service that stops responding.
You may not know the exact cause, but you can still detect command failure,
show a general error message, record diagnostic details, and stop safely.

Error handling does not guarantee that every problem can be fixed
automatically. The goal is to fail clearly and avoid continuing as if the task
succeeded.

## Check a command's exit status

Use a command directly in an `if` statement when deciding what to do:

```bash
if ls "/path/that/does/not/exist"; then
    echo "Directory contents listed."
else
    echo "Error: Could not list the directory." >&2
fi
```

You can also inspect `$?`, which contains the exit status of the most recently
run command:

```bash
ls "/path/that/does/not/exist"
status=$?

if [ "$status" -ne 0 ]; then
    echo "Listing failed with exit code $status." >&2
fi
```

Save `$?` immediately. If another command runs first, `$?` will refer to that
command instead.

> Prefer `if command; then ...` when possible. It connects the check directly
> to the command and avoids accidentally overwriting `$?`.

## Some non-zero statuses are normal results

A non-zero exit status does not always mean that something unexpected broke.
For example, `grep` returns `1` when it did not find a match. Handle that
result according to what your script expects:

```bash
if grep -q "ERROR" application.log; then
    echo "Errors were found."
else
    echo "No matching errors were found."
fi
```

## Stop a script with `exit`

Use `exit` to stop the script and return a status to its caller:

```bash
echo "Error: A required input is missing." >&2
exit 1
```

Use `exit 0` to indicate success when you need to exit explicitly. Non-zero
values such as `1` conventionally indicate failure. Choose clear messages and
consistent codes for your own scripts.

## Use `set -e` carefully

```bash
set -e
```

This tells Bash to exit when many commands fail. It can help prevent a script
from continuing after a failure, but it is **not a complete error handler**:

- It does not explain what failed or provide a helpful message by itself.
- Bash has contexts where a non-zero status is expected or treated
  differently, including conditions and parts of `&&` or `||` lists.
- It cannot repair failures such as network outages or full disks.

For important steps, explicit checks make the intended behavior easier to
understand:

```bash
if dnf install nginx -y; then
    echo "Nginx is ready."
else
    echo "Error: Could not install Nginx. Check the package manager output and network." >&2
    exit 1
fi
```

## Conditional operators: `&&` and `||`

Use `&&` to run a command only if the previous command succeeds:

```bash
mkdir -p build && echo "Build directory is ready."
```

Use `||` to run a command only if the previous command fails:

```bash
mkdir -p build || {
    echo "Error: Could not create the build directory." >&2
    exit 1
}
```

Avoid this pattern for error handling:

```bash
command1 && echo "Succeeded" || echo "Failed"
```

The `||` part can run if either `command1` fails **or** the success-message
command fails. An `if` statement is clearer when the message depends on the
first command's status.

## Logging an error

Send error messages to standard error with `>&2`. To append a message to a
log file as well:

```bash
echo "Error: Could not complete the deployment." | tee -a error.log >&2
```

This shows the message in the terminal and appends it to `error.log`.

## A small complete example

```bash
#!/usr/bin/env bash

# Stop with a clear message if the script is not given a filename.
if [ "$#" -ne 1 ]; then
    echo "Usage: bash check-file.sh FILENAME" >&2
    exit 1
fi

file_name=$1

# Check the expected failure case explicitly.
if [ ! -f "$file_name" ]; then
    echo "Error: File not found: $file_name" >&2
    exit 1
fi

echo "File exists: $file_name"
exit 0
```

## Key points

- Check command statuses when the next action depends on success or failure.
- Handle expected situations explicitly and explain unexpected failures as
  clearly as possible.
- Use `exit` with a non-zero status when the script cannot continue safely.
- `set -e` can stop a script in many failure cases, but it does not replace
  clear checks, messages, or logging.
- A non-zero status may represent a normal result, so interpret it in the
  context of the command.