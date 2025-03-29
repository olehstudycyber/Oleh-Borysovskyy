# Cybersecurity Home Lab - Physical Lab Penetration Testing

## Project Overview
**Lab Name:** Physical Lab Server Penetration Test  
**Target:** Windows Server 2025 (IP: 192.168.1.2)  
**Attacker Machine:** Kali Linux (IP: 192.168.1.10)  
**Date:** 2024-10-27  
**Tester:** Oleh Borysovskyy  
**Authorization:** Internal Lab Environment - No external access  

## 1️⃣ Lab Setup (Physical Environment)
**Network Configuration:**
* Router: Netgear
* IP Addressing: 192.168.1.0/24 subnet
* Kali Linux (Attacker): 192.168.1.10 (Physical machine)
* Windows Server 2025 (Target): 192.168.1.2 (Physical machine)
* Network Cabling: Wired (Cat 5 Ethernet), Wi-Fi available

**Hardware:**
* Kali Linux Machine: Dell laptop
* Windows Server Machine: Buypower (i7, 16GB RAM)
* Additional Machine: MacBook Air running Ubuntu Server

**Operating Systems:**
* Kali Linux: Version 2024.2 (Latest)
* Windows Server 2025: Build 25398 (Clean install, AD Installed, SSH Enabled)
* Ubuntu Server: Installed but pending IDS/SIEM setup

**Security & Access Controls:**
* Firewall/Antivirus: Windows Defender enabled (default settings)
* Physical Security: Lab is located in a secured room with controlled access

## 2️⃣ Network Discovery (Reconnaissance)
**Performed Nmap Scan:**
```sh
nmap -sn 192.168.1.0/24
```
**Scan Output:**
```
Nmap scan report for 192.168.1.1 (Router)
Host is up (0.00030s latency).

Nmap scan report for 192.168.1.2 (Windows Server 2025 - Target)
Host is up (0.00020s latency).

Nmap scan report for 192.168.1.10 (Kali Linux - Attacker)
Host is up (0.00040s latency).

Nmap done: 256 IP addresses (3 hosts up) scanned in 3.12 seconds.
```
**Findings:**
✅ Windows Server (192.168.1.2) and Kali Linux (192.168.1.10) confirmed online and reachable.  
✅ Router is functional and network is isolated as intended.

## 3️⃣ Active Directory Configuration (Windows Server 2025)
* Installed Active Directory Domain Services (AD DS)
* Domain Name: lab.local
* User & Group Management:
  * Created Organizational Units (OUs)
  * Implemented Role-Based Access Control (RBAC)
  * Configured Group Policy (Password policies, USB restrictions)

## 4️⃣ Remote Access
* From Windows 11 Pro: Successfully connected to Windows Server via RDP.
* From Kali Linux: SSH enabled but not yet tested for access.

## 5️⃣ Next Steps
* Install and configure Intrusion Detection System (IDS) (Snort/Suricata)
* Deploy Security Information and Event Management (SIEM) (Wazuh/Splunk)
* Begin penetration testing phase (scanning, enumeration, exploitation)
* Document vulnerabilities and remediation strategies

---

📌 How to Use This Repository
* Follow along as I build and test my cybersecurity home lab.
* Check out my configurations and replicate them for your own learning.
* Contribute ideas or suggestions for security improvements.

🔗 Author & Contact
Oleh Borysovskyy | Cybersecurity Enthusiast
