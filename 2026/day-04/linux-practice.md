# Day 04 – Linux Practice: Processes and Services

## Process Checks

### 1. ps aux

Command:

    ps aux

What I learned:

This command shows the processes currently running on the Linux system. I used it to see nginx, systemd, ssh, and other processes.

### 2. pgrep nginx

Command:

    pgrep nginx

What I learned:

This command finds the Process IDs (PIDs) of nginx. I could see the nginx master and worker processes.

---

## Service Checks

### 3. systemctl status nginx

Command:

    systemctl status nginx

What I learned:

This command checks the status of the nginx service. My nginx service was active and running.

### 4. systemctl is-enabled nginx

Command:

    systemctl is-enabled nginx

What I learned:

This command checks whether nginx is configured to start automatically when the server boots. My result was enabled.

---

## Log Checks

### 5. journalctl -u nginx --no-pager -n 20

Command:

    journalctl -u nginx --no-pager -n 20

What I learned:

This command shows the latest 20 log messages for the nginx service.

### 6. journalctl -u nginx --since "1 hour ago" --no-pager

Command:

    journalctl -u nginx --since "1 hour ago" --no-pager

What I learned:

This command shows nginx logs from the last one hour.

---

## Mini Troubleshooting Flow

If a website is not working, I can follow these steps:

### Step 1 – Check the nginx service

    systemctl status nginx

Check whether nginx is active and running.

### Step 2 – Check nginx processes

    pgrep nginx

Check whether nginx processes are running.

### Step 3 – Check nginx logs

    journalctl -u nginx --no-pager -n 20

Check the latest nginx logs for possible problems.

### Step 4 – Test nginx locally

    curl localhost

My curl localhost command returned the website content, which showed that nginx was responding locally.

---

## What I Practiced

Today I practiced checking Linux processes, inspecting a systemd service, reading service logs, and performing a basic nginx troubleshooting flow on my AWS Ubuntu server.

I learned how ps, pgrep, systemctl, journalctl, and curl can be used together to investigate a service problem.
