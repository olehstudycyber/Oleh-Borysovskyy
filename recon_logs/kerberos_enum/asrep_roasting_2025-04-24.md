# 🔐 AS-REP Roasting & Kerberos Enumeration (2025-04-24)

**Target:** 192.168.1.2 (Windows Server 2025 - `narnia.com`)  
**Attacker Machine:** Kali Linux (`192.168.1.10`)  
**Tools Used:** `kerbrute`, `impacket` (GetNPUsers.py)

---

## 🎯 Goal

- Identify valid domain usernames
- Test for Kerberos accounts with "Do not require pre-authentication"
- Retrieve AS-REP hashes for offline cracking

---

## 🧰 Step 1: Kerbrute Enumeration

**Command:**
```bash
kerbrute userenum --dc 192.168.1.2 -d narnia.com usernames.txt
