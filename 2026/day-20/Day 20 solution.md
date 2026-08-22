# Day 20 – Bash Scripting Challenge: Log Analyzer and Report Generator

## Objective

Today I built a real-world Bash project that automatically analyzes log files, counts errors, identifies critical events, generates a summary report, and archives processed logs.

I practiced:

- Validating command-line arguments
- Searching logs using `grep`
- Counting errors automatically
- Finding critical events with line numbers
- Generating timestamped reports
- Archiving processed logs

---

## Environment

- Platform: AWS EC2
- Operating System: Ubuntu 26.04 LTS
- Shell: Bash

---

## Task 1 – Create a Sample Log File

I created `sample_log.log` containing system events such as `INFO`, `ERROR`, `Failed`, and `CRITICAL` entries for testing the script.

### Commands

```bash
cd ~

nano sample_log.log
wc -l sample_log.log
```

### Output

```text
16 sample_log.log
```

### What I Learned

- A sample dataset helps test automation safely.
- `wc -l` quickly verifies file size.
- Mixed log entries simulate real production logs.

---

## Task 2 – Build the Log Analyzer Script

I created `log_analyzer.sh` to automate log analysis.

The script performs:

- Input validation
- File existence verification
- Error counting
- Critical event detection
- Top error analysis
- Report generation
- Log archiving

### Commands

```bash
nano log_analyzer.sh
chmod +x log_analyzer.sh

./log_analyzer.sh sample_log.log
```

### Output

```text
Total Error Count: 8
Generating report...
Report generated: log_report_2026-08-22.txt
Log archived successfully.
```

### What I Learned

- Input validation prevents invalid executions.
- `grep` makes log filtering simple.
- Bash can automate repetitive monitoring tasks.

---

## Task 3 – Generated Summary Report

The script automatically created a timestamped report.

### Command

```bash
cat log_report_$(date +%Y-%m-%d).txt
```

### Output

```text
===== Daily Log Analysis Report =====
Date: Sat Aug 22 13:22:23 UTC 2026
Log File: sample_log.log
Total Lines: 16
Total Errors: 8

===== Top 5 Error Messages =====
      3 Connection timed out
      1 Permission denied
      1 File not found
      1 Disk I/O error

===== Critical Events =====
5:2026-08-22 09:04:22 CRITICAL Disk space below threshold
9:2026-08-22 09:08:40 CRITICAL Database connection lost
```

### Report Contents

The report includes:

- Date of analysis
- Log filename
- Total lines processed
- Total error count
- Most common error messages
- Critical events with line numbers

### What I Learned

- Automated reporting saves manual effort.
- `grep -n` adds useful line numbers.
- `sort` and `uniq -c` help identify recurring problems.

---

## Task 4 – Archive Processed Logs

After analysis, the script copied the processed log into an archive directory.

### Command

```bash
ls -l archive
```

### Output

```text
total 4
-rw-rw-r-- 1 ubuntu ubuntu 716 Aug 22 13:22 sample_log.log
```

### What I Learned

- Archiving keeps processed logs organized.
- Historical logs remain available for troubleshooting.
- Automation reduces manual file management.

---

## Script Verification

I verified that the analyzer script was executable.

### Command

```bash
ls -l log_analyzer.sh
```

### Output

```text
-rwxrwxr-x 1 ubuntu ubuntu 890 Aug 22 13:22 log_analyzer.sh
```

---

## Verification

I confirmed that all Bash scripts created during my learning journey remain available.

### Command

```bash
ls -l *.sh
```

### Output

```text
-rwxrwxr-x args_demo.sh
-rwxrwxr-x backup.sh
-rwxrwxr-x count.sh
-rwxrwxr-x countdown.sh
-rwxrwxr-x disk_check.sh
-rwxrwxr-x for_loop.sh
-rwxrwxr-x functions.sh
-rwxrwxr-x greet.sh
-rwxrwxr-x local_demo.sh
-rwxrwxr-x log_analyzer.sh
-rwxrwxr-x log_rotate.sh
-rwxrwxr-x maintenance.sh
-rwxrwxr-x strict_demo.sh
-rwxrwxr-x system_info.sh
...
```

The output confirmed that all scripts were successfully created and remained executable.

---

## Commands Used

```bash
cd ~

nano sample_log.log
wc -l sample_log.log

nano log_analyzer.sh
chmod +x log_analyzer.sh
./log_analyzer.sh sample_log.log

cat log_report_$(date +%Y-%m-%d).txt

ls -l archive

ls -l log_analyzer.sh

ls -l *.sh
```

---

## Tools & Commands Used

| Tool | Purpose |
|------|---------|
| `grep` | Search log entries |
| `grep -n` | Show line numbers |
| `wc -l` | Count total lines |
| `sort` | Sort matching entries |
| `uniq -c` | Count repeated errors |
| `head` | Display top results |
| `date` | Generate timestamped filenames |
| `cp` | Archive processed logs |

---

## What I Learned

- Bash can automate log analysis efficiently.
- `grep`, `sort`, and `uniq` are powerful log-processing tools.
- Timestamped reports make daily monitoring easier.
- Input validation improves script reliability.
- Archiving processed logs keeps systems organized.

---

## DevOps Takeaway

Log analysis is one of the most common operational tasks in DevOps. Instead of manually searching through thousands of log lines, Bash scripts can automatically identify recurring errors, highlight critical incidents, generate daily reports, and archive processed logs—making troubleshooting faster and more reliable.

---

## Evidence

Capture these screenshots for your GitHub repository:

- `sample-log-created.png`
- `log-analyzer-output.png`
- `log-report.png`
- `archive-folder.png`
- `log-analyzer-script.png`
- `scripts-list.png`

---

## Day 20 Summary

Today I completed my first complete log analysis automation project. The script validates input, counts errors, identifies critical events, generates a timestamped summary report, and archives processed logs. This project combines multiple Bash skills into a practical DevOps workflow used for monitoring and troubleshooting production systems.
