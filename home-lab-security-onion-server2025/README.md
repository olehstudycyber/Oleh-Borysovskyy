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

### Lab Subnets
- **VMnet8 (NAT):** 172.31.38.0/24 - Internal Lab traffic & Internet.
- **Bridged LAN:** 172.20.123.0/24 - Direct link for physical client (Dell laptop).

### Current IP Table
| Device | Interface | IP Address | Subnet Mask | Gateway |
|---|---|---|---|---|
| VMware NAT Gateway | VMnet8 | 172.31.38.2 | 255.255.255.0 | - |
| Security Onion | NAT | 172.31.38.128 | 255.255.255.0 | 172.31.38.2 |
| LAB-DC01 | Ethernet0 (NAT) | 172.31.38.50 | 255.255.255.0 | 172.31.38.2 |
| LAB-DC01 | Ethernet1 (Bridge)| 172.20.123.90 | 255.255.255.0 | None |
| Dell Laptop | Wi-Fi (Bridge) | 172.20.123.91 | 255.255.255.0 | 172.20.112.1 |

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
   ```bash
   sudo /usr/sbin/so-status
   sudo systemctl status salt-master
   sudo systemctl restart networking
