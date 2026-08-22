# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Objective

Today I combined everything from Days 16–18 into real-world Bash automation projects by creating scripts for log rotation, server backups, scheduled maintenance, and understanding how cron jobs automate recurring tasks.

I practiced:

- Rotating old log files automatically
- Creating timestamped server backups
- Understanding cron scheduling syntax
- Building a maintenance script that combines multiple automation tasks
- Logging script execution with timestamps

---

## Environment

- Platform: AWS EC2
- Operating System: Ubuntu 26.04 LTS
- Shell: Bash

---

## Task 1 – Log Rotation Script

I created `log_rotate.sh` to automate log maintenance.

The script:

- Accepts a log directory as an argument.
- Compresses `.log` files older than 7 days.
- Deletes compressed logs older than 30 days.
- Validates that the directory exists before running.

### Commands

```bash
mkdir -p ~/myapp-logs

touch ~/myapp-logs/app1.log
touch ~/myapp-logs/app2.log
touch ~/myapp-logs/app3.log

touch -d "10 days ago" ~/myapp-logs/app1.log
touch -d "8 days ago" ~/myapp-logs/app2.log
touch -d "2 days ago" ~/myapp-logs/app3.log

nano log_rotate.sh
chmod +x log_rotate.sh
./log_rotate.sh ~/myapp-logs
```

### Output

```text
Log rotation completed.
Compressed old log files.
Deleted old compressed logs.
```

### Verification

```bash
ls -l ~/myapp-logs
```

Output:

```text
total 8
-rw-rw-r-- 1 ubuntu ubuntu 29 Aug 12 13:03 app1.log.gz
-rw-rw-r-- 1 ubuntu ubuntu 29 Aug 14 13:03 app2.log.gz
-rw-rw-r-- 1 ubuntu ubuntu  0 Aug 20 13:03 app3.log
```

### What I Learned

- `find` can locate files based on age.
- `gzip` compresses old log files automatically.
- Automation helps manage log storage efficiently.

---

## Task 2 – Server Backup Script

I created `backup.sh` to generate timestamped compressed backups.

The script:

- Accepts source and destination directories.
- Creates a `.tar.gz` archive.
- Verifies successful archive creation.
- Removes backups older than 14 days.

### Commands

```bash
mkdir -p ~/backups

nano backup.sh
chmod +x backup.sh

./backup.sh ~/myapp-logs ~/backups
```

### Output

```text
tar: Removing leading '/' from member names
Backup created successfully.
-rw-rw-r-- 1 ubuntu ubuntu 243 Aug 22 13:09 /home/ubuntu/backups/backup-2026-08-22-13-09-46.tar.gz
```

### Verification

```bash
ls -lh ~/backups
```

Output

```text
total 4.0K
-rw-rw-r-- 1 ubuntu ubuntu 243 Aug 22 13:09 backup-2026-08-22-13-09-46.tar.gz
```

### What I Learned

- `tar -czf` creates compressed backup archives.
- Timestamped filenames prevent overwriting previous backups.
- Verifying backups ensures successful automation.

---

## Task 3 – Understanding Crontab

I checked whether any scheduled cron jobs already existed.

### Command

```bash
crontab -l
```

### Output

```text
no crontab for ubuntu
```

No cron jobs were configured, which is expected on a fresh EC2 instance.

