# Special Variables

Special variables are predefined variables that provide information about script arguments, process IDs, exit statuses, directories, and execution time. They help automate real-time DevOps tasks without manually defining every variable.

## Important special variables

| Variable | Meaning | DevOps use |
| --- | --- | --- |
| `$0` | Script name or invocation path | Identify which script is running |
| `$1`, `$2`, ... | First, second, and later arguments | Pass environment names, filenames, or other inputs |
| `"$@"` | All arguments, preserving each as a separate value when quoted | Process multiple inputs safely |
| `"$*"` | All arguments combined into one word when quoted | Handle arguments together as a single string |
| `$#` | Number of arguments | Validate required inputs |
| `$$` | Process ID of the current shell | Identify the running script process |
| `$!` | Process ID of the most recently started background job | Track a background task |
| `$?` | Exit status of the most recently completed command | Check command success or failure |
| `$LINENO` | Current line number in the script | Locate a line during debugging |
| `$SECONDS` | Seconds since the current Bash shell started | Measure approximate script runtime |
| `$USER` | Common environment variable containing the current username | Display or use the executing user's name |
| `$HOME` | Current user's home directory | Locate user-specific files |
| `$PWD` | Current working directory | Identify the directory the script is running from |
| `$(realpath "$0")` | Command substitution that prints the resolved path of the script | Locate the script file |

## Remember

- `"$@"` preserves each argument separately; `"$*"` combines them into one word.
- Check `$?` immediately after the command whose status you need to inspect.
- Capture `$!` immediately after starting a background process.
- `$PWD` is the current working directory, not necessarily the directory containing the script.
- `$USER` is an environment variable, and `realpath` is an external command; neither is a Bash special parameter.
- `$SECONDS` measures time since the Bash shell started, which may be earlier than the script's start time.
- `$0` may be a relative path or command name; `realpath "$0"` requires `realpath` to be installed and the path to resolve.

`$@`, `$*`, `$#`, `$?`, `$$`, and `$!` are commonly asked about in DevOps interviews.
