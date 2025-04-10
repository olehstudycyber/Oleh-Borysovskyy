# Cybersecurity Home Lab – Oleh Borysovskyy

Welcome to my cybersecurity home lab! This repository documents my hands-on experience with penetration testing, system hardening, and monitoring in a physical, isolated lab environment.

## 🧠 Objective

To simulate real-world cybersecurity scenarios using a physical lab environment with Windows Server 2025, Kali Linux, Active Directory, and security tools like Wazuh SIEM and Sysmon.

---

## 🖥️ Lab Environment Overview

| Component          | Details                                      |
|--------------------|----------------------------------------------|
| **Attacker**       | Kali Linux 2024.2 (Dell laptop)              |
| **Target**         | Windows Server 2025 (Build 25398, Buypower)  |
| **Client**         | Windows 11 Pro (Remote access to server)     |
| **Network**        | Isolated via Netgear Router (192.168.1.0/24) |
| **SIEM/IDS**       | Wazuh (coming soon)                          |
| **Tools**          | Nmap, Metasploit, Hydra, Sysmon, Windows Defender |

---

## 📁 Repository Structure

├── recon_logs/ # Nmap, Netdiscover, Enum4linux, etc. ├── exploitation/ # Exploit attempts, payloads, and PoCs ├── post_exploitation/ # Privilege escalation, persistence ├── SIEM_IDS/ # Wazuh config/logs (in progress) ├── hardening/ # Sysmon rules, audit policy, hardening notes ├── reports/ # Penetration testing reports └── SECURITYPLUS_LAB_TRACKER.md # Project progress tracker

yaml
Copy
Edit

---

## 🔧 Setup Highlights

- **Windows Server 2025**: Active Directory enabled, Sysmon installed, Defender running
- **Kali Linux**: Primary offensive machine
- **Network**: Fully isolated lab, wired Ethernet (Cat 5)
- **Security**: Lab is physically secured; no internet access

---

## 🚧 In Progress

- Wazuh SIEM deployment & log forwarding
- Integration of IDS alerts with exploitation attempts
- Documentation of full red team to blue team workflows

---

## 📄 License & Contributions

This repository is for educational and personal development purposes only. Contributions are welcome v

## 📫 Let's Connect  

🔹 **LinkedIn**: [(https://www.linkedin.com/in/oleh-borysovskyy-a2a65152/)](#)  
🔹 **GitHub**: [olehstudycyber](https://github.com/olehstudycyber)  
🔹 **Email**: [oborysovskyy@gmail.com]  

---

🚀 *Constantly learning & building in cybersecurity!*  
