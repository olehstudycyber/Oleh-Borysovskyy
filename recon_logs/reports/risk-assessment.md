# 🧾 Risk Assessment Report – Lab Environment

## 🧠 Summary
This report summarizes the risks identified during lab-based penetration testing on the Windows Server 2025 machine.

---

## 🧩 Key Findings

| Risk ID | Description                         | Severity | Mitigation                      |
|--------|-------------------------------------|----------|---------------------------------|
| R-001  | SMBv1 vulnerability open on port 445 | High     | Patch OS, disable SMBv1         |
| R-002  | Weak RDP configuration               | Medium   | Enable NLA, restrict access     |
| R-003  | No IDS/Firewall rule customization   | Medium   | Deploy Wazuh, tune Defender     |

---

## 📋 Recommendations
- Apply latest patches to OS and services
- Harden RDP access (e.g., 2FA, VPN tunneling)
- Deploy and monitor with SIEM (e.g., Wazuh)

---

## ✅ Conclusion
Risks identified were expected for a test environment. Documentation supports future hardening and detection configuration.
