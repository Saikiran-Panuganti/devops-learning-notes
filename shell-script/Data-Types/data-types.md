# Data Types in Shell Scripting (Bash)

In Bash, variables do not need a predefined data type. Bash mainly treats variables as strings, but it can also perform integer arithmetic and work with arrays.

## Types of data in Bash

| Type | Description | Example |
| --- | --- | --- |
| String | Stores text | `NAME="Saikiran"` |
| Integer | Whole number used in arithmetic | `AGE=27` |
| Indexed array | Stores multiple values | `TOOLS=("Docker" "AWS" "Git")` |
| Associative array | Stores key-value pairs | `declare -A USER` |
| Boolean-like value | Uses `true`/`false` or `0`/`1` conventions | `STATUS=true` |

**Note:** Bash has no strict data types like Python or Java. For example, `AGE=27` is a variable assignment; arithmetic operations interpret its value numerically.

## Real-time examples

### 1. String

```bash
#!/bin/bash

NAME="Saikiran"
ROLE="DevOps Engineer"

echo "Name: $NAME"
echo "Role: $ROLE"
```

Output:

```text
Name: Saikiran
Role: DevOps Engineer
```

**Use case:** Store usernames, application names, and environment names.

### 2. Integer

```bash
#!/bin/bash

NUM1=10
NUM2=20

TOTAL=$((NUM1 + NUM2))

echo "Total: $TOTAL"
```

Output:

```text
Total: 30
```

**Use case:** Calculate the number of servers, deployments, or failed jobs.

### 3. Indexed array

```bash
#!/bin/bash

TOOLS=("Docker" "Kubernetes" "Terraform")

echo "First tool: ${TOOLS[0]}"
echo "All tools: ${TOOLS[@]}"
```

Output:

```text
First tool: Docker
All tools: Docker Kubernetes Terraform
```

**Use case:** Store multiple server names, tools, or environments.

### 4. Associative array

Associative arrays store values using named keys and require Bash 4 or later.

```bash
#!/bin/bash

declare -A SERVER
SERVER[dev]="Development"
SERVER[prod]="Production"

echo "${SERVER[dev]}"
echo "${SERVER[prod]}"
```

Output:

```text
Development
Production
```

**Use case:** Map environment names to their descriptions or configuration values.

### 5. Boolean-like value

Bash does not have a native Boolean variable type. Scripts commonly use values such as `true` and `false` by convention.

```bash
#!/bin/bash

DEPLOYMENT_STATUS=true

if [ "$DEPLOYMENT_STATUS" = "true" ]; then
    echo "Deployment successful"
else
    echo "Deployment failed"
fi
```

Output:

```text
Deployment successful
```

**Use case:** Check deployment status or enable and disable script options.

## Quick notes

- **String:** Stores text values.
- **Integer:** Supports arithmetic operations using `$(( ))`.
- **Indexed array:** Stores multiple values using numeric indexes.
- **Associative array:** Stores key-value pairs.
- **Boolean-like value:** Uses conventions such as `true` and `false`; these are not native Boolean data types in Bash.

**Important:** Bash does not have native floating-point arithmetic. For decimal calculations, use tools such as `bc` or Python.