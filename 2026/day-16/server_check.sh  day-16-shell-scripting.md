# Day 16 – Shell Scripting Basics

## Objective

Today I started writing Bash shell scripts by learning how to use the Bash interpreter, variables, user input, conditional statements, and simple automation scripts for Linux administration.

I practiced these concepts on an AWS EC2 Ubuntu server.

---

## Task 1 – My First Script

### Script: `hello.sh`

```bash
#!/bin/bash
echo "Hello, DevOps!"
```

### Commands Used

```bash
chmod +x hello.sh
./hello.sh
```

### Output

```text
Hello, DevOps!
```

### What happens without the shebang?

Without `#!/bin/bash`, the script may still run from the current shell, but the operating system doesn't know which interpreter should execute it when run directly.

---

## Task 2 – Variables

### Script: `variables.sh`

```bash
#!/bin/bash

NAME="Manish"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"

echo 'Single quotes: $NAME'
echo "Double quotes: $NAME"
```

### Output

```text
Hello, I am Manish and I am a DevOps Engineer
Single quotes: $NAME
Double quotes: Manish
```

### Difference

- **Single quotes** treat variables as plain text.
- **Double quotes** expand variable values.

---

## Task 3 – User Input

### Script: `greet.sh`

```bash
#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL."
```

### Example Output

```text
Enter your name: Manish
Enter your favourite tool: Docker

Hello Manish, your favourite tool is Docker.
```

---

## Task 4 – If-Else Conditions

### Script: `check_number.sh`

```bash
#!/bin/bash

read -p "Enter a number: " NUM

if [ "$NUM" -gt 0 ]; then
    echo "Positive"
elif [ "$NUM" -lt 0 ]; then
    echo "Negative"
else
    echo "Zero"
fi
```

### Example Output

| Input | Output |
|------|--------|
| 10 | Positive |
| -5 | Negative |
| 0 | Zero |

---

### Script: `file_check.sh`

```bash
#!/bin/bash

read -p "Enter filename: " FILE

if [ -f "$FILE" ]; then
    echo "File exists."
else
    echo "File does not exist."
fi
```

### Example Output

```text
Enter filename: notes.txt
File exists.
```

---

## Task 5 – Server Status Check

### Script: `server_check.sh`

```bash
#!/bin/bash

SERVICE="nginx"

read -p "Do you want to check the status of $SERVICE? (y/n): " CHOICE

if [ "$CHOICE" = "y" ]; then
    if systemctl is-active --quiet "$SERVICE"; then
        echo "$SERVICE is active."
    else
        echo "$SERVICE is not active."
    fi
else
    echo "Skipped."
fi
```

### Example Output

When entering `y`:

```text
nginx is active.
```

When entering `n`:

```text
Skipped.
```

---

## Commands Used

```bash
nano hello.sh
chmod +x hello.sh
./hello.sh

nano variables.sh
chmod +x variables.sh
./variables.sh

nano greet.sh
chmod +x greet.sh
./greet.sh

nano check_number.sh
chmod +x check_number.sh
./check_number.sh

nano file_check.sh
chmod +x file_check.sh
./file_check.sh

nano server_check.sh
chmod +x server_check.sh
./server_check.sh

ls -l *.sh
```

---

## What I Learned

- The shebang (`#!/bin/bash`) tells Linux which interpreter should execute a script.
- Variables become dynamic when used with double quotes.
- The `read` command accepts user input during script execution.
- `if`, `elif`, and `else` help scripts make decisions.
- Bash scripts can automate common Linux administration tasks like checking file existence and service health.

---

## DevOps Takeaway

Shell scripting is one of the core skills for DevOps engineers because repetitive tasks can be automated instead of being executed manually. Even simple scripts for checking services, validating files, or collecting system information can save time and reduce human error.

---

## Evidence

Screenshots collected during this exercise:

- `hello-script.png`
- `variables-script.png`
- `greet-script.png`
- `check-number.png`
- `file-check.png`
- `server-check.png`
- `scripts-list.png`

---

## Day 16 Summary

Today I built my foundation in Bash scripting by creating executable scripts, working with variables and user input, using conditional statements, and automating basic Linux tasks on my AWS EC2 server.
