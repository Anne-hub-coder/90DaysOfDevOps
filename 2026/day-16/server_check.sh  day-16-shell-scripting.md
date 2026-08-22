# Day 16 – Shell Scripting Basics

## Objective

Today I learned the fundamentals of Bash shell scripting by creating and executing multiple scripts on an AWS EC2 Ubuntu server.

I practiced:

- Creating executable Bash scripts
- Using the shebang (`#!/bin/bash`)
- Working with variables
- Taking user input using `read`
- Writing `if-else` conditions
- Checking file existence
- Verifying service status with `systemctl`

---

## Environment

- Platform: AWS EC2
- Operating System: Ubuntu Linux
- Shell: Bash

---

## Task 1 – My First Script

I created `hello.sh` with a shebang and simple `echo` statements.

### Commands

```bash
nano hello.sh
chmod +x hello.sh
./hello.sh
```

### Output

```text
harry says, hello ron and hermionie
Ron says, hey hey, is there some food
hermionie says, there is some dirt on your nose
```

### What I Learned

- `#!/bin/bash` tells Linux which interpreter should execute the script.
- `chmod +x` makes a script executable.
- `./hello.sh` runs the script from the current directory.

---

## Task 2 – Variables

I created `variables.sh` to practice Bash variables.

### Commands

```bash
nano variables.sh
chmod +x variables.sh
./variables.sh
```

### Output

```text
Hello, I am ANUSHKA and I am a DevOps Engineer
Hello, I am $NAME and I am a $ROLE
```

### Observation

- Double quotes (`""`) expand variables.
- Single quotes (`''`) print variables as plain text.

---

## Task 3 – User Input with `read`

I created `greet.sh` to accept user input.

### Commands

```bash
nano greet.sh
chmod +x greet.sh
./greet.sh
```

### Input

```text
Enter your name: ANUSHKA
Enter your favourite tool: DOCKER
```

### Output

```text
Hello ANUSHKA, your favourite tool is DOCKER.
```

### What I Learned

- `read` captures user input.
- Variables can be reused later in the script.

---

## Task 4 – If-Else Conditions

### Number Check Script

I created `check_number.sh` to determine whether a number is positive, negative, or zero.

#### Commands

```bash
nano check_number.sh
chmod +x check_number.sh
./check_number.sh
```

### Input

```text
Enter a number: 10
```

### Output

```text
Positive
```

The script correctly identified that `10` is a positive number.

### File Check Script

I created `file_check.sh` to verify whether a file exists.

#### Commands

```bash
nano file_check.sh
chmod +x file_check.sh
./file_check.sh
```

### Test 1

Input:

```text
Enter filename: K89
```

Output:

```text
File does not exist.
```

### Test 2

Input:

```text
Enter filename: notes.txt
```

Output:

```text
File exists.
```

### What I Learned

- `-f` checks whether a file exists.
- Conditional statements help automate common Linux checks.

---

## Task 5 – Service Status Script

I created `server_check.sh` to verify whether the Nginx service was running.

### Commands

```bash
nano server_check.sh
chmod +x server_check.sh
./server_check.sh
```

### Input

```text
Do you want to check the status of nginx? (y/n): y
```

### Output

```text
nginx is active.
```

### What I Learned

- Scripts can combine variables, user input, and system commands.
- `systemctl is-active` is useful for checking service health.

---

## Scripts Created

| Script | Purpose |
|---------|---------|
| `hello.sh` | Print greeting messages |
| `variables.sh` | Practice Bash variables |
| `greet.sh` | Take user input |
| `check_number.sh` | Check positive, negative, or zero |
| `file_check.sh` | Verify file existence |
| `server_check.sh` | Check Nginx service status |

---

## Verification

I verified all the scripts created during today's practice.

### Command

```bash
ls -l *.sh
```

### Output

```text
-rw-rw-r-- 1 ubuntu ubuntu  98 arguments.sh
-rwxrwxr-x 1 ubuntu ubuntu 164 check_number.sh
-rwxrwxr-x 1 ubuntu ubuntu 136 file_check.sh
-rwxrwxr-x 1 ubuntu ubuntu 127 greet.sh
-rwxrwxr-x 1 ubuntu ubuntu 158 hello.sh
-rwxrwxr-x 1 ubuntu ubuntu 302 server_check.sh
-rwxrwxr-- 1 ubuntu ubuntu 352 show_variables.sh
-rwxrwxr-x 1 ubuntu ubuntu 124 variables.sh
```

The output confirmed that the scripts I created are executable.

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

- The shebang determines which interpreter executes a script.
- `chmod +x` is required before executing custom scripts.
- Variables behave differently with single and double quotes.
- `read` enables interactive scripts.
- `if-else` conditions automate decision-making.
- File checks (`-f`) and service checks (`systemctl`) are practical DevOps scripting skills.

---

## DevOps Takeaway

Shell scripting is one of the most valuable skills in DevOps because it helps automate repetitive tasks like checking services, validating files, collecting user input, and performing system health checks.

Instead of running multiple commands manually, a Bash script can combine them into a reusable automation workflow.

---

## Evidence

Capture these screenshots for your GitHub repository:

- `hello-script.png`
- `variables-script.png`
- `greet-script.png`
- `check-number.png`
- `file-check.png`
- `server-check.png`
- `scripts-list.png`

---

## Day 16 Summary

Today I built six Bash scripts that introduced me to core shell scripting concepts including variables, user input, conditional logic, and service monitoring.

This gave me practical experience writing Bash scripts that can automate common Linux administration tasks used in real DevOps environments.
