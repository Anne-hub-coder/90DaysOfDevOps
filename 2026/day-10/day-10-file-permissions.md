# Day 10 – File Permissions & File Operations Challenge

## Objective

Today I practiced Linux file creation, file reading, and file permission management on my Ubuntu AWS EC2 instance.

I learned how to create files, read file contents, modify permissions using `chmod`, and understand how Linux controls access through read, write, and execute permissions.

---

## Task 1 – Create Files

### Commands

```bash
touch devops.txt

echo "Day 10 Linux File Permissions Practice" > notes.txt
echo "Learning chmod and file operations." >> notes.txt
echo "DevOps starts with Linux basics." >> notes.txt

echo 'echo "Hello DevOps"' > script.sh
```

### Verification

```bash
ls -l
```

### What I learned

- `touch` creates an empty file.
- `>` creates or overwrites a file.
- `>>` appends content.
- `echo` can quickly create simple files.

---

## Task 2 – Read Files

### Commands

```bash
cat notes.txt
cat script.sh
head -n 5 /etc/passwd
tail -n 5 /etc/passwd
```

### What I learned

- `cat` displays the complete file.
- `head` shows the beginning of a file.
- `tail` shows the end of a file.

---

## Task 3 – Check Current Permissions

### Command

```bash
ls -l devops.txt notes.txt script.sh
```

### Permission Format

| Symbol | Value |
|--------|-------|
| `r` | Read (4) |
| `w` | Write (2) |
| `x` | Execute (1) |

Permission layout:

```text
Owner | Group | Others
 rwx    rwx      rwx
```

### What I learned

- The first permission set belongs to the owner.
- The second belongs to the group.
- The third applies to everyone else.

---

## Task 4 – Modify Permissions

### Make `script.sh` executable

```bash
chmod +x script.sh
./script.sh
```

Output:

```text
Hello DevOps
```

### Make `devops.txt` read-only

```bash
chmod a-w devops.txt
```

### Set `notes.txt` to `640`

```bash
chmod 640 notes.txt
```

### Create `project` directory

```bash
mkdir project
chmod 755 project
```

### Verification

```bash
ls -l script.sh
ls -l devops.txt
ls -l notes.txt
ls -ld project
```

### Permission Changes

| File | Permission |
|------|------------|
| `script.sh` | Executable |
| `devops.txt` | Read-only |
| `notes.txt` | `640` |
| `project/` | `755` |

### What I learned

- `chmod +x` makes a file executable.
- `chmod a-w` removes write permission.
- Numeric permissions (`640`, `755`) provide precise access control.

---

## Task 5 – Test Permissions

### Commands

```bash
chmod -x script.sh
./script.sh

chmod +x script.sh

echo "Trying to write" >> devops.txt
```

### Observations

- Executing a file without execute permission resulted in **Permission denied**.
- Restoring execute permission allowed the script to run again.
- I observed how Linux permissions affect file access.

---

## Commands Used

```bash
touch devops.txt

echo "Day 10 Linux File Permissions Practice" > notes.txt
echo "Learning chmod and file operations." >> notes.txt
echo "DevOps starts with Linux basics." >> notes.txt

echo 'echo "Hello DevOps"' > script.sh

ls -l

cat notes.txt
cat script.sh

head -n 5 /etc/passwd
tail -n 5 /etc/passwd

chmod +x script.sh
./script.sh

chmod a-w devops.txt
chmod 640 notes.txt

mkdir project
chmod 755 project

ls -ld project

chmod -x script.sh
./script.sh
chmod +x script.sh
```

---

## What I Learned

- Created files using multiple Linux methods.
- Read files using `cat`, `head`, and `tail`.
- Understood Linux permission format (`rwx`).
- Modified permissions using both symbolic and numeric modes.
- Learned why execute permission is required for scripts.

---

## DevOps Takeaway

File permissions are one of the most important Linux security concepts in DevOps. They control who can read, modify, or execute files, helping teams securely manage scripts, configuration files, and shared project directories.

---

## Evidence

Screenshots collected during this exercise:

- `files-created.png`
- `read-files.png`
- `permissions-before.png`
- `permissions-after.png`
- `permission-test.png`

---

## Day 10 Summary

Today I practiced creating files, reading file contents, changing permissions with `chmod`, testing access restrictions, and understanding how Linux permissions help secure systems in real-world DevOps environments.
