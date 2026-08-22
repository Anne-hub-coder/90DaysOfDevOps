# Day 18 – Shell Scripting: Functions & Intermediate Concepts

## Objective

Today I learned how to write cleaner and reusable Bash scripts by using functions, local variables, strict mode (`set -euo pipefail`), and a structured system information script.

I practiced:

- Creating reusable functions
- Passing arguments to functions
- Using local variables
- Understanding `set -euo pipefail`
- Building a modular system information script

---

## Environment

- Platform: AWS EC2
- Operating System: Ubuntu 26.04 LTS
- Shell: Bash

---

## Task 1 – Basic Functions

I created `functions.sh` containing two reusable functions.

- `greet()` prints a greeting using a name argument.
- `add()` adds two numbers and prints their sum.

### Commands

```bash
cd ~

nano functions.sh
chmod +x functions.sh
./functions.sh
```

### Output

```text
Hello, ANUSHKA!
Sum: 30
```

### What I Learned

- Functions help avoid repeating code.
- Function arguments are accessed using `$1`, `$2`, etc.
- Scripts become easier to maintain when logic is separated into reusable functions.

---

## Task 2 – Disk & Memory Functions

I created `disk_check.sh` to collect system information through reusable functions.

### Commands

```bash
nano disk_check.sh
chmod +x disk_check.sh
./disk_check.sh
```

### Output

```text
===== Disk Usage =====
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        13G  3.5G  9.0G  28% /

===== Memory Usage =====
               total        used        free      shared  buff/cache   available
Mem:           908Mi       801Mi        62Mi       457Mi       607Mi       106Mi
Swap:             0B          0B          0B
```

### What I Learned

- `df -h` displays disk usage in a human-readable format.
- `free -h` shows memory usage clearly.
- Functions can organize multiple system checks inside one script.

---

## Task 3 – Strict Mode (`set -euo pipefail`)

I created `strict_demo.sh` to understand Bash strict mode.

### Commands

```bash
nano strict_demo.sh
chmod +x strict_demo.sh
./strict_demo.sh
```

### Output

```text
Testing strict mode...
Trying undefined variable...
./strict_demo.sh: line 8: MY_VAR: unbound variable
```

### Understanding Strict Mode

| Flag | Purpose |
|------|---------|
| `set -e` | Exit immediately if any command fails. |
| `set -u` | Treat undefined variables as errors. |
| `set -o pipefail` | Fail the entire pipeline if any command fails. |

### What I Learned

- Strict mode prevents silent failures.
- Undefined variables immediately stop execution.
- It makes automation scripts much safer for production environments.

---

## Task 4 – Local Variables

I created `local_demo.sh` to compare local and global variables.

### Commands

```bash
nano local_demo.sh
chmod +x local_demo.sh
./local_demo.sh
```

### Output

```text
Inside function: DevOps
Outside function: GLOBAL
```

### What I Learned

- `local` variables exist only inside a function.
- Global variables remain available throughout the script.
- Local variables reduce unexpected side effects.

---

## Task 5 – System Information Reporter

I created `system_info.sh`, a complete Bash utility that combines multiple reusable functions.

The script reports:

- Hostname
- Operating System
- Uptime
- Disk usage
- Memory usage
- Top CPU-consuming processes

### Commands

```bash
nano system_info.sh
chmod +x system_info.sh
./system_info.sh
```

### Output

```text
===== Hostname & OS =====
ip-172-31-33-72
PRETTY_NAME="Ubuntu 26.04 LTS"

===== Uptime =====
12:52:22 up 1 day, 5:58, 1 user, load average: 0.00, 0.00, 0.00

===== Disk Usage =====
Filesystem       Size  Used Avail Use% Mounted on
/dev/root         13G  3.5G  9.0G  28% /
tmpfs            455M     0  455M   0% /dev/shm
tmpfs            182M  940K  181M   1% /run
efivarfs         128K  3.3K  120K   3% /sys/firmware/efi/efivars

===== Memory Usage =====
               total        used        free      shared  buff/cache   available
Mem:           908Mi       801Mi        62Mi       457Mi       607Mi       107Mi
Swap:             0B          0B          0B

===== Top CPU Processes =====
    PID COMMAND         %CPU
    724 containerd       0.1
   8569 kworker/0:2-eve  0.0
   8386 kworker/1:1-eve  0.0
   8875 systemd          0.0
    633 snapd            0.0
```

### What I Learned

- A `main()` function keeps script execution organized.
- Breaking scripts into functions improves readability.
- System monitoring tasks can be combined into one reusable utility.

---

## Scripts Created

| Script | Purpose |
|---------|---------|
| `functions.sh` | Greeting and addition functions |
| `disk_check.sh` | Disk and memory reporting |
| `strict_demo.sh` | Practice Bash strict mode |
| `local_demo.sh` | Compare local vs global variables |
| `system_info.sh` | Complete system information utility |

---

## Verification

I verified that all newly created scripts had executable permissions.

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
-rwxrwxr-x 1 ubuntu ubuntu 179 disk_check.sh
-rwxrwxr-x 1 ubuntu ubuntu 136 file_check.sh
-rwxrwxr-x 1 ubuntu ubuntu  84 for_loop.sh
-rwxrwxr-x 1 ubuntu ubuntu 113 functions.sh
-rwxrwxr-x 1 ubuntu ubuntu 222 greet.sh
-rwxrwxr-x 1 ubuntu ubuntu 158 hello.sh
-rwxrwxr-x 1 ubuntu ubuntu 156 local_demo.sh
-rwxrwxr-x 1 ubuntu ubuntu 213 safe_script.sh
-rwxrwxr-x 1 ubuntu ubuntu 302 server_check.sh
-rwxrwxr-- 1 ubuntu ubuntu 352 show_variables.sh
-rwxrwxr-x 1 ubuntu ubuntu 153 strict_demo.sh
-rwxrwxr-x 1 ubuntu ubuntu 574 system_info.sh
-rwxrwxr-x 1 ubuntu ubuntu 124 variables.sh
```

The output confirmed that all scripts were successfully created and were executable.

---

## Commands Used

```bash
cd ~

nano functions.sh
chmod +x functions.sh
./functions.sh

nano disk_check.sh
chmod +x disk_check.sh
./disk_check.sh

nano strict_demo.sh
chmod +x strict_demo.sh
./strict_demo.sh

nano local_demo.sh
chmod +x local_demo.sh
./local_demo.sh

nano system_info.sh
chmod +x system_info.sh
./system_info.sh

ls -l *.sh
```

---

## What I Learned

- Functions make Bash scripts reusable and easier to maintain.
- Local variables prevent unintended changes outside functions.
- `set -euo pipefail` makes scripts safer by stopping on errors.
- `df -h` and `free -h` are useful system monitoring commands.
- A `main()` function improves script organization and readability.

---

## DevOps Takeaway

Modern DevOps automation depends heavily on well-structured Bash scripts.

Using functions, strict mode, and modular design creates scripts that are easier to debug, safer to run, and more suitable for production environments.

---

## Evidence

Capture these screenshots for your GitHub repository:

- `functions-script.png`
- `disk-check.png`
- `strict-demo.png`
- `local-demo.png`
- `system-info.png`
- `scripts-list.png`

---

## Day 18 Summary

Today I moved beyond basic shell scripting by writing reusable functions, working with local variables, understanding Bash strict mode, and building a modular system information script.

These concepts form the foundation for writing reliable automation scripts used in real DevOps workflows.
