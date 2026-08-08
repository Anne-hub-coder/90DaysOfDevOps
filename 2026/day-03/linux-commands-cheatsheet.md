# Day 03 – Linux Commands Cheat Sheet

## 1. File System Commands

| Command | Usage |
|---|---|
| `pwd` | Shows the current working directory. |
| `ls` | Lists files and directories. |
| `ls -l` | Shows files with detailed information. |
| `ls -la` | Shows detailed information including hidden files. |
| `cd` | Changes the current directory. |
| `mkdir` | Creates a new directory. |
| `touch` | Creates an empty file. |
| `cp` | Copies files or directories. |
| `mv` | Moves or renames files and directories. |
| `rm` | Removes files or directories. |
| `cat` | Displays the contents of a file. |
| `find` | Searches for files and directories. |
| `du -h` | Shows disk usage of files and directories. |
| `df -h` | Shows available and used disk space. |

## 2. Process Management

| Command | Usage |
|---|---|
| `ps` | Displays running processes. |
| `ps aux` | Shows detailed information about running processes. |
| `top` | Monitors processes, CPU, and memory in real time. |
| `kill <PID>` | Sends a signal to a process using its PID. |
| `pgrep <name>` | Finds the PID of a process by name. |
| `jobs` | Shows jobs running in the current shell. |
| `free -h` | Shows memory usage in a human-readable format. |

## 3. Networking Troubleshooting

| Command | Usage |
|---|---|
| `ping google.com` | Tests network connectivity to a host. |
| `ip addr` | Displays network interfaces and IP addresses. |
| `dig google.com` | Queries DNS information for a domain. |
| `curl https://example.com` | Sends a request to a URL and displays the response. |
| `hostname` | Displays the system hostname. |

## 4. Useful System Commands

| Command | Usage |
|---|---|
| `whoami` | Shows the current logged-in user. |
| `date` | Displays the current date and time. |
| `uptime` | Shows how long the system has been running and system load. |
| `man <command>` | Opens the manual page for a command. |
| `history` | Shows previously executed commands. |

## Quick Troubleshooting Flow

### Check where I am

```bash
pwd
