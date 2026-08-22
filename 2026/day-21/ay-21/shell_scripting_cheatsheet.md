# Day 21 – Shell Scripting Cheat Sheet

## Objective

Today I created my personal Bash scripting cheat sheet based on everything I practiced during Days 16–20 on my AWS EC2 Ubuntu instance. Instead of collecting theory alone, I included the commands, scripts, and patterns I actually used while building automation projects like backups, log rotation, system reporting, and log analysis.

---

# Quick Reference Table

| Topic | Key Syntax | My Example |
|--------|------------|------------|
| Shebang | `#!/bin/bash` | `hello.sh` |
| Variable | `NAME="ANUSHKA"` | `variables.sh` |
| User Input | `read -p` | `greet.sh` |
| Arguments | `$1`, `$#`, `$@` | `args_demo.sh`, `greet.sh` |
| If Statement | `if [ condition ]; then` | `file_check.sh` |
| For Loop | `for item in list; do` | `for_loop.sh` |
| While Loop | `while [ condition ]; do` | `countdown.sh` |
| Function | `greet() {}` | `functions.sh` |
| Strict Mode | `set -euo pipefail` | `strict_demo.sh`, `system_info.sh` |
| Grep | `grep pattern file` | `log_analyzer.sh` |
| Tar Backup | `tar -czf` | `backup.sh` |
| Find | `find -mtime` | `log_rotate.sh` |

---

# 1. Bash Basics

## Shebang

Every script I created started with:

```bash
#!/bin/bash
```

This tells Linux to execute the script using the Bash interpreter.

Example from my project:

- `hello.sh`
- `functions.sh`
- `backup.sh`
- `log_analyzer.sh`

---

## Running Scripts

I used these commands repeatedly:

```bash
chmod +x hello.sh
./hello.sh
```

Example output from my EC2:

```text
harry says, hello ron and hermionie
Ron says, hey hey, is there some food
hermionie says, there is some dirt on your nose
```

I also learned that:

```bash
bash script.sh
```

can run a script without executable permission.

---

## Comments

```bash
# This is a comment
```

Inline example:

```bash
echo "Hello"   # Prints Hello
```

---

## Variables

Example from my `variables.sh`:

```bash
NAME="ANUSHKA"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

Actual output:

```text
Hello, I am ANUSHKA and I am a DevOps Engineer
```

Single quotes vs double quotes:

```bash
echo "$NAME"
echo '$NAME'
```

Output:

```text
ANUSHKA
$NAME
```

---

## Reading User Input

Example from `greet.sh`:

```bash
read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL."
```

My output:

```text
Enter your name: ANUSHKA
Enter your favourite tool: DOCKER

Hello ANUSHKA, your favourite tool is DOCKER.
```

---

## Command-Line Arguments

I practiced:

| Variable | Meaning |
|----------|---------|
| `$0` | Script name |
| `$1` | First argument |
| `$#` | Total arguments |
| `$@` | All arguments |
| `$?` | Exit code |

Example:

```bash
./args_demo.sh Docker Linux Bash
```

Output:

```text
Script name: ./args_demo.sh
Total arguments: 3
Arguments: Docker Linux Bash
```

---

# 2. Operators & Conditionals

## String Comparisons

```bash
=
!=
-z
-n
```

Example:

```bash
if [ "$NAME" = "ANUSHKA" ]; then
    echo "Matched"
fi
```

---

## Integer Comparisons

I used:

```bash
-eq
-ne
-lt
-gt
-le
-ge
```

Example from `check_number.sh`.

Input:

```text
10
```

Output:

```text
Positive
```

---

## File Test Operators

| Operator | Meaning |
|----------|---------|
| `-f` | File exists |
| `-d` | Directory exists |
| `-e` | Exists |
| `-r` | Readable |
| `-w` | Writable |
| `-x` | Executable |
| `-s` | File has content |

Example from `file_check.sh`.

Input:

```text
notes.txt
```

Output:

```text
File exists.
```

Input:

```text
K89
```

Output:

```text
File does not exist.
```

---

## If-Else

Example:

```bash
if [ condition ]; then
    echo "True"
elif [ other ]; then
    echo "Other"
else
    echo "False"
fi
```

I used this in:

- `check_number.sh`
- `file_check.sh`
- `server_check.sh`
- `backup.sh`
- `log_analyzer.sh`

---

## Logical Operators

AND

```bash
command1 && command2
```

OR

```bash
command1 || echo "Failed"
```

NOT

```bash
! command
```

---

## Case Statement

Example syntax:

```bash
case "$choice" in
    y) echo "Yes";;
    n) echo "No";;
    *) echo "Invalid";;
esac
```

---

# 3. Loops

## For Loop

Example from `for_loop.sh`.

Output:

```text
Apple
Banana
Mango
Orange
Grapes
```

Example from `count.sh`.

Output:

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

---

## While Loop

Example from `countdown.sh`.

Input:

```text
1
```

Output:

```text
1
0
Done!
```

---

## Until Loop

Syntax:

