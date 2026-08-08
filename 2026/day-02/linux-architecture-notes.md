# Day 02 – Linux Architecture, Processes, and systemd

## Linux Architecture

- **Kernel:** Core of Linux. It manages CPU, memory, processes, devices, filesystems, and networking.
- **User Space:** Where applications and commands run, such as Bash, Vim, Python, and Nginx.
- **systemd:** System and service manager used by modern Linux systems. It manages services and system startup.

```text
User Applications
       ↓
   User Space
       ↓
    systemd
       ↓
    Kernel
       ↓
   Hardware
```

## Linux Processes

- A **process** is a running instance of a program.
- Every process has a **PID (Process ID)**.
- Processes can create other processes, forming parent-child relationships.

### Process States

- **Running:** Process is running or ready to run.
- **Sleeping:** Process is waiting for an event or resource.
- **Stopped:** Process execution has been stopped.
- **Zombie:** Process has finished but its parent has not collected its exit status.

## systemd

- Manages system services and startup.
- Can start, stop, restart, and monitor services.
- Can enable services to start automatically during boot.

```bash
systemctl status nginx
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl enable nginx
```

## 5 Daily Linux Commands

1. `ps` – View running processes.
2. `top` – Monitor processes, CPU, and memory.
3. `systemctl` – Manage and check services.
4. `kill` – Send a signal to a process.
5. `free -h` – Check memory usage.

## DevOps Connection

Understanding processes, system resources, and systemd helps a DevOps engineer troubleshoot crashed services, CPU/memory problems, service failures, and application issues.
