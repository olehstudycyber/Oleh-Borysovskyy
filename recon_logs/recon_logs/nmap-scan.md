# 🔎 Network Reconnaissance – Nmap Scan

## 🧠 Objective
Perform a network scan to identify live hosts, open ports, and potential vulnerabilities on the target server in an isolated lab environment.

---

## 🛠️ Tools Used
- `Nmap` v7.94
- Kali Linux 2024.2

---

## 🖥️ Target Information
- IP: `192.168.1.2` (Windows Server 2025)
- Subnet: `192.168.1.0/24`

---

## 🔍 Scan Commands & Results

### 1. Basic Host Discovery

```bash
nmap -sn 192.168.1.0/24
