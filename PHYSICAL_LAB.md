# 🛡️ Cybersecurity Home Lab - Physical Lab Penetration Testing

## Project Overview

**Lab Name:** Physical Lab Server Penetration Test  
**Target:** Windows Server 2025 (IP: 192.168.1.2)  
**Attacker Machine:** Kali Linux (IP: 192.168.1.10)  
**Date:** 2024-10-27  
**Tester:** Oleh Borysovskyy  
**Authorization:** Internal Lab Environment (No external access)  

---

## 1️⃣ Lab Setup (Physical Environment)

### 🔹 Network Configuration:

* **Router:** Netgear  
* **IP Addressing:** 192.168.1.0/24 subnet  
* **Devices:**
    * **Kali Linux (Attacker):** 192.168.1.10 (Physical machine)
    * **Windows Server 2025 (Target):** 192.168.1.2 (Physical machine)
    * **Windows 11 Pro (Remote Access):** (Physical machine)
* **Connectivity:** Wired (Cat 5 Ethernet), Wi-Fi available
    
    ![Image of Network Configuration](link_to_image)

### 🔹 Hardware:

* **Kali Linux Machine:** Dell laptop  
* **Windows Server Machine:** PC (i7, 16GB RAM)  
* **Windows 11 Pro:** (Remote access to Windows Server)
    
    ![Image of Hardware Setup](link_to_image)

### 🔹 Operating Systems:

* **Kali Linux:** Version 2024.2 (Latest)  
* **Windows Server 2025:** Build 25398 (Clean install, AD Installed, SSH Enabled)
    
    ![Image of Windows Server 2025 OS](link_to_image)
    
* **Windows 11 Pro Edition:** Version 24H2 (OS build 26100.3476)
    
    ![Image of Windows 11 Pro OS](link_to_image)

### 🔹 Security & Access Controls:

* **Firewall/Antivirus:** Windows Defender enabled (default settings)  
* **Physical Security:** Lab is located in a secured room with controlled access  

---

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
✅ Router is functional, and network is isolated as intended.

    ![Image of Nmap Scan Result](link_to_image)

---

## 3️⃣ Active Directory Configuration (Windows Server 2025)

### 🔹 AD DS Setup:
* **Domain Name:** lab.local  

**Installed Roles:**
* Active Directory Domain Services (AD DS)
* DNS Server
* File Server

    ![Image of AD DS Setup](link_to_image)

### 🔹 Security Policies & User Management:
* Created Organizational Units (OUs)
* Implemented Role-Based Access Control (RBAC)
* Configured Group Policies:
  * 🔒 Password Policies: Enforced complexity, expiration, and account lockout
  * 🔒 USB Restrictions: Disabled removable storage access for standard users
  * 🔒 RDP Access Control: Allowed only from Windows 11 Pro
  
    ![Image of Security Policies](link_to_image)

---

## 4️⃣ Remote Access Configuration
* **Windows 11 Pro → RDP to Windows Server:** Successful
* **Kali Linux → SSH to Windows Server:** Pending testing

    ![Image of Remote Access Session](link_to_image)

---

## 5️⃣ Penetration Testing Plan

| **Phase**          | **Tools & Techniques**                             |
|--------------------|----------------------------------------------------|
| **Reconnaissance** | Nmap, Netdiscover, DNS enumeration                 |
| **Scanning**       | Nmap, OpenVAS, Nikto (Web scanning)                |
| **Exploitation**   | Metasploit, Hydra (Password brute-force)           |
| **Privilege Escalation** | WinPEAS, SharpHound (BloodHound)             |
| **Post-Exploitation**    | Mimikatz, Windows Event Log analysis          |

---

## 6️⃣ Next Steps & Roadmap

* ✅ Install and configure Intrusion Detection System (IDS) (Snort/Suricata) on Linux machine
* ⏳ Deploy Security Information and Event Management (SIEM) (Wazuh/Splunk) on Ubuntu Server
* ⏳ Perform initial vulnerability scanning on Windows Server 2025 (Nmap/OpenVAS)
* ⏳ Test SSH access from Kali Linux (Confirm Windows Defender firewall rules)
* ⏳ Conduct password cracking simulations (Hashcat, Hydra)

---

## 📂 How to Use This Repository

* ✅ Follow along as I build and test my cybersecurity home lab.
* ✅ Check out my configurations and replicate them for your own learning.
* ✅ Contribute ideas or suggestions for security improvements.

---

## 🔗 Author & Contact

Oleh Borysovskyy | Cybersecurity Enthusiast

* 📌 **LinkedIn:** [Oleh Borysovskyy](https://www.linkedin.com/in/oleh-borysovskyy-a2a65152/)
* 📌 **GitHub:** [olehstudycyber](https://github.com/olehstudycyber)
* 📌 **Email:** [oborysovskyy@gmail.com](mailto:oborysovskyy@gmail.com)

---

## 🚀 Final Notes

* 🔹 If SSH from Kali works, update the README.
* 🔹 Add screenshots of vulnerabilities found during penetration testing.
* 🔹 After the SIEM/IDS setup, document real-time log monitoring results.
