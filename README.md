# 🛡️ Cybersecurity Home Lab & Incident Response Portfolio

## 📌 Portfolio Overview
Welcome to my security research and engineering portfolio. This repository documents a structured laboratory environment dedicated to practicing offensive penetration testing methodologies, analyzing application vulnerabilities under the hood, and documenting defensive enterprise incident response strategies. 

---

## 🗺️ Lab Environment & Topology
* **Attacker Infrastructure:** Kali Linux (VMware Workstation Player)
* **Target Environment:** Metasploitable 2 (Deliberately vulnerable Linux framework)
* **Internal Routing Architecture:** VMware NAT Virtual Network isolation layer (`VMnet8` internal virtual switch configuration)

---

## 🗂️ Lab Modules & Security Reports

Select a specific research module below to view full technical breakdowns, step-by-step terminal execution, and verified inline lab screenshots:

### 📡 Module 1: FTP Supply Chain Backdoor Validation
* **Target Vector:** `vsftpd 2.3.4` (CVE-2011-2523)
* **Concepts Practiced:** Host reconnaissance, automated bind shell exploitation execution hooks, framework parameter debugging (`LHOST` validation workarounds).
* **🔗 Project Documentation:** [View Complete Walkthrough (README.md)](vsftpd-walkthrough.md) *(Note: Keep this section intact below if preferred, or use a dedicated module file)*

### 📁 Module 2: Command Injection & Credential Harvesting via SMB
* **Target Vector:** Samba `usermap_script` (CVE-2007-2447)
* **Concepts Practiced:** SMB service version enumeration, **Reverse TCP Shell handling**, administrative privilege exploitation, and highly restricted Linux credential configuration harvesting (`/etc/shadow` extraction).
* **🔗 Project Documentation:** [👉 Click to View Samba Walkthrough](./samba-walkthrough.md)

### ⏳ Upcoming Module 3: Cloud Incident Response & Threat Hunting Report
* **Target Vector:** Administrative API Token Compromise / Corporate Data Exfiltration
* **Concepts:** Log file forensic analysis, Cloud Identity & Access Management (IAM) abuse tracking, Indicators of Compromise (IoC) mapping.
* **Status:** 🛠️ *Currently in development. Lab environment provisioning in progress.*

---
_Disclaimer: All documented exploits, configurations, and analytical walk-throughs contained within this repository are executed strictly within isolated academic virtualization environments for authorized educational analysis purposes only._
