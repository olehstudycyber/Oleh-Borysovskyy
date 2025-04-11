# 🛡️ Cybersecurity Home Lab – Oleh Borysovskyy

Welcome to my cybersecurity home lab! This repository documents my hands-on experience with penetration testing, system hardening, and monitoring in a **physical, isolated lab environment**.

---

## 🎯 Objective

To simulate real-world cybersecurity scenarios using a physical lab setup featuring **Windows Server 2025**, **Kali Linux**, **Active Directory**, and security tools like **Wazuh SIEM** and **Sysmon**.

---

## 🧪 Lab Overview

- **Attacker**: Kali Linux (192.168.1.10)
- **Target**: Windows Server 2025 (192.168.1.2)
- **Network**: Isolated LAN (192.168.1.0/24)
- **Tools Used**: Nmap, Metasploit, Wazuh, Sysmon, Windows Defender, Hydra, Enum4linux
- ## 🖼️ Lab Network Diagram

![Lab Network Diagram](./reports/lab_network_diagram.png)

---

## 📁 Repository Structure

```plaintext
├── recon_logs/           # Nmap, Netdiscover, Enum4linux, etc.
├── exploitation/         # Exploit attempts, payloads, and PoCs
├── post_exploitation/    # Privilege escalation, persistence
├── SIEM_IDS/             # Wazuh config/logs (in progress)
├── hardening/            # Sysmon rules, audit policy, hardening notes
├── reports/              # Penetration testing reports
└── SECURITYPLUS_LAB_TRACKER.md  # Project progress tracker
🖥️ Lab Environment Overview
Component	Details
Attacker	Kali Linux 2024.2 (Dell laptop)
Target	Windows Server 2025 (Build 25398, Buypower)
Client	Windows 11 Pro (used to remotely access server)
Network	Isolated via Netgear Router (192.168.1.0/24)
SIEM/IDS	Wazuh (setup in progress)
Security Tools	Nmap, Metasploit, Hydra, Sysmon, Windows Defender
🚧 In Progress
🔧 Wazuh SIEM deployment & log forwarding setup

📡 Integration of IDS alerts with attack chains

📘 Full documentation of red team to blue team workflows

🛠️ Setup Highlights
Windows Server 2025: Active Directory enabled, Sysmon installed, Windows Defender active

Kali Linux: Primary offensive system

Network: Fully isolated, wired Cat5 Ethernet

Security: Physical access restricted; no internet exposure

🧠 Projects & Progress
Check SECURITYPLUS_LAB_TRACKER.md for current status and task tracking.

📄 License & Contributions
This repository is for educational and personal development purposes only.
Contributions, suggestions, and feedback are welcome.

📫 Let's Connect
🔹 LinkedIn: Oleh Borysovskyy

🔹 GitHub: @olehstudycyber

🔹 **Email**: [oborysovskyy@gmail.com]  

---

🚀 *Constantly learning & building in cybersecurity!*  
