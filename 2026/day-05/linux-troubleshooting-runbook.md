# Day 05 – Linux Troubleshooting Runbook

## Target Service

**Service:** Nginx  
**System:** Ubuntu 26.04 LTS on AWS EC2  
**Hostname:** `ip-172-31-33-72`

---

## 1. Environment Basics

### 1.1 Check OS and Kernel

**Command:**

```bash
uname -a
```

**Output:**

```text
Linux ip-172-31-33-72 7.0.0-1006-aws #6-Ubuntu SMP PREEMPT Tue May 26 12:04:34 UTC 2026 x86_64 GNU/Linux
```

**Observation:**  
The server is running an Ubuntu AWS kernel on an x86_64 system.

### 1.2 Check Operating System

**Command:**

```bash
cat /etc/os-release
```

**Output:**

```text
PRETTY_NAME="Ubuntu 26.04 LTS"
NAME="Ubuntu"
VERSION_ID="26.04"
VERSION="26.04 LTS (Resolute Raccoon)"
UBUNTU_CODENAME=resolute
```

**Observation:**  
The server is running Ubuntu 26.04 LTS.

---

## 2. CPU and Memory Snapshot

### 2.1 Check Running Processes

**Command:**

```bash
top
```

**Observation:**  
The system was mostly idle and CPU usage was very low. Nginx was running normally.

### 2.2 Check Memory

**Command:**

```bash
free -h
```

**Output:**

```text
total        used        free      shared  buff/cache   available
Mem:           908Mi       314Mi       145Mi       2.7Mi       560Mi       593Mi
Swap:             0B          0B          0B
```

**Observation:**  
The server has about 908 MiB of RAM and about 593 MiB available memory. No swap is configured.

---

## 3. Disk and IO Snapshot

### 3.1 Check Disk Usage

**Command:**

```bash
df -h
```

**Output:**

```text
Filesystem       Size  Used Avail Use% Mounted on
/dev/root         13G  2.6G  9.9G  21% /
/dev/nvme0n1p13  989M   95M  828M  11% /boot
/dev/nvme0n1p15  105M  6.3M   99M   7% /boot/efi
```

**Observation:**  
The root filesystem is only 21% used, so there is plenty of available disk space.

### 3.2 Check Log Directory Size

**Command:**

```bash
du -sh /var/log
```

**Output:**

```text
18M     /var/log
```

**Observation:**  
The `/var/log` directory is about 18 MB. Some protected directories showed permission-denied messages, but the command still reported the total size.

---

## 4. Network Snapshot

### 4.1 Check Listening Ports

**Command:**

```bash
ss -tulpn
```

**Observation:**  
SSH is listening on port 22 and Nginx is listening on port 80.

Important ports observed:

```text
0.0.0.0:22
0.0.0.0:80
[::]:22
[::]:80
```

### 4.2 Test Nginx Locally

**Command:**

```bash
curl -I localhost
```

**Output:**

```text
HTTP/1.1 200 OK
Server: nginx/1.28.3 (Ubuntu)
Date: Sat, 08 Aug 2026 08:34:43 GMT
Content-Type: text/html
Content-Length: 3221
Connection: keep-alive
```

**Observation:**  
Nginx responded successfully with HTTP 200 OK.

---

## 5. Service Check

### Check Nginx Status

**Command:**

```bash
systemctl status nginx
```

**Observation:**

```text
Active: active (running)
Main PID: 678 (nginx)
Tasks: 3
Memory: 4.6M
CPU: 42ms
```

**Observation:**  
Nginx is enabled and currently running normally.

---

## 6. Logs Reviewed

### 6.1 Check Nginx Journal Logs

**Command:**

```bash
journalctl -u nginx -n 50 --no-pager
```

**Recent output:**

```text
Aug 08 06:49:03 ip-172-31-33-72 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
Aug 08 06:49:03 ip-172-31-33-72 systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
```

**Observation:**  
Nginx started successfully and no recent startup error was shown.

### 6.2 Check Nginx Error Log

**Command:**

```bash
tail -n 50 /var/log/nginx/error.log
```

**Observation:**  
This command can be used to inspect the latest Nginx error messages during troubleshooting.

---

## 7. Quick Findings

- Ubuntu 26.04 LTS is running normally.
- CPU usage is very low.
- About 593 MiB memory is available.
- No swap is configured.
- Root disk usage is only 21%.
- `/var/log` is about 18 MB.
- Nginx is active and running.
- Nginx is listening on port 80.
- `curl -I localhost` returned HTTP 200 OK.
- Nginx journal logs show a successful startup.
- No immediate resource or service problem was identified.

---

## 8. Mini Troubleshooting Flow

### Step 1 – Check Nginx Status

```bash
systemctl status nginx
```

If Nginx is stopped or failed, continue troubleshooting.

### Step 2 – Check Recent Logs

```bash
journalctl -u nginx -n 50 --no-pager
```

Look for startup errors, configuration problems, permission errors, or other failures.

### Step 3 – Test Nginx Configuration

```bash
sudo nginx -t
```

If the configuration test fails, fix the configuration before restarting Nginx.

### Step 4 – Test the Service Locally

```bash
curl -I localhost
```

A response such as `HTTP/1.1 200 OK` means Nginx is responding locally.

---

## 9. If This Worsens

If the problem continues, I would:

1. Check Nginx error logs and system logs for the exact failure.
2. Check CPU, memory, disk, and network usage again.
3. Test the Nginx configuration before restarting.
4. Restart Nginx only after collecting useful evidence.

If a restart is necessary:

```bash
sudo systemctl restart nginx
```

Then verify:

```bash
systemctl status nginx
curl -I localhost
```

---

## 10. What I Practiced

Today I practiced:

- `uname -a` – checking the kernel and system architecture.
- `cat /etc/os-release` – checking the Ubuntu version.
- `top` – checking running processes and CPU usage.
- `free -h` – checking memory.
- `df -h` – checking disk usage.
- `du -sh /var/log` – checking log directory size.
- `ss -tulpn` – checking listening network ports.
- `curl -I localhost` – testing the Nginx web service.
- `systemctl status nginx` – checking service status.
- `journalctl -u nginx` – checking service logs.
- `tail -n 50 /var/log/nginx/error.log` – checking the Nginx error log.

## Conclusion

The troubleshooting drill showed that the EC2 server and Nginx service were healthy during the checks. The server had available memory, low disk usage, low CPU usage, and Nginx returned HTTP 200 OK locally.
