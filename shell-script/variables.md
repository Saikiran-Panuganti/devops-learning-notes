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

Use `$NAME` or `${NAME}` to access a variable's value.

```bash
echo "$NAME"
echo "${NAME}_backup"
```

Braces mark the end of a variable name when adjoining text could be mistaken as part of its name.

## Quoting

- Double quotes (`"$NAME"`) expand variables and preserve the value as one string.
- Single quotes (`'$NAME'`) preserve the text literally; variables are not expanded.
- Quote variable expansions by default to prevent word splitting and pathname expansion.

## Values and types

Bash variables do not have declared data types. They hold text; the operation using a value determines how it is interpreted. Bash arithmetic supports integers:

```bash
COUNT=$((COUNT + 1))
```

## Common special variables

| Variable | Meaning |
| --- | --- |
| `$0` | Script name or invocation path |
| `$1`, `$2`, ... | Positional arguments |
| `$#` | Number of positional arguments |
| `"$@"` | All positional arguments, kept as separate values when quoted |
| `$?` | Exit status of the most recently completed command |

## Remember

- Assign with `NAME=value`; spaces around `=` are not allowed.
- Use `$NAME` to access a value and quote expansions by default.
- Bash variables are not strongly typed.
- Use `local` for function-only variables and `export` to pass values to child processes.
- Keep hands-on scripts and exercises in the [DevOps hands-on labs](../../devops-hands-on-labs/README.md) repository.
