# Home Cyber Lab – Security Onion + Windows Server 2025

## 1. Overview

This repository documents my home cyber lab built on:

- ASUS laptop – Windows 11 host running a Security Onion VM (blue‑team monitoring).
- Dell Inspiron 7386 – Windows 11 admin / client box (16 GB RAM, Wi‑Fi only).
- Windows Server 2025 – AD DS / DNS / DHCP / backup and Windows admin practice.

Goals:

- Build Windows Server admin skills (AD, DNS, DHCP, backup).
- Practice blue‑team monitoring with Security Onion.
- Generate realistic Windows events and observe them in the SIEM.

---

## 2. Hardware and Roles

### ASUS Laptop

- Host OS: Windows 11.
- Hypervisor: VMware Workstation Pro.
- VM: Security Onion (SOC web UI, Zeek, Suricata, Elastic stack).
- Purpose: Network monitoring, alerting, and log analysis.

### Dell Inspiron 7386

- Specs: i7‑8565U, 16 GB RAM, Wi‑Fi only.
- OS: Windows 11.
- Role: Admin / client workstation, light test VM host.
- Tools (planned/installed):
  - PowerShell 7, Windows Terminal.
  - Sysinternals Suite.
  - Wireshark.
  - RSAT for remote AD administration.

### Windows Server 2025 Machine

- OS: Windows Server 2025.
- Role: Domain Controller, DNS, DHCP, file/backup lab.
- Future: Source of AD logs and server events forwarded to the SIEM.

---

## 3. Network Design (High Level)

- Lab subnet for Security Onion and servers (example):
  - Security Onion IP: 172.31.38.128 (NAT/VMnet8).
- Home LAN for Wi‑Fi clients (example):
  - Dell / other clients on 192.168.x.x.
- VMware networks:
  - VMnet8 NAT configured to 172.31.38.0/24 to match Security Onion’s expected subnet.
  - Bridged / extra adapters removed or minimized to avoid routing conflicts.

---

## 4. Security Onion – Install and Fix Log

### 4.1 Initial Problem

- Symptom: “System appears to be starting. No highstate has completed since the system was restarted.”
- SOC web interface unreachable.
- Root cause: IP/subnet mismatch between Security Onion’s management config and the VM’s actual network (Bridged with 192.168.x.x vs expected 172.31.38.x).

### 4.2 Network Recovery Steps

- Updated VMware Virtual Network Editor:
  - Set VMnet8 NAT subnet to `172.31.38.0/24`.
- Updated VM network adapter:
  - Switched from Bridged / multiple adapters to a single NAT adapter on VMnet8.
- Verified services with:
  - `sudo /usr/sbin/so-status`
  - `hostname -I`
  - `sudo systemctl status salt-master`
  - `sudo systemctl restart networking`

**Lesson learned:** Security Onion is very sensitive to IP changes after install. It is usually easier to adjust the VMware network to match Security Onion’s expected subnet than to reconfigure the OS.

### 4.3 Web Access / Firewall Fix

- Symptom: Ping worked, `so-status` showed Running services, but browser timed out on `https://172.31.38.128`.
- Root cause: Security Onion host‑based firewall was blocking the actual host IP (VMware adapter IP vs physical Wi‑Fi IP).

- Fix:
  - Identified the correct host IP used to reach the VM (VMware virtual adapter).
  - Allowed it in the analyst group:

    ```bash
    sudo so-firewall includehost analyst <HOST_IP>
    sudo so-firewall apply
    ```

  - Accepted self‑signed certificate in the browser.
  - Result: SOC web login screen loaded successfully.

---

## 5. Windows Server 2025 – Plan

### 5.1 Base Install

- Fresh install of Windows Server 2025.
- Configure:
  - Static IP.
  - Hostname (e.g., `DC01`).
  - Basic firewall rules as needed.

### 5.2 Core Roles

Planned roles (phase 1):

- Active Directory Domain Services (AD DS).
- DNS.
- DHCP for lab clients.

Planned tasks:

- Promote to Domain Controller and create a new forest/domain.
- Create OUs, users, and groups.
- Configure DHCP scope for lab clients.

### 5.3 Backup and Recovery Practice

- Enable Windows Server Backup (or equivalent).
- Take:
  - System state backups.
  - Bare‑metal / full server backups.
- Recovery drills:
  - Delete a test user/group.
  - Restore from backup.
  - Verify restored object(s).

---

## 6. Dell Windows 11 – Admin / Client Workstation

### 6.1 Post‑Install Steps

- Run Windows Update until fully up to date.
- Install Dell drivers and BIOS updates.
- Configure Wi‑Fi and any necessary power/driver settings.

### 6.2 Admin Tools

- Install:
  - PowerShell 7.
  - Windows Terminal.
  - Sysinternals Suite (ProcMon, Autoruns, PsExec, Sysmon, etc.).
  - Wireshark.
  - RSAT for AD, DNS, and Group Policy management.

### 6.3 Logging and Security

- Install Sysmon with a tuned configuration.
- (Optional) Install a Wazuh/other SIEM agent once the log pipeline is ready.
- Use Dell for:
  - Domain join tests.
  - Admin tasks.
  - Investigation of events seen in Security Onion.

---

## 7. Integration Workflow

### 7.1 Domain and Clients

- Join Dell (Windows 11) to the Server 2025 domain.
- Optionally create an extra Windows client VM and join it to the domain.

### 7.2 Activity and Events

Practice scenarios:

- Logon failures and lockouts.
- Group Policy changes (password policy, lock screen, security baselines).
- File share access and NTFS permissions changes.
- Basic admin tasks (creating users, groups, OUs).

### 7.3 Monitoring and Correlation

- Ensure Security Onion sees network traffic between clients and Server 2025.
- (Future) Forward Windows event logs / Sysmon logs into the SIEM pipeline.
- For each scenario, record:
  - “Action”: what I did on a Windows box.
  - “Expected logs/alerts”: which events/alerts should appear.
  - “Observed”: what actually showed up in Security Onion / SIEM.

---

## 8. Do / Don’t Rules

**Do:**

- Install only what supports AD administration, cyber monitoring, or backup practice.
- Keep Dell and Server 2025 clean, focused, and fast.
- Document fixes, commands, and lessons learned after each lab session.

**Don’t:**

- Load the Dell with many VMs or random non‑lab apps.
- Turn lab machines into general‑purpose desktops.
- Change Security Onion’s IP casually without planning the network.

---

## 9. Status and Next Steps

**Current status:**

- Security Onion VM installed, network and firewall issues fixed, SOC web UI reachable.
- Dell Windows 11 base configuration and tools: _[fill in what is done]_.
- Server 2025: _[planned / in progress / installed]_.

**Next steps:**

1. Finish Server 2025 base install and add AD DS + DNS + DHCP.
2. Join Dell (and any client VMs) to the domain.
3. Generate test activity and confirm visibility in Security Onion.
4. Add Windows log forwarding / Sysmon integration.

---
