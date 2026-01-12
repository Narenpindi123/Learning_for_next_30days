# Day 6 – Brute Force Detection & Security Event Analysis

## Objective
The objective of Day 6 is to simulate common attack behavior, observe the resulting system and network activity, identify indicators of compromise (IOCs), and produce a professional security event write-up similar to real SOC and incident response workflows.

---

## Task 1 – Attack Overview

### Brute Force Overview
A brute force attack is an authentication-based attack where an adversary repeatedly attempts different credential combinations to gain unauthorized access. These attacks typically target exposed services such as SSH, RDP, FTP, or web login portals and rely on weak passwords, lack of rate limiting, or missing MFA.

### Recon → Exploit → Post-Exploit Chain
- **Reconnaissance:** Identifying services, ports, and potential entry points
- **Exploitation:** Attempting authentication or exploiting vulnerabilities
- **Post-Exploitation:** Maintaining access, escalating privileges, or moving laterally

### Indicators of Compromise (IOCs)
- Multiple failed login attempts
- Repeated connections from a single IP
- Abnormal authentication timing
- Short-lived SSH sessions

---

## Task 2 – Generate and Capture Suspicious Activity

### Activity Generated
- Repeated failed SSH login attempts using invalid credentials
- SSH traffic captured during authentication failures

### Monitoring Methods
- System authentication logs (`/var/log/auth.log`)
- Network traffic capture using Wireshark or tcpdump

### Expected Observations
- Authentication failure log entries
- Multiple TCP connection attempts to port 22
- Repeated SSH sessions terminating after failed authentication

---

## Task 3 – Identification and Analysis

### Suspicious IP Identification
Authentication logs revealed multiple failed login attempts originating from a single source IP within a short time window. Network traffic analysis confirmed repeated SSH connection attempts from the same source.

### Pattern Identification
The observed behavior aligns with a brute force authentication attempt characterized by:
- Repeated login failures
- High connection frequency
- Targeting of SSH service
- No successful authentication

**MITRE ATT&CK Technique:**  
- T1110 – Brute Force

---

## Task 4 – Final Security Event Write-Up

### Incident Summary
A suspected brute force authentication attempt was detected against an SSH service on a Linux system. Multiple failed login attempts were observed and confirmed through log and network traffic analysis. No successful compromise occurred.

### Indicators of Compromise (IOCs)
- Repeated `Failed password` entries in authentication logs
- Multiple SSH connections to TCP port 22
- Short-lived SSH sessions following authentication failures

### Impact Assessment
- No unauthorized access gained
- No privilege escalation or persistence detected
- Overall impact classified as low

### Recommendations
- Enable SSH rate limiting or fail2ban
- Disable password-based SSH authentication
- Enforce key-based authentication
- Implement MFA where possible
- Monitor authentication logs continuously

---

## Conclusion
This lab demonstrates how common brute force attacks are detected and analyzed in real-world environments. By correlating system logs with network traffic, suspicious behavior can be identified early, reducing the risk of successful compromise. The exercise mirrors standard SOC analyst responsibilities and reinforces the importance of proactive monitoring and defensive controls.
