# ANSI Color Codes in Bash

## Definition

ANSI escape codes are special character sequences that tell a terminal how to
display text. They can add colors and styles such as bold text.

## Purpose

Colors can make terminal messages easier to scan. For example, a script can
show success in green, warnings in yellow, and errors in red.

### DevOps perspective

Color codes are often used to make deployment output, status messages, and
troubleshooting information easier to distinguish. Some CI/CD systems or
terminals do not display colors, so scripts should keep their messages
understandable without color as well.

## Basic color format

A common format for a color code is:

```text
\033[CODEm
```

- `\033` represents the Escape character.
- `[` begins the formatting instruction.
- `CODE` selects a color or style.
- `m` ends the instruction.

Use the reset code `\033[0m` after colored text so later output returns to the
terminal's normal style.

## Common foreground colors

| Color | Code |
| --- | --- |
| Black | `\033[30m` |
| Red | `\033[31m` |
| Green | `\033[32m` |
| Yellow | `\033[33m` |
| Blue | `\033[34m` |
| Magenta | `\033[35m` |
| Cyan | `\033[36m` |
| White | `\033[37m` |
| Reset | `\033[0m` |

## Your first color example

Use `printf` to print a green message and then reset the color:

```bash
#!/usr/bin/env bash

printf '\033[32mDeployment successful\033[0m\n'
```

The words `Deployment successful` should appear in green. The `\n` starts a
new line, and `\033[0m` resets the color so later text is not green.

## Store colors in variables

Variables make color codes easier to reuse and understand:

```bash
#!/usr/bin/env bash

RED='\033[31m'
GREEN='\033[32m'
YELLOW='\033[33m'
RESET='\033[0m'

printf "${GREEN}SUCCESS: Deployment completed.${RESET}\n"
printf "${YELLOW}WARNING: Check the service status.${RESET}\n"
printf "${RED}ERROR: Deployment failed.${RESET}\n"
```

The color variable goes before the message. Always add the reset code after
the colored part to avoid coloring later output.

## Add a text style

ANSI codes can also apply styles. For example, `1` enables bold text:

```bash
BOLD='\033[1m'
RESET='\033[0m'

printf "${BOLD}Important message${RESET}\n"
```

## One-line DevOps example

```bash
RED='\033[31m'
RESET='\033[0m'

printf "${RED}ERROR: Deployment failed.${RESET}\n"
```

This displays the error message in red when the terminal supports ANSI colors.

## Daily-life comparison

Think of traffic signals:

- Green means go or success.
- Yellow means caution or warning.
- Red means stop or error.

Color-coded terminal messages use the same idea to make a status easier to
notice. The text itself should still clearly explain the status.

## Common beginner mistakes

- **Forgetting the reset code:** later terminal output may keep the same color.
- **Using `echo -e` everywhere:** `echo` handles escape sequences differently
  across shells. Bash `printf` is a more predictable choice.
- **Expecting color in every terminal:** some terminals and CI logs disable or
  do not support ANSI colors.
- **Using color as the only signal:** include words such as `SUCCESS`,
  `WARNING`, or `ERROR` so the message remains clear without color.