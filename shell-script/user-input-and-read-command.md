# User Input and the `read` Command

In Bash/shell scripting, the `read` command accepts input from a user and stores it in a variable.

It is useful for interactive scripts that need usernames,passwords, environment names, confirmations, or other runtime values.

```bash
echo "Please enter your username:"
read -r USER_NAME

echo "Please enter your password:"
read -rs PASSWORD
```

| Command | Purpose |
| --- | --- |
| `read` | Accepts user input |
| `read -p` | Displays a prompt before accepting input |
| `read -s` | Hides input while typing |
| `echo` | Displays text in the terminal |
| `$VARIABLE_NAME` | Accesses a variable's value |