```bash
until [ "$N" -eq 0 ]
do
    ...
done
```

---

## Loop Over Files

I later used this idea inside `log_rotate.sh`.

Example:

```bash
for file in *.log
```

---

## Loop Over Command Output

Example:

```bash
while read line
do
    echo "$line"
done
```

---

# 4. Functions

## Creating Functions

Example from `functions.sh`.

```bash
greet() {
    echo "Hello $1!"
}
```

Output:

```text
Hello, ANUSHKA!
```

---

## Function Arguments

Example:

```bash
add() {
    echo $(($1+$2))
}
```

Output:

```text
Sum: 30
```

---

## Return vs Echo

- `return` returns an exit status.
- `echo` returns actual data.

I used `echo` in my scripts for readable output.

---

## Local Variables

Example from `local_demo.sh`.

Output:

```text
Inside function: DevOps
Outside function: GLOBAL
```

This showed that `local` variables remain inside functions.

---

# 5. Text Processing Commands

These became my most-used DevOps tools.

## Grep

Real examples from `log_analyzer.sh`.

```bash
grep -E "ERROR|Failed"
grep -n "CRITICAL"
```

Useful flags:

- `-i`
- `-r`
- `-c`
- `-n`
- `-v`
- `-E`

---

## Awk

Example:

```bash
awk '{print $1}'
```

Useful for column extraction.

---

## Sed

Replace text:

```bash
sed 's/foo/bar/g'
```

Edit file:

```bash
sed -i 's/foo/bar/g'
```

---

## Cut

Example:

```bash
cut -d' ' -f4-
```

I used similar extraction while processing logs.

---

## Sort

Example:

```bash
sort
sort -rn
```

Used for ranking common errors.

---

## Uniq

Count repeated entries:

```bash
uniq -c
```

Used inside `log_analyzer.sh`.

---

## Tr

Convert case:

```bash
tr 'a-z' 'A-Z'
```

---

## Wc

Example:

```bash
wc -l sample_log.log
```

Actual output:

```text
16 sample_log.log
```

---

## Head & Tail

Examples:

```bash
head -5 file
tail -5 file
tail -f logfile
```

Useful for live log monitoring.

---

# 6. Real One-Liners I Actually Used

### Check Disk Usage

```bash
df -h
```

Used inside `system_info.sh`.

---

### Check Memory

```bash
free -h
```

---

### Find Large Directories

```bash
du -sh * | sort -hr | head -5
```

---

### Compress Old Logs

Used in `log_rotate.sh`.

```bash
find ~/myapp-logs -name "*.log" -mtime +7 -exec gzip {} \;
```

---

### Count Errors

Used in `log_analyzer.sh`.

```bash
grep -E "ERROR|Failed" sample_log.log | wc -l
```

Output:

```text
8
```

---

# 7. Error Handling & Debugging

## Exit Codes

Success:

```bash
exit 0
```

Failure:

```bash
exit 1
```

Check last command:

```bash
echo $?
```

---

## Strict Mode

I practiced:

```bash
set -euo pipefail
```

Actual output from `strict_demo.sh`.

```text
Testing strict mode...
Trying undefined variable...
MY_VAR: unbound variable
```

### What each flag does

| Flag | Purpose |
|------|---------|
| `set -e` | Stop on command failure |
| `set -u` | Fail on undefined variables |
| `pipefail` | Detect failures inside pipes |
| `set -x` | Debug execution |

---

## Trap

Example:

```bash
trap cleanup EXIT
```

Useful for cleanup before exiting.

---

# 8. Real Projects I Built

| Project | Purpose |
|---------|---------|
| `hello.sh` | First Bash script |
| `variables.sh` | Variables |
| `greet.sh` | User input |
| `check_number.sh` | If-else |
| `for_loop.sh` | For loops |
| `countdown.sh` | While loops |
| `functions.sh` | Functions |
| `system_info.sh` | System reporting |
| `backup.sh` | Backup automation |
| `log_rotate.sh` | Log rotation |
| `maintenance.sh` | Combined maintenance |
| `log_analyzer.sh` | Log analysis project |

---

# Commands I Personally Used

```bash
chmod +x script.sh
./script.sh

read -p

grep -E "ERROR|Failed"
grep -n "CRITICAL"

wc -l

sort | uniq -c

tar -czf

find -mtime

systemctl is-active nginx

df -h

free -h

tail -f logfile
```

---

# What I Learned

- Shebang ensures Bash executes scripts correctly.
- Variables, loops, and functions make scripts reusable.
- `grep`, `sort`, `uniq`, and `find` are essential for log analysis.
- `set -euo pipefail` creates safer production-ready scripts.
- Real automation projects helped me understand how DevOps engineers use Bash daily.

---

# DevOps Takeaway

This cheat sheet is built from the scripts and commands I actually executed on my Ubuntu EC2 instance during Days 16–20. Instead of memorizing syntax, I now have a practical reference covering backups, log rotation, monitoring, reporting, and log analysis—the exact Bash skills that form the foundation of DevOps automation.
