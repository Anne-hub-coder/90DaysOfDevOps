# Day 12 – Revision (Days 01–11)

## Goal

Today I took a revision day to reinforce the Linux fundamentals I practiced during Days 01–11 instead of learning a new topic.

---

## Process & Service Checks

### Commands

```bash
ps aux | head -10
```

```bash
top
```

```bash
systemctl status nginx
```

```bash
journalctl -u nginx -n 10 --no-pager
```

### What I observed

- Running processes were displayed successfully.
- `top` showed live CPU and memory usage.
- Nginx was active and running.
- Recent logs confirmed the service was operating normally.

---

## File Skills Practice

### Commands

```bash
touch revision.txt
```

```bash
echo "Day 12 Revision" > revision.txt
```

```bash
echo "Practicing Linux fundamentals." >> revision.txt
```

```bash
cat revision.txt
```

```bash
ls -l revision.txt
```

```bash
chmod 644 revision.txt
```

```bash
ls -l revision.txt
```

### What I observed

- Created a new file successfully.
- Used `>` to overwrite content.
- Used `>>` to append new content.
- Changed file permissions using `chmod 644`.

---

## User & Ownership Practice

### Commands

```bash
touch ownership-review.txt
```

```bash
sudo chown tokyo ownership-review.txt
```

```bash
ls -l ownership-review.txt
```

```bash
id tokyo
```

### What I observed

- Successfully changed file ownership.
- Verified the owner using `ls -l`.
- Confirmed the user's details using `id`.

---

## My Top 5 Incident Commands

| Command | Why I'd Use It |
|---------|----------------|
| `systemctl status nginx` | Check service health |
| `journalctl -u nginx` | Read service logs |
| `ps aux` | View running processes |
| `ls -l` | Check permissions and ownership |
| `chmod` | Fix permission issues |

---

## Mini Self-Check

### 1. Which 3 commands save me the most time?

- `systemctl status nginx` — quickly checks if a service is healthy.
- `journalctl -u nginx` — helps troubleshoot using logs.
- `ls -l` — instantly shows permissions and ownership.

### 2. How do I check if a service is healthy?

I would run:

```bash
systemctl status nginx
```

```bash
journalctl -u nginx -n 10 --no-pager
```

```bash
ss -tulpn | grep :80
```

### 3. How do I safely change ownership and permissions?

Example:

```bash
sudo chown tokyo ownership-review.txt
```

```bash
chmod 644 ownership-review.txt
```

This changes the file owner safely and sets read/write permissions for the owner while giving read-only access to others.

### 4. What will I improve in the next 3 days?

- Practice Docker commands.
- Improve Linux troubleshooting speed.
- Become more confident with file permissions and ownership.

---

## Commands Used

```bash
ps aux | head -10
top
systemctl status nginx
journalctl -u nginx -n 10 --no-pager
touch revision.txt
echo "Day 12 Revision" > revision.txt
echo "Practicing Linux fundamentals." >> revision.txt
cat revision.txt
ls -l revision.txt
chmod 644 revision.txt
touch ownership-review.txt
sudo chown tokyo ownership-review.txt
ls -l ownership-review.txt
id tokyo
```

---

## What I Learned

- Process checks become faster with `ps` and `top`.
- Service troubleshooting starts with `systemctl` and `journalctl`.
- File permissions and ownership are easier to understand after practicing repeatedly.
- Small daily revision helps build long-term Linux confidence.

---

## DevOps Takeaway

This revision day helped reinforce the core Linux skills that every DevOps engineer uses daily—checking services, reading logs, managing files, and troubleshooting systems.

---

## Evidence

Screenshots collected during this exercise:

- `process-check.png` *(optional)*
- `service-check.png` *(optional)*
- `file-revision.png` *(optional)*

---

## Day 12 Summary

Today I reviewed everything from Days 01–11 by practicing process checks, service monitoring, file operations, permissions, and ownership. Revisiting these fundamentals improved my confidence in using Linux for real DevOps tasks.
