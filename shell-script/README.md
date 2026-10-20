# Shell Scripting

This folder is a step-by-step guide to writing and understanding Bash scripts for Linux and DevOps tasks. Each lesson will focus on one concept and include explanations, runnable examples, common mistakes, and practice questions.

> **Scope:** Examples in this learning path use Bash. Bash is a particular shell; not every feature shown here is available in POSIX `sh` or other shells.

## Learning path

| Order | Topic | Status |
| --- | --- | --- |
| 1 | [Variables](./variables.md) | Available |
| 2 | Data types and values | Planned |
| 3 | Input, output, and redirection | Planned |
| 4 | Quoting and expansions | Planned |
| 5 | Conditions and tests | Planned |
| 6 | Loops | Planned |
| 7 | Functions and scope | Planned |
| 8 | Arrays | Planned |
| 9 | Script arguments and options | Planned |
| 10 | Exit status and error handling | Planned |
| 11 | Files, directories, and text processing | Planned |
| 12 | Processes, signals, and job control | Planned |
| 13 | Debugging, logging, and shellcheck | Planned |
| 14 | Practical automation scripts | Planned |

## What you will learn

By the end of this path, you should be able to read and write small Bash scripts, handle inputs and failures deliberately, combine common Linux commands safely, and apply these skills to repeatable DevOps tasks.

## How to practice

- Use a Bash environment, such as Linux, macOS, WSL, or a suitable container.
- Save examples as `.sh` files and run them with `bash filename.sh`.
- For scripts you own, you can make a script executable with `chmod +x filename.sh` and run it as `./filename.sh`.
- Try the practice questions before reading or writing a solution.
- Test scripts with harmless sample data before using them on important files or systems.

## Recommended conventions

- Use `#!/usr/bin/env bash` for Bash scripts.
- Quote variable expansions by default, for example `"$name"`.
- Use meaningful variable names and explain non-obvious behavior.
- Treat external input as untrusted; validate it before using it in commands.
- Prefer explicit error checks and clear messages over silently ignoring failures.
- Do not put passwords, tokens, or private keys in scripts or notes.
