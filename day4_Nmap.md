# Day 4 – Network Scanning & Reconnaissance with Nmap and Shodan

## Overview
Day 4 focuses on understanding and practicing **network reconnaissance** using tools such as **Nmap** and **Shodan**. The objective of this lab is to learn how scanning and search-based reconnaissance work, what information they reveal, and how both attackers and defenders use this information in real-world scenarios.

All activities were performed **only on authorized systems** or through **publicly available data sources** for educational and ethical learning purposes.

---

## Task 1 – Network Scanning Fundamentals

### Active vs Passive Scanning
- **Active scanning** involves directly interacting with a target by sending packets and analyzing responses. It provides accurate results but is detectable.
- **Passive scanning** gathers information without direct interaction, often by observing traffic or using publicly available data sources.


### TCP SYN Scan vs TCP Full Connect Scan
- **TCP SYN scan** is a half-open scan that does not complete the TCP handshake. It is faster and less likely to be logged.
- **TCP full connect scan** completes the handshake and is more easily detected in system logs.


### Version Detection
- Identifies exact software and service versions running on open ports.
- This information is critical because vulnerabilities are often **version-specific**.

### OS Fingerprinting
- Attempts to identify the operating system based on TCP/IP behavior.
- Accuracy depends on open ports, responses, and network conditions.

### Ethical Scanning Considerations
- Scanning must always be authorized.
- Scope and intent must be clearly defined.
- Unauthorized scanning may be illegal and unethical.

---

## Task 2 – Practical Scanning

### Targets Scanned
- **Localhost**
- **Test Virtual Machine**

### Scans Performed
- Port scanning
- Service and version detection
- OS detection

### Example Commands
```bash
nmap localhost
sudo nmap -p- localhost
sudo nmap -sV localhost
sudo nmap -O localhost

sudo nmap -sS <test_vm_ip>
sudo nmap -sV <test_vm_ip>
sudo nmap -O <test_vm_ip>
```

---

# Task 3 – Reconnaissance Report
## Scan Types Used
- TCP SYN / TCP Connect scans for port discovery
- Service version detection for identifying running software
- OS fingerprinting for identifying the operating system

## Information Gained
- Open ports and exposed services
- Software and service versions
- Operating system details

Why Attackers Use Reconnaissance
To identify attack surfaces

To locate vulnerable or outdated services

To reduce guesswork and plan targeted attacks

Defensive Perspective
Helps identify unnecessary exposed services

Supports attack surface reduction

Enables early detection of reconnaissance activity

Task 4 – How Nmap Helps Attackers and Defenders
Nmap is a neutral tool whose impact depends on intent and authorization.

Attackers
Discover open ports and services

Identify vulnerable software versions

Tailor attacks based on OS information

Defenders
Identify exposed services on their own systems

Validate firewall and security configurations

Detect reconnaissance activity in early attack stages

Additional Learning – Shodan Reconnaissance
Use of Shodan
In addition to Nmap, Shodan was used as a passive reconnaissance tool to understand how exposed systems appear on the public internet.

Shodan provides visibility into:

Internet-facing services

Open ports and banners

Known vulnerabilities associated with exposed systems

Vulnerabilities Identified
Using Shodan, two publicly exposed vulnerabilities were identified:

One system located in Visakhapatnam (Vizag)

One system located in Buffalo

These vulnerabilities were identified through publicly available data and no exploitation was performed.

Responsible Disclosure
Both vulnerabilities were reported responsibly to the respective organizations.

No sensitive technical details were publicly disclosed.

The reports followed ethical and professional disclosure practices.

Responses from the affected organizations are currently pending.

This activity reinforced the importance of:

Ethical behavior

Responsible disclosure

Defensive security awareness

Key Learning Outcomes
Scanning and reconnaissance reveal significant system information

Service and version exposure increases risk

OS fingerprinting aids targeted attacks

Public exposure can be identified without active scanning

Ethical and responsible disclosure is a critical security skill

Conclusion
This lab demonstrated how both active and passive reconnaissance techniques are used in cybersecurity. Understanding how attackers gather information enables defenders to reduce exposure, harden systems, and respond appropriately to potential threats.

Ethical Notice
All scanning activities were conducted in a controlled lab environment or using publicly available information. No unauthorized scanning or exploitation was performed. All identified vulnerabilities were handled through responsible disclosure practices.
