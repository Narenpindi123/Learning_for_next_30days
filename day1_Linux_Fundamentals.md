# Linux Fundamentals Notes

These notes cover essential Linux filesystem concepts, permissions, and log analysis.
They are intended for beginners and cybersecurity-focused learning.

---

## Linux Filesystem Structure

### `/` (Root)
The root directory is the top-level directory in Linux.  
All files and directories exist under `/`.  
Improper changes here can prevent the system from booting.

---

### `/home`
Contains home directories for regular users.  
Each user has a personal directory (e.g., `/home/naren`) where files, downloads, and user-specific configurations are stored.

**Security relevance:**
- SSH keys (`~/.ssh`)
- Command history (`.bash_history`)
- Browser and application data  
Attackers often search `/home` after gaining access.

---

### `/etc`
Stores system-wide configuration files.

Examples:
- `/etc/passwd` – user account information
- `/etc/shadow` – encrypted passwords
- `/etc/sudoers` – sudo permissions
- `/etc/ssh/sshd_config` – SSH configuration

**Security relevance:**
Misconfigured files in `/etc` can allow unauthorized access, weak authentication, or privilege escalation.

---

### `/var`
Contains variable data that changes during system operation.

Common subdirectories:
- `/var/log` – system and authentication logs
- `/var/lib` – application state data

**Security relevance:**
Logs are critical for detecting attacks, auditing activity, and incident response.

---

### `/bin`
Contains essential system commands required for basic system functionality.

Examples:
- `ls`
- `cp`
- `cat`
- `bash`

**Security relevance:**
Tampering with binaries in `/bin` can indicate system compromise.

---

### `/usr`
Contains installed applications, libraries, and shared data.

Examples:
- `/usr/bin` – user commands
- `/usr/lib` – libraries
- `/usr/share` – documentation and resources

**Security relevance:**
Malicious changes here can affect multiple users and services.

---

## Linux Permissions Overview

Linux permissions define **who can access files and what actions they can perform**.

Each file or directory has permissions for:
- Owner
- Group
- Others

Permission types:
- `r` – read
- `w` – write
- `x` – execute

Example:
-rwxr-xr--

yaml
Copy code

---

## Why Linux Permissions Are Critical for Security

Linux permissions are a core security control mechanism.

### 1. Prevent Unauthorized Access
Permissions restrict sensitive files (such as password files and logs) to authorized users only.

Example:
- `/etc/shadow` is readable only by root to protect password hashes.

---

### 2. Enforce Least Privilege
Users and applications are granted **only the permissions they need**.

This limits:
- Accidental system damage
- Abuse of privileges
- Attack impact if an account is compromised

---

### 3. Protect System Integrity
Writable system files or scripts can be modified by attackers to execute malicious code.

Examples of risky configurations:
- World-writable files (`chmod 777`)
- Root-owned scripts writable by normal users

---

### 4. Reduce Privilege Escalation Risks
Many privilege escalation attacks rely on:
- Misconfigured permissions
- Writable executables or cron jobs
- Insecure ownership of files

Correct permissions significantly reduce these risks.

---

### 5. Secure Multi-User Environments
Linux is designed for multi-user systems.  
Permissions prevent users from accessing or modifying each other’s data.

This is essential in:
- Servers
- Enterprise systems
- Shared development environments

---

## Log Files (`/var/log`)

Log files record system activity and events.

Important logs:
- `auth.log` – login attempts and sudo usage
- `syslog` – system messages
- `kern.log` – kernel events

Logs are essential for:
- Monitoring system health
- Detecting attacks
- Investigating incidents

---

## Common Commands Used

```bash
ls -l          # view permissions and ownership
chmod 755 file # change permissions
chown user file # change ownership
cd /var/log    # navigate to logs
less auth.log  # view logs safely
```
---

## Summary
- Understanding the Linux filesystem, permissions, and logs is essential for:
- System administration
- Cybersecurity analysis
- Incident response
-Penetration testing
Linux permissions are a foundational security mechanism that protect systems from unauthorized access and misuse.
