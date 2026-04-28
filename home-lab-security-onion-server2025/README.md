# Home Cyber Lab - Security Onion + Windows Server 2025

**Author:** Oleh Borysovskyy
**Started:** April 2026
**Status:** Active Build - Domain Controller Live

---

## 1. Overview

This repository documents my home cyber lab built on:
- **ASUS laptop** - Windows 11 host running a Security Onion VM (blue-team monitoring).
- **Dell Inspiron 7386** - Windows 11 admin / client box (16 GB RAM, Wi-Fi only).
- **Windows Server 2025** - AD DS / DNS / DHCP / backup and Windows admin practice.

### Goals
- Build Windows Server admin skills (AD, DNS, DHCP, backup).
- Practice blue-team monitoring with Security Onion.
- Generate realistic Windows events and observe them in the SIEM.
- Build a production-style SOC environment for career transition.

---

## 2. Hardware and Roles

### ASUS Laptop
| Field | Value |
|---|---|
| Host OS | Windows 11 |
| Hypervisor | VMware Workstation Pro |
| VM | Security Onion (SOC web UI, Zeek, Suricata, Elastic stack) |
| Purpose | Network monitoring, alerting, and log analysis |

### Dell Inspiron 7386
| Field | Value |
|---|---|
| Specs | i7-8565U, 16 GB RAM, Wi-Fi only |
| OS | Windows 11 |
| Role | Admin / client workstation, light test VM host |

### Windows Server 2025 (VM)
| Field | Value |
|---|---|
| OS | Windows Server 2025 Standard (Desktop Experience) |
| Hostname | LAB-DC01 |
| Domain | corp.local |
| Role | Domain Controller, DNS, DHCP, file/backup lab |

---

## 3. Network Design

### Lab Subnet (VMware NAT - VMnet8)
| Device | IP | Role |
|---|---|---|
| VMware NAT Gateway | 172.31.38.2 | Default gateway |
| Security Onion | 172.31.38.128 | SIEM / IDS monitoring |
| LAB-DC01 (WinServer) | 172.31.38.50 | Domain Controller (planned static) |

### VMware Networks
- **VMnet8 (NAT)** - 172.31.38.0/24 - Lab VMs
- All lab traffic routed through VMware NAT

---

## 4. Security Onion - Install and Fix Log

### 4.1 Initial Problem
- **Symptom:** "System appears to be starting. No highstate has completed since the system was restarted."
- **Root cause:** IP/subnet mismatch between Security Onion's management config and the VM's actual network.
- **Lesson:** Security Onion is very sensitive to IP changes after install.

### 4.2 Network Recovery Steps
1. Updated VMware Virtual Network Editor - Set VMnet8 NAT subnet to 172.31.38.0/24
2. Switched VM from Bridged to single NAT adapter on VMnet8
3. Verified services:
   ```
   sudo /usr/sbin/so-status
   sudo systemctl status salt-master
   sudo systemctl restart networking
   ```

### 4.3 Web Access / Firewall Fix
- **Symptom:** Ping worked, but browser timed out on https://172.31.38.128
- **Fix:** Allowed host IP in analyst group
   ```
   sudo so-firewall includehost analyst <HOST_IP>
   sudo so-firewall apply
   ```
- **Result:** SOC web login screen loaded successfully.

---

## 5. Windows Server 2025 - Build Log

### Session 1 - April 28, 2026
| Task | Status |
|---|---|
| Fresh install Windows Server 2025 Standard (Desktop Experience) | Complete |
| VMware Tools installed | Complete |
| Renamed to LAB-DC01 | Complete |
| AD DS role installed | Complete |
| DNS Server role installed | Complete |
| Promoted to Domain Controller | Complete |
| Domain created: corp.local | Complete |
| OU: LabUsers created | Complete |
| OU: LabComputers created | Complete |
| OU: LabAdmins created | Complete |
| User: jdoe (LabUsers) | Complete |
| User: asmith (LabUsers) | Complete |
| User: bwilson (LabUsers) | Complete |
| User: labadmin (LabAdmins, Domain Admins + Enterprise Admins) | Complete |
| Snapshot: clean-base-setup | Taken |
| Snapshot: AD-DS-installed | Taken |

### Planned (Phase 2)
- [ ] Set static IP: 172.31.38.50
- [ ] Configure DHCP scope: 172.31.38.100-200
- [ ] Join Dell Windows 11 to corp.local domain
- [ ] Create Group Policy: password policy, lockout policy
- [ ] Install Sysmon on all Windows endpoints
- [ ] Forward Windows event logs to Security Onion

---

## 6. Dell Windows 11 - Admin / Client Workstation

### Planned Setup
- [ ] Windows Update fully applied
- [ ] PowerShell 7 + Windows Terminal
- [ ] Sysinternals Suite (ProcMon, Autoruns, PsExec, Sysmon)
- [ ] Wireshark
- [ ] RSAT for AD, DNS, and Group Policy management
- [ ] Join to corp.local domain
- [ ] Configure as SOC analyst workstation

---

## 7. Integration Workflow

### Phase 1 - Identity
- [ ] Domain users logging in across lab machines
- [ ] Group Policy applied and verified
- [ ] Account lockout testing

### Phase 2 - Monitoring
- [ ] Security Onion sees traffic between all lab hosts
- [ ] Sysmon logs forwarded to SIEM
- [ ] Windows Event Logs (4624, 4625, 4688, etc.) visible in Security Onion

### Phase 3 - Attack Simulation
- [ ] Brute force attack (Hydra) - detected by Suricata/Wazuh
- [ ] Port scan (Nmap) - detected by Zeek/Suricata
- [ ] Malware simulation (EICAR) - Defender + Wazuh alert
- [ ] Lateral movement with domain credentials
- [ ] Incident reports written for each scenario

---

## 8. Do / Don't Rules

### Do
- Install only what supports AD administration, cyber monitoring, or backup practice.
- Keep Dell and Server 2025 clean, focused, and fast.
- Document fixes, commands, and lessons learned after each lab session.
- Take snapshots before major changes.

### Don't
- Load the Dell with many VMs or random non-lab apps.
- Turn lab machines into general-purpose desktops.
- Change Security Onion's IP casually without planning the network.

---

## 9. Tools Reference

| Tool | Purpose | Status |
|---|---|---|
| VMware Workstation Pro 17 | Hypervisor | Installed |
| Security Onion | SIEM / IDS / NSM | Running |
| Windows Server 2025 | Domain Controller | Live |
| Active Directory | Identity management | Live |
| pfSense | Firewall (planned) | Pending |
| Kali Linux | Attack simulation (planned) | Pending |
| Sysmon | Endpoint telemetry | Pending |
| Wazuh | Host-based monitoring | Pending |

---

## 10. Career Goals

This lab supports my transition from IT Assistant to SOC Analyst / Systems Administrator:
- Hands-on AD DS administration
- SIEM deployment and log analysis
- Security monitoring and incident response
- MITRE ATT&CK mapping from real attack simulations
- Documented project for portfolio and GitHub

---

*Last updated: April 28, 2026*
