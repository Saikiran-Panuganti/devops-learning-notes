# Variables

## What is a variable?

A variable in shell scripting is a named memory location used to store and reuse data during script execution.

## Assignment

```bash
NAME="value"
```

- Do not put spaces around `=`.
- Variable names are case-sensitive: `NAME` and `name` are different.
- Names commonly use uppercase letters for configuration values and lowercase for local script variables.

## Expansion

Use `$NAME` or `${NAME}` to access a variable's value:

```bash
USER="devops"

echo "$USER"
echo "${USER}_team"
```

Output:

```text
devops
devops_team
```

Braces clearly mark where the variable name ends. Without braces, `$USER_team` refers to a different variable named `USER_team`, not the value of `USER` followed by `_team`.

## Quoting

- Double quotes (`"$NAME"`) expand variables and preserve the value as one string.
- Single quotes (`'$NAME'`) preserve the text literally; variables are not expanded.
- Quote variable expansions by default to prevent word splitting and pathname expansion.


## Remember

- Assign with `NAME=value`; spaces around `=` are not allowed.
- Use `$NAME` to access a value and quote expansions by default.
- Bash variables are not strongly typed.
- Use `local` for function-only variables and `export` to pass values to child processes.
- Keep hands-on scripts and exercises in the [DevOps hands-on labs](../../devops-hands-on-labs/README.md) repository.
