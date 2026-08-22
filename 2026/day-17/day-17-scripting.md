# Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## Objective

Today I expanded my Bash scripting skills by practicing loops, command-line arguments, package automation, and basic error handling on an AWS EC2 Ubuntu server.

I worked with:

- `for` and `while` loops
- Command-line arguments (`$1`, `$#`, `$@`, `$0`)
- Package checking with `dpkg`
- Root permission validation
- Error handling using `set -e` and `||`

---

## Environment

- Platform: AWS EC2
- Operating System: Ubuntu Linux
- Shell: Bash

---

## Task 1 – For Loop

### Fruit Loop Script

I created `for_loop.sh` to loop through a list of fruits.

### Commands

```bash
nano for_loop.sh
chmod +x for_loop.sh
./for_loop.sh
```

### Output

```text
Apple
Banana
Mango
Orange
Grapes
```

### Counting Script

I created `count.sh` to print numbers from 1 to 10.

### Commands

```bash
nano count.sh
chmod +x count.sh
./count.sh
```

### Output

```text
1
2
3
4
5
6
7
8
9
10
```

### What I Learned

- `for` loops execute repeated tasks efficiently.
- Numeric ranges make repetitive operations simpler.

---

## Task 2 – While Loop

I created `countdown.sh` to count down from a user-provided number.

### Commands

```bash
nano countdown.sh
chmod +x countdown.sh
./countdown.sh
```

### My Input

```text
Enter a number: 1
```

### Output

```text
1
0
Done!
```

### What I Learned

- `while` loops continue until a condition becomes false.
- Variables can be updated during each iteration.

---

## Task 3 – Command-Line Arguments

### Greeting Script

I modified `greet.sh` to accept a command-line argument while still supporting interactive input.

### Commands

```bash
nano greet.sh
./greet.sh
./greet.sh ANUSHKA
```

### Output

Without argument:

```text
Usage: ./greet.sh <name>
Enter your name: ANUSHKA
Enter your favourite tool: DOCKER
Hello ANUSHKA, your favourite tool is DOCKER.
```

With argument:

```text
Hello, ANUSHKA!
Enter your name: ANUSHKA
Enter your favourite tool: DOCKER
Hello ANUSHKA, your favourite tool is DOCKER.
```

### Arguments Demo

I created `args_demo.sh` to display script arguments.

### Commands

```bash
nano args_demo.sh
chmod +x args_demo.sh
./args_demo.sh Docker Linux Bash
```

### Output

```text
Script name: ./args_demo.sh
Total arguments: 3
Arguments: Docker Linux Bash
```

### What I Learned

- `$1` stores the first argument.
- `$#` counts the total number of arguments.
- `$@` displays all arguments.
- `$0` prints the script name.

---

## Task 4 – Package Installation Script

I created `install_packages.sh` to check whether packages were already installed before attempting installation.

### Commands

```bash
sudo -i

nano install_packages.sh
chmod +x install_packages.sh
./install_packages.sh

exit
```

### Output

```text
nginx is already installed.
curl is already installed.
wget is already installed.
```

### What I Learned

- `dpkg -s` checks whether a package is installed.
- Root validation prevents running installation scripts without proper permissions.
- Automation reduces manual package management work.

---

## Task 5 – Error Handling

I created `safe_script.sh` using `set -e` to improve script reliability.

### Commands

```bash
nano safe_script.sh
chmod +x safe_script.sh
./safe_script.sh
./safe_script.sh
```

### First Run

```text
Script completed successfully.
```

### Second Run

```text
mkdir: /tmp/devops-test: File exists
Directory already exists
Script completed successfully.
```

### What I Learned

- `set -e` exits when unexpected errors occur.
- `||` provides fallback messages when commands fail.
- Error handling makes scripts safer for automation.

---

## Scripts Created

| Script | Purpose |
|---------|---------|
| `for_loop.sh` | Loop through a list of fruits |
| `count.sh` | Print numbers 1–10 |
| `countdown.sh` | Countdown using a while loop |
| `greet.sh` | Practice command-line arguments |
| `args_demo.sh` | Display Bash arguments |
| `install_packages.sh` | Check and install packages |
| `safe_script.sh` | Practice error handling |

---

## Verification

I verified that all scripts were created successfully.

### Command

```bash
ls -l *.sh
```

### Output

```text
-rwxrwxr-x 1 ubuntu ubuntu  86 args_demo.sh
-rw-rw-r-- 1 ubuntu ubuntu  98 arguments.sh
-rwxrwxr-x 1 ubuntu ubuntu 164 check_number.sh
-rwxrwxr-x 1 ubuntu ubuntu  52 count.sh
-rwxrwxr-x 1 ubuntu ubuntu 120 countdown.sh
-rwxrwxr-x 1 ubuntu ubuntu 136 file_check.sh
-rwxrwxr-x 1 ubuntu ubuntu  84 for_loop.sh
-rwxrwxr-x 1 ubuntu ubuntu 222 greet.sh
-rwxrwxr-x 1 ubuntu ubuntu 158 hello.sh
-rwxrwxr-x 1 ubuntu ubuntu 213 safe_script.sh
-rwxrwxr-x 1 ubuntu ubuntu 302 server_check.sh
-rwxrwxr-- 1 ubuntu ubuntu 352 show_variables.sh
-rwxrwxr-x 1 ubuntu ubuntu 124 variables.sh
```

The output confirmed that all newly created scripts had executable permissions.

---

## Commands Used

```bash
cd ~

nano for_loop.sh
chmod +x for_loop.sh
./for_loop.sh

nano count.sh
chmod +x count.sh
./count.sh

nano countdown.sh
chmod +x countdown.sh
./countdown.sh

nano greet.sh
./greet.sh
./greet.sh ANUSHKA

nano args_demo.sh
chmod +x args_demo.sh
./args_demo.sh Docker Linux Bash

sudo -i
nano install_packages.sh
chmod +x install_packages.sh
./install_packages.sh
exit

nano safe_script.sh
chmod +x safe_script.sh
./safe_script.sh
./safe_script.sh

ls -l *.sh
```

---

## What I Learned

- `for` and `while` loops automate repetitive tasks.
- Command-line arguments make Bash scripts reusable.
- `$1`, `$#`, `$@`, and `$0` are essential Bash variables.
- Package validation prevents unnecessary installations.
- `set -e` and `||` improve script reliability and error handling.

---

## DevOps Takeaway

Shell scripting is one of the most important DevOps skills because it transforms manual Linux administration into repeatable automation.

Today's exercises showed how loops, arguments, package checks, and error handling can be combined to create reliable scripts for real-world server management and deployment tasks.

---

## Evidence

Capture these screenshots for your GitHub repository:

- `for-loop.png`
- `count-loop.png`
- `countdown.png`
- `greet-arguments.png`
- `args-demo.png`
- `install-packages.png`
- `safe-script.png`
- `scripts-list.png`

---

## Day 17 Summary

Today I built seven Bash scripts covering loops, command-line arguments, package management, and error handling. This strengthened my scripting foundation and moved me closer to writing production-ready automation scripts used in real DevOps workflows.
