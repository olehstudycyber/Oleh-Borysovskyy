# Nessus Vulnerability Scan Report – Windows Server 2025
**Target IP:** 192.168.1.2  
**Hostname:** PC.narnia.com  
**Scan Date:** [Insert Date]  
**Tool:** Nessus Essentials  
**Severity Focus:** Medium  

---

## 🔍 Summary

This report documents the results of a Nessus vulnerability scan against the Windows Server 2025 target in the isolated home lab environment. The goal was to identify exploitable weaknesses and misconfigurations for hardening and testing defensive response mechanisms.

---

## 🟠 Medium Risk Findings

### 1. 📛 Self-Signed & Untrusted SSL Certificate
- **Issue:** SSL certificate is self-signed and uses an untrusted CA.
- **Details:**
  - Certificate CN: `PC.narnia.com`
  - Hostname mismatch detected
  - Cannot be verified by clients
- **Recommendation:**
  - Replace with a certificate from a trusted CA or an internal lab CA.
  - Ensure the certificate CN/SAN matches the hostname or IP address.

---

### 2. 🔐 TLS 1.0 / TLS 1.1 Supported
- **Issue:** Weak encryption protocols are still enabled.
- **Details:**
  - TLS v1.0 and v1.1 detected
- **Recommendation:**
  - Disable TLS 1.0 and TLS 1.1 using Group Policy or registry settings.
  - Enforce TLS 1.2 or TLS 1.3 only.

---

### 3. 🔓 RDP Without Network Level Authentication (NLA)
- **Issue:** NLA is not enabled for Remote Desktop Protocol.
- **Details:**
  - Exposes system to brute-force and pre-authentication attacks.
- **Recommendation:**
  - Enable NLA via System Properties or Group Policy.
  - Path: `System Properties > Remote > Require NLA`  
  - Or GPO: `Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options`

---

## ✅ Next Steps

- [ ] Apply the recommended fixes on the Windows Server 2025 host.
- [ ] Re-run Nessus scan to validate remediation.
- [ ] Cross-reference findings with Windows Event Logs (Sysmon).
- [ ] Monitor fixes using Wazuh or a centralized SIEM (coming soon).

---

## 📁 Repository Context

This report is part of the ongoing **Physical Cybersecurity Lab Penetration Testing** documentation.  
See the full lab structure and timeline in:  
[`SECURITYPLUS_LAB_TRACKER.md`](../SECURITYPLUS_LAB_TRACKER.md)
