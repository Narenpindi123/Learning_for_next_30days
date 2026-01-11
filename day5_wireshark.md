# Wireshark Traffic Analysis – Linux

This lab focuses on understanding network traffic using Wireshark by analyzing packets, applying filters, and examining DNS and HTTP communications. The goal is to gain hands-on experience with live traffic capture and protocol-level analysis from a security perspective.

---

## Task 1: Wireshark Fundamentals

### Packets vs Frames
- A **frame** is a Layer 2 (Data Link) unit that includes MAC addresses and encapsulates packets.
- A **packet** is a Layer 3 (Network) unit containing IP addressing and routing information.
- In Wireshark, frames provide capture metadata, while packets reveal network-layer details.

**Security relevance:**  
Frames help identify local devices, while packets are used to trace communication across networks and detect malicious traffic patterns.

---

### Capture Filters vs Display Filters

**Capture Filters**
- Applied before traffic is captured
- Use Berkeley Packet Filter (BPF) syntax
- Reduce noise and storage usage

Examples:
tcp port 80
udp port 53

**Display Filters**
- Applied after capture
- Wireshark-specific syntax
- Used for detailed analysis

Examples:
dns
http
tcp.port == 443


**Security relevance:**  
Capture filters are useful during live incidents, while display filters are essential for forensic and threat-hunting analysis.

---

### TCP Three-Way Handshake
- **SYN**: Client initiates connection
- **SYN-ACK**: Server acknowledges
- **ACK**: Connection established

**Security relevance:**  
Abnormal handshakes may indicate scanning, denial-of-service attempts, or malicious automation.

---

### DNS in PCAPs
- DNS commonly uses UDP port 53
- Resolves domain names to IP addresses

**Security relevance:**  
DNS traffic is often the first indicator of compromise and is frequently used by malware for command-and-control communication.

---

## Task 2: Capturing Live Network Traffic

### Live Capture
- Wireshark was installed with non-root capture permissions
- The active network interface (Wi-Fi/Ethernet) was selected
- Normal browsing activity was generated to produce traffic

---

### Display Filters Used

**DNS**
dns

**HTTP**
http

**HTTPS / TLS**
tls

---

### Identifying IPs and Protocols
- Source and destination IP addresses were identified from the IP header
- Protocol stacks observed:
  - Ethernet → IP → TCP/UDP → DNS / HTTP / TLS

**Security relevance:**  
Identifying protocols and IPs helps determine communication behavior, external connections, and potential threats.

---

## Task 3: Protocol Analysis

### DNS Query Analysis
A DNS query packet was analyzed to observe:
- Source IP (client)
- Destination IP (DNS server)
- UDP port 53
- Queried domain name

**Security perspective:**  
DNS analysis helps detect suspicious domains, beaconing activity, and early-stage malware communication.

---

### HTTP Request Analysis
An HTTP GET request was analyzed by visiting a non-HTTPS website.

Observed details:
- TCP destination port 80
- HTTP GET method
- Host and User-Agent headers

**Security perspective:**  
HTTP traffic is unencrypted, making it susceptible to interception and data leakage, and is often targeted in attacks.

---

## Conclusion

This lab demonstrated how Wireshark can be used to capture and analyze live network traffic. By examining DNS and HTTP communications, it is possible to identify IP addresses, protocols, and communication patterns that are critical for security monitoring and incident response. These skills are foundational for SOC operations and network forensics.

---
