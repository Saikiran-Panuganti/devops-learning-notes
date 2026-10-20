# Bash Variables

Variables let a script give a name to a value so it can be reused, changed, and passed to commands. They are used for configuration, user input, command results, and environment settings.

> **Shell note:** This lesson uses Bash. Shell syntax can differ between Bash, POSIX `sh`, Zsh, and other shells.

## 1. Create and use a variable

Assign a value with `name=value`. Do not put spaces around `=`:

```bash
name="Ada"
greeting="Hello"

printf '%s, %s!\n' "$greeting" "$name"
```

Output:

```text
Hello, Ada!
```

Use `$name` or `${name}` to expand a variable. Braces make the variable boundary explicit and are useful when adjoining text:

```bash
service="api"
printf 'Starting %s-service\n' "$service"
```

Use braces when appending characters that could be read as part of the variable name:

```bash
version=2
printf 'release-%s\n' "${version}_stable"
```

### Why are there no spaces around `=`?

In a shell assignment, `name=value` is assignment syntax. With spaces, the shell interprets the first word as a command:

```bash
name = "Ada"  # Not an assignment; attempts to run a command named "name"
```

## 2. Quote variable expansions

Double-quote expansions by default:

```bash
directory="/var/tmp/build output"
mkdir -p -- "$directory"
```

Without quotes, the shell can perform word splitting and pathname expansion. A value containing spaces may become multiple arguments, and wildcard characters such as `*` may expand to filenames.

Use `"$name"` when you want the value passed as one argument. Use `${name}` when you need an unambiguous variable boundary.

Single quotes preserve literal text; they do not expand variables:

```bash
name="Ada"
printf '%s\n' '$name'   # Prints: $name
printf '%s\n' "$name"   # Prints: Ada
```

## 3. Bash variables are not strongly typed

Bash variables hold text; a variable does not have a declared type like an integer or Boolean in many programming languages. How a value is interpreted depends on the operation that uses it.

For integer arithmetic, use arithmetic expansion:

```bash
attempts=2
attempts=$((attempts + 1))
printf 'Attempts: %s\n' "$attempts"
```

This prints `Attempts: 3`. Arithmetic contexts treat values as integers; they are not general-purpose decimal or floating-point calculations.

For comparisons, use a test expression appropriate to the value:

```bash
if [[ "$environment" == "production" ]]; then
    printf 'Production configuration selected\n'
fi
```

String comparison and numeric comparison are different operations. Conditions are covered in a later lesson.

## 4. Empty and unset variables

An unset variable has not been assigned. An empty variable is set to an empty string:

```bash
unset optional_value
empty_value=""

printf 'Unset: <%s>\n' "$optional_value"
printf 'Empty: <%s>\n' "$empty_value"
```

Both expansions appear empty in this example, so use parameter expansion to distinguish or provide defaults:

```bash
printf 'Value: %s\n' "${optional_value:-default}"
```

`${value:-default}` uses `default` if `value` is unset or empty. `${value-default}` uses it only when `value` is unset.

With `set -u`, expanding an unset variable causes a script error. This can catch misspellings, but scripts must deliberately handle values that are optional:

```bash
#!/usr/bin/env bash
set -u

name=${1:-Guest}
printf 'Hello, %s!\n' "$name"
```

## 5. Local, global, and exported variables

At the top level of a script, an assignment is available in the current shell process. A variable created inside a function is global unless declared `local`:

```bash
describe_service() {
    local service_name="web"
    printf 'Service: %s\n' "$service_name"
}

describe_service
```

Use `local` for function implementation details to avoid unintentionally changing variables elsewhere in the script. Function scope will be explained in more detail in the functions lesson.

Shell variables are not automatically inherited by child processes. Export a variable to include it in the environment of commands started by the current shell:

```bash
APP_ENV="development"
export APP_ENV

bash -c 'printf "Environment: %s\n" "$APP_ENV"'
```

The child Bash process prints `development`. A one-command environment variable can also be written as:

```bash
APP_ENV="test" bash -c 'printf "Environment: %s\n" "$APP_ENV"'
```

Environment variables are useful for configuration, but do not use them as a reason to expose secrets in logs or command output.

## 6. Read-only variables and removing variables

Use `readonly` to prevent reassignment in the current shell:

```bash
readonly SCRIPT_NAME="backup"
printf 'Running %s\n' "$SCRIPT_NAME"
```

Use `unset` to remove a variable:

```bash
temporary_value="sample"
unset temporary_value
```

After `unset`, the variable is no longer defined. `readonly` variables cannot be unset in the normal way.

## 7. Special variables you will see in scripts

Some variables are set by Bash and are useful for scripts:

| Variable | Meaning |
| --- | --- |
| `$0` | Name or path used to invoke the script |
| `$1`, `$2`, ... | First, second, and later positional arguments |
| `$#` | Number of positional arguments |
| `"$@"` | All positional arguments, preserving each as a separate argument when quoted |
| `$?` | Exit status of the most recently completed command |
| `$$` | Process ID of the current shell |

Example:

```bash
#!/usr/bin/env bash

printf 'Script: %s\n' "$0"
printf 'Argument count: %s\n' "$#"
printf 'First argument: %s\n' "${1:-<none>}"
```

Run it as `bash example.sh hello` to see the script name, argument count, and first argument. Script arguments and exit statuses will be covered in their own lessons.

## 8. Common mistakes

### Spaces around the assignment operator

```bash
region = "us-east-1"  # Incorrect
region="us-east-1"    # Correct
```

### Forgetting to quote an expansion

```bash
rm -r $target     # Risky: splitting and wildcard expansion may change the arguments
printf '%s\n' "$target"
```

Do not run destructive commands on unvalidated input. Quoting preserves the argument as one value, but it does not by itself make an operation safe.

### Using single quotes when expansion is needed

```bash
printf '%s\n' '$HOME'   # Literal text
printf '%s\n' "$HOME"   # Value of HOME
```

### Assuming a variable is available in a child command

```bash
APP_ENV="test"
bash -c 'printf "%s\n" "$APP_ENV"'  # Not exported to the child
```

Export it if the child process needs it.

## 9. Practice

1. Create variables for a service name and environment, then print both in one sentence.
2. Set a counter to `1`, increment it using arithmetic expansion, and print the result.
3. Set a path containing a space and pass it as one argument to `printf`.
4. Write a script that greets the first argument, using `Guest` when no argument is supplied.
5. Export a variable and verify that a child Bash process can read it.

## Quick revision

- Assign with `name=value`; do not add spaces around `=`.
- Expand values with `$name` or `${name}`.
- Quote expansions with double quotes by default.
- Bash variables hold text; arithmetic contexts interpret suitable values as integers.
- Use `local` inside functions to avoid accidental global changes.
- Use `export` to pass a variable to child processes.
- Use `${value:-default}` to provide a fallback when a variable is unset or empty.

## References

- [Bash Reference Manual: Shell Parameters](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameters.html)
- [Bash Reference Manual: Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)
- [Bash Reference Manual: Shell Arithmetic](https://www.gnu.org/software/bash/manual/html_node/Shell-Arithmetic.html)
