# Home Cyber Lab - Security Onion + Windows Server 2025

**Author:** Oleh Borysovskyy
**Started:** April 2026
**Status:** Active Build - Domain Controller Live

---

## 1. Overview
This repository documents a home cyber lab built for practicing systems administration and security monitoring.

### Core Infrastructure
*   **ASUS Laptop**: Windows 11 host running Security Onion (SIEM/IDS).
*   **Dell Inspiron 7386**: Physical Windows 11 admin/client workstation.
*   **Windows Server 2025**: Virtualized Domain Controller (AD DS, DNS, DHCP).

### Goals
*   Build Windows Server administration skills (Active Directory, Group Policy).
*   Deploy and tune Security Onion for blue-team network monitoring.
*   Generate and analyze realistic Windows event logs in a SIEM environment.
*   Document a production-style SOC environment for career transition.

---

## 2. Hardware and Roles

### ASUS Laptop (Primary Host)
| Field | Value |
| :--- | :--- |
| **Host OS** | Windows 11 |
| **Hypervisor** | VMware Workstation Pro |
| **Primary VM** | Security Onion (Zeek, Suricata, Elastic Stack) |
| **Purpose** | Network monitoring and log analysis |

### Dell Inspiron 7386 (Physical Client)
| Field | Value |
| :--- | :--- |
| **Specs** | i7-8565U, 16 GB RAM |
| **Role** | Admin workstation and SOC analyst endpoint |
| **Status** | Successfully joined to `corp.local` domain |

### Windows Server 2025 (VM)
| Field | Value |
| :--- | :--- |
| **Hostname** | LAB-DC01 |
| **Domain** | corp.local |
| **Roles** | AD DS, DNS, DHCP |

---

## 3. Network Architecture
The lab utilizes a dual-homed network design to balance internal domain traffic with external internet access.

### IP Assignments
| Device | Interface | IP Address | Subnet Mask | Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **Security Onion** | VMnet8 (NAT) | 172.31.38.128| 255.255.255.0| 172.31.38.2|
| **LAB-DC01** | Ethernet0 (NAT) | 172.31.38.50| 255.255.255.0| 172.31.38.2|
| **LAB-DC01** | Ethernet1 (Bridge)| 172.20.123.90| 255.255.255.0| None|
| **Dell Laptop** | Wi-Fi (Bridge) | 172.20.123.91| 255.255.255.0| 172.20.112.1|

---

## 4. Security Onion Configuration & Fixes

### 4.1 Management Subnet Recovery
*   **Problem**: SOC interface unreachable due to IP/subnet mismatch after installation.
*   **Fix**: Updated VMware Virtual Network Editor to match the expected `172.31.38.0/24` subnet and verified services using `so-status`.

### 4.2 Firewall Access
*   **Problem**: Browser timed out when attempting to reach the Web UI.
*   **Fix**: Used `so-firewall includehost analyst <HOST_IP>` to allow the host machine to access the analyst console.

---

## 5. Windows Server 2025 Build Log

### Session 1 - April 28, 2026
*   Installed Windows Server 2025 Standard with Desktop Experience.
*   Promoted to Domain Controller for `corp.local`.
*   Created Organizational Units (OUs): `LabUsers`, `LabComputers`, `LabAdmins`.
*   Provisioned test users: `jdoe`, `asmith`, `bwilson`, and `labadmin`.

### Session 2 - April 29, 2026
*   **Dual-NIC Setup**: Configured Ethernet0 for NAT (Internet) and Ethernet1 for Bridged (LAN).
*   **Internet Access**: Resolved routing by configuring DNS Forwarders (8.8.8.8) and setting interface metrics.
*   **Connectivity Fix**: Standardized subnet masks across all lab devices to `255.255.255.0` and explicitly bound VMnet0 to the physical Wi-Fi adapter.
*   **Success**: Physical Dell Laptop successfully joined the `corp.local` domain.

---

## 6. Integration & Career Goals

### Roadmap
1.  **Phase 1 (Identity)**: Implement GPOs for account lockouts and password complexity.
2.  **Phase 2 (Monitoring)**: Deploy Sysmon and forward Windows event logs to Security Onion.
3.  **Phase 3 (Simulation)**: Conduct Nmap scans and brute-force simulations to test SIEM alerting.

### Career Alignment
This lab serves as a portfolio project for transitioning to **SOC Analyst** or **Systems Administrator** roles by demonstrating hands-on experience in AD administration, SIEM deployment, and incident response.

---
*Last Updated: April 29, 2026*