### Cron Syntax

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0–7)
│ │ │ └──── Month (1–12)
│ │ └────── Day of month (1–31)
│ └──────── Hour (0–23)
└────────── Minute (0–59)
```

### Cron Entries for Documentation

**Run log rotation every day at 2 AM**

```cron
0 2 * * * /home/ubuntu/log_rotate.sh /home/ubuntu/myapp-logs
```

**Run backup every Sunday at 3 AM**

```cron
0 3 * * 0 /home/ubuntu/backup.sh /home/ubuntu/myapp-logs /home/ubuntu/backups
```

**Run health check every 5 minutes**

```cron
*/5 * * * * /home/ubuntu/health_check.sh
```

> **Note:** These entries were documented but not applied using `crontab -e`.

### What I Learned

- Cron automates recurring tasks.
- Scheduling backups reduces manual effort.
- Keeping cron entries documented helps during deployment planning.

---

## Task 4 – Scheduled Maintenance Script

I created `maintenance.sh` to combine multiple automation tasks into one workflow.

The script:

- Runs log rotation.
- Runs the backup script.
- Stores all output in a timestamped maintenance log.

### Commands

```bash
nano maintenance.sh
chmod +x maintenance.sh
./maintenance.sh
```

### Maintenance Log

```bash
cat ~/maintenance.log
```

Output

```text
===== Sat Aug 22 13:11:46 UTC 2026 =====
Running log rotation...
Log rotation completed.
Compressed old log files.
Deleted old compressed logs.
Running backup...
tar: Removing leading '/' from member names
Backup created successfully.
-rw-rw-r-- 1 ubuntu ubuntu 243 Aug 22 13:11 /home/ubuntu/backups/backup-2026-08-22-13-11-47.tar.gz
Maintenance completed.
```

### Daily Cron Entry

```cron
0 1 * * * /home/ubuntu/maintenance.sh
```

### What I Learned

- Multiple automation tasks can be combined into one script.
- Logging script execution makes troubleshooting easier.
- Timestamped logs provide an execution history.

---

## Scripts Created

| Script | Purpose |
|---------|---------|
| `log_rotate.sh` | Compress and clean old log files |
| `backup.sh` | Create timestamped backups |
| `maintenance.sh` | Run log rotation and backups together |

---

## Verification

I verified that all newly created scripts had executable permissions.

### Command

```bash
ls -l *.sh
```

### Output

```text
-rwxrwxr-x backup.sh
-rwxrwxr-x log_rotate.sh
-rwxrwxr-x maintenance.sh
-rwxrwxr-x system_info.sh
-rwxrwxr-x functions.sh
-rwxrwxr-x strict_demo.sh
-rwxrwxr-x local_demo.sh
-rwxrwxr-x greet.sh
-rwxrwxr-x countdown.sh
-rwxrwxr-x count.sh
-rwxrwxr-x for_loop.sh
...
```

The output confirmed that all scripts were successfully created and were executable.

---

## Commands Used

```bash
cd ~

mkdir -p ~/myapp-logs
touch ~/myapp-logs/app1.log
touch ~/myapp-logs/app2.log
touch ~/myapp-logs/app3.log

touch -d "10 days ago" ~/myapp-logs/app1.log
touch -d "8 days ago" ~/myapp-logs/app2.log
touch -d "2 days ago" ~/myapp-logs/app3.log

nano log_rotate.sh
chmod +x log_rotate.sh
./log_rotate.sh ~/myapp-logs

ls -l ~/myapp-logs

mkdir -p ~/backups

nano backup.sh
chmod +x backup.sh
./backup.sh ~/myapp-logs ~/backups

ls -lh ~/backups

crontab -l

nano maintenance.sh
chmod +x maintenance.sh
./maintenance.sh

cat ~/maintenance.log

ls -l *.sh
```

---

## What I Learned

- `find`, `gzip`, and `tar` are powerful Linux tools for automation.
- Timestamped backups prevent accidental overwrites.
- Cron scheduling helps automate recurring maintenance tasks.
- Logging script output improves monitoring and troubleshooting.
- Combining multiple scripts creates more practical DevOps workflows.

---

## DevOps Takeaway

Real-world DevOps teams automate routine maintenance tasks like log cleanup, backups, and health checks instead of running them manually.

Today's project demonstrated how Bash scripting and cron scheduling work together to create reliable server maintenance workflows that save time and reduce operational risk.

---

## Evidence

Capture these screenshots for your GitHub repository:

- `log-rotation.png`
- `backup-created.png`
- `crontab-check.png`
- `maintenance-log.png`
- `scripts-list.png`

---

## Day 19 Summary

Today I built three practical automation scripts that perform log rotation, server backups, and scheduled maintenance. I also learned how cron scheduling works and how combining multiple Bash scripts creates reusable maintenance workflows used in real DevOps environments.
