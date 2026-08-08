# Day 07 – Linux File System Hierarchy & Scenario Practice

## Part 1: Linux File System Hierarchy

### `/` - Root Directory

The `/` directory is the starting point of the Linux file system.
All other directories are located under the root directory.

**I would use this when:** I need to understand the overall Linux file system structure.

### `/home` - User Home Directories

`/home` contains the home directories of normal users.
For example, a user may have files stored under `/home/ubuntu`.

**I would use this when:** I need to find a user's personal files.

### `/root` - Root User Home

`/root` is the home directory of the root user.

**I would use this when:** I need to understand where the root user's personal files are stored.

### `/etc` - Configuration Files

`/etc` contains configuration files used by the Linux system and services.

**I would use this when:** I need to check or troubleshoot system or service configuration.

### `/var/log` - Log Files

`/var/log` contains system and application log files.
Logs are very important when troubleshooting problems.

**I would use this when:** I need to investigate errors or service problems.

### `/tmp` - Temporary Files

`/tmp` is used to store temporary files.
These files are generally not intended for permanent storage.

**I would use this when:** I need temporary space while testing or troubleshooting.

### `/bin` - Essential Commands

`/bin` contains essential command binaries used by the system.

**I would use this when:** I need to understand where essential Linux commands are located.

### `/usr/bin` - User Commands

`/usr/bin` contains many standard commands and programs available to users.

**I would use this when:** I need to locate installed command-line programs.

### `/opt` - Optional Applications

`/opt` is commonly used for optional or third-party applications.

**I would use this when:** I need to understand where additional software may be installed.

---

## Part 2: Scenario Practice

### Scenario 1: Service Not Starting

**Problem:** A web application called `myapp` failed to start after a server reboot.

#### Step 1: Check the service status

```bash
systemctl status myapp
```

**Why:** This tells me whether the service is running, stopped, or failed.

#### Step 2: Check the service logs

```bash
journalctl -u myapp -n 50
```

**Why:** The logs can show the error that caused the service to fail.

#### Step 3: Check whether the service is enabled

```bash
systemctl is-enabled myapp
```

**Why:** This tells me whether the service is configured to start automatically after reboot.

#### Step 4: Check the service again

```bash
systemctl status myapp
```

**Why:** I want to verify whether the service is now running successfully.

**What I learned:** I should check the service status first, then inspect logs, and finally check whether it is enabled at boot.

---

### Scenario 2: High CPU Usage

**Problem:** The application server is slow and I need to find which process is using high CPU.

#### Step 1: Check live CPU usage

```bash
top
```

**Why:** `top` shows running processes and their CPU usage.

#### Step 2: Find processes using the most CPU

```bash
ps aux --sort=-%cpu | head -10
```

**Why:** This sorts processes by CPU usage so I can quickly identify the highest CPU consumers.

#### Step 3: Identify the PID

I would note the PID of the process using unusually high CPU.

**Why:** The PID allows me to investigate that specific process further.

**What I learned:** When troubleshooting high CPU, I should identify the process first instead of immediately restarting the server.

---

### Scenario 3: Finding Service Logs

**Problem:** A developer asks where the logs for the `docker` service are.

#### Step 1: Check the service

```bash
systemctl status docker
```

**Why:** This tells me whether the Docker service is running and may show recent log messages.

#### Step 2: View the latest logs

```bash
journalctl -u docker -n 50
```

**Why:** This displays the latest 50 log entries for the Docker service.

#### Step 3: Follow logs in real time

```bash
journalctl -u docker -f
```

**Why:** This allows me to watch new log entries as they are generated.

**What I learned:** Systemd-managed services can be investigated using `journalctl -u <service-name>`.

---

### Scenario 4: File Permissions Issue

**Problem:** A script called `backup.sh` gives a `Permission denied` error when I try to run it.

#### Step 1: Check the file permissions

```bash
ls -l /home/user/backup.sh
```

**Why:** I need to check whether the file has execute permission.

#### Step 2: Add execute permission

```bash
chmod +x /home/user/backup.sh
```

**Why:** `chmod +x` adds execute permission to the file.

#### Step 3: Verify the permission

```bash
ls -l /home/user/backup.sh
```

**Why:** I want to confirm that the execute permission has been added.

#### Step 4: Run the script

```bash
./backup.sh
```

**Why:** If the permissions are correct, the script should now be executable.

**What I learned:** Before changing permissions, I should first inspect the existing permissions with `ls -l`.

---

## What I Learned

Today I learned about the basic Linux file system hierarchy and where important files are stored.

I learned that:

- `/etc` is important for configuration files.
- `/var/log` is important for troubleshooting logs.
- `/home` contains normal users' home directories.
- `/tmp` is used for temporary files.
- `systemctl` can be used to inspect services.
- `journalctl` can be used to investigate service logs.
- `top` and `ps` can help identify high CPU processes.
- `ls -l` and `chmod` are useful for troubleshooting file permissions.

## DevOps Takeaway

When troubleshooting a Linux server, I should first understand where the relevant configuration files, logs, processes, and services are located.

I also learned that troubleshooting should be done step by step instead of making changes immediately.
