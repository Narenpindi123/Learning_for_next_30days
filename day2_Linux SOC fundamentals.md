# Day 2 – Linux SOC Fundamentals (Tasks 1–4)

## Objective
Day 2 focuses on Linux host-based monitoring, process management, authentication log analysis, and incident documentation. These tasks simulate real-world activities performed by SOC Analysts and Incident Responders.

---

## Environment
- OS: Linux Mint
- Shell: Bash
- Logs Analyzed: /var/log/auth.log, journalctl
- Tools Used: ps, top, kill, grep, journalctl, last

---

# Task 1 – View Running Processes

## Purpose
To identify active processes, resource usage, and potential suspicious activity. This is essential for detecting malware, cryptomining activity, or unauthorized services.

---

## Commands Used

```bash
ps aux
Explanation:
```
a – show processes for all users

u – display user-oriented output

x – include background processes without a terminal

---

```bash
top
```

Explanation:
- Displays real-time CPU and memory usage
- Used to identify abnormal resource consumption

---

## Security Relevance
- Unusual CPU or memory usage can indicate malicious activity
- Unknown or unexpected processes may signal persistence or compromise

---

# Task 2 – Kill and Monitor Processes
## Purpose
To identify, monitor, and terminate processes as part of containment or troubleshooting.

---

## Process Identification
```bash
ps aux | grep firefox
```
Observation:

- The PID appeared to change on each execution.
- This occurred because the grep firefox command matched itself.
Each execution spawns a new grep process, which exits immediately, resulting in a new PID every time.

---

## Correct Identification Methods
```bash
pgrep -a firefox
```
or

```bash
ps aux | grep firefox | grep -v grep
```
---

## Killing a Process
```bash
kill <PID>
```
Force termination (only if required):
```bash
kill -9 <PID>
```

---

## Why “No such process” Occurred
The PID belonged to the short-lived grep process, which had already exited by the time the kill command was issued.

---

## Security Relevance
- SOC analysts must distinguish between short-lived helper processes and persistent malicious processes
- Avoids false positives during investigations

---

# Task 3 – Detect Failed Login Attempts Using Logs
## Purpose
To simulate and detect suspicious authentication activity, such as brute-force login attempts.

---

Simulating Failed Logins
```bash
ssh fakeuser@localhost
```
An incorrect password was entered multiple times to generate failed authentication events.

---

## Log Analysis
Authentication Log Location
```bash
/var/log/auth.log
```
---

## Identify Failed Login Attempts
```bash
sudo grep "Failed password" /var/log/auth.log
```
Sample log entry:
```pgsql
Failed password for invalid user fakeuser from 127.0.0.1 port 54322 ssh2
```
Explanation:
- Indicates a failed SSH authentication attempt
- Shows attempted username, source IP, and timestamp

---

Count Failed Attempts
```bash
sudo grep "Failed password" /var/log/auth.log | wc -l
```
Repeated failures within a short time frame indicate possible brute-force behavior.

---

## Identify Source IP Addresses
```bash
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}'
```

---

## Check for Successful Logins
```bash
sudo grep "Accepted password" /var/log/auth.log
```
Result:
- No successful logins were observed following the failed attempts
- No account compromise detected

---

## Using journalctl
```bash
journalctl -u ssh --since "15 minutes ago"
```

---

## Security Relevance
- Repeated failed logins from the same IP suggest brute-force attempts
- Failed attempts followed by success may indicate compromised credentials

---

# Task 4 – Mini Incident Note
## Incident Title
Suspected Brute-Force Login Attempt on Linux Host

---

## Incident Summary
Multiple failed SSH authentication attempts were observed within a short time window. The pattern of activity matched common brute-force login behavior.

---

## Detection Method
The incident was detected through manual analysis of Linux authentication logs after simulating failed login attempts.

---

## Evidence Collected
## Evidence 1 – Failed Authentication Attempts
```bash
sudo grep "Failed password" /var/log/auth.log
```

Findings:
- Multiple failed attempts
- Invalid usernames
- Same source IP
- Close timestamps

---

## Evidence 2 – Login Correlation
```bash
sudo grep "Accepted password" /var/log/auth.log
```
Finding:
- No successful logins detected

---
## Evidence 3 – Process Review
```bash
ps aux
```
Finding:
- No suspicious or unauthorized processes running

---

Impact Assessment
Severity: Low

System Compromise: None

Data Loss: None

Persistence: Not observed

Root Cause
The activity was intentionally generated for lab validation. In a production environment, this behavior would indicate a brute-force attack attempt.

Recommended Actions
Enable account lockout policies

Deploy fail2ban to block repeated authentication failures

Monitor authentication logs continuously

Forward logs to a SIEM for centralized alerting

Incident Status
Closed – No compromise detected

Skills Demonstrated
Linux process monitoring

Authentication log analysis

Brute-force detection

Incident response documentation

SOC analyst workflow
