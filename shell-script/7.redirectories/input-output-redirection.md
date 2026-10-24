# Input and Output Redirection

## Definition

Input and output redirection in shell scripting controls where a command reads
input and where it sends output, instead of using the keyboard and screen.

## Purpose

Redirection helps automate tasks by reading data from files and saving command
results or errors to files for logging, reporting, and troubleshooting.

### DevOps perspective

In DevOps, redirection is commonly used to:

- Store application logs.
- Save script execution results.
- Capture errors for debugging.
- Support automated backup and monitoring tasks.
- Generate reports during CI/CD pipelines.

### Real-time example

To save disk usage information to a report file instead of displaying it in
the terminal, run:

```bash
df -h > disk_report.txt
```

The `>` operator redirects standard output to `disk_report.txt`. It creates
the file if it does not exist and overwrites its contents if it does.

> These examples use Bash. The `&>` and `&>>` operators are Bash syntax.

## Common redirection operators

| Operator | Purpose |
| --- | --- |
| `>` | Redirect standard output to a file, replacing existing contents |
| `>>` | Append standard output to a file |
| `<` | Read standard input from a file |
| `2>` | Redirect standard error to a file, replacing existing contents |
| `&>` | Redirect both standard output and standard error to a file |

## Standard input, output, and error

Every command starts with three standard data streams:

| File descriptor | Name | Default destination |
| --- | --- | --- |
| `0` | Standard input (`stdin`) | Keyboard |
| `1` | Standard output (`stdout`) | Terminal; normally used for successful output |
| `2` | Standard error (`stderr`) | Terminal; normally used for error messages |

The number before a redirection operator selects the stream. If no number is
given for output redirection, Bash uses descriptor `1`.

## Write output to a file: `>` and `>>`

The `>` operator sends standard output to a file. It creates the file if it
does not exist, and **replaces the existing contents** if it does:

```bash
echo "First message" > output.log
```

The `>>` operator appends standard output to the end of a file, keeping its
existing contents:

```bash
echo "Another message" >> output.log
```

These are equivalent to `1>` and `1>>` because standard output is descriptor
`1`:

```bash
echo "Saved to stdout.log" 1> stdout.log
echo "Appended to stdout.log" 1>> stdout.log
```

## Redirect errors: `2>` and `2>>`

Use `2>` to write standard error to a file. Like `>`, it replaces the file's
contents:

```bash
some_command 2> errors.log
```

Use `2>>` to append errors instead:

```bash
some_command 2>> errors.log
```

## Redirect output and errors together

In Bash, `&>` sends both standard output and standard error to the same file,
replacing its contents:

```bash
some_command &> command.log
```

Use `&>>` to append both streams instead:

```bash
some_command &>> command.log
```

The longer equivalent form for appending both streams is:

```bash
some_command >> command.log 2>&1
```

Here, `2>&1` sends standard error to the same destination as standard output.
The order matters: first redirect standard output to the file, then redirect
standard error to that output destination.

## Redirect input: `<`

The `<` operator gives a command its input from a file instead of the keyboard:

```bash
sort < names.txt
```

## Show output and save it with `tee`

Normally, redirecting output to a file means you do not see it in the terminal.
`tee` writes output to the terminal and a file at the same time:

```bash
echo "Installation succeeded" | tee -a install.log
```

The `-a` option tells `tee` to append to the file. Without `-a`, `tee` replaces
the file's contents. The `|` pipe sends the output from `echo` into `tee`.

To save both output and errors while still showing them in the terminal:

```bash
some_command 2>&1 | tee -a command.log
```

## Quick reference

| Syntax | Effect |
| --- | --- |
| `command > file` | Write stdout to a file; replace existing contents |
| `command >> file` | Append stdout to a file |
| `command 2> file` | Write stderr to a file; replace existing contents |
| `command 2>> file` | Append stderr to a file |
| `command &> file` | Write stdout and stderr to a file; replace existing contents |
| `command &>> file` | Append stdout and stderr to a file |
| `command < file` | Read command input from a file |
| `command \| tee -a file` | Display stdout and append it to a file |
| `command 2>&1` | Send stderr to the current stdout destination |
