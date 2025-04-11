# Nmap Reconnaissance - Windows Server 2025

## Overview
This reconnaissance scan was conducted from the Kali Linux attacker machine targeting Windows Server 2025 on a dedicated, isolated lab network. The purpose of the scan was to enumerate open ports, identify services, and fingerprint the OS.

## Target Details
- **IP:** 192.168.1.2
- **OS:** Windows Server 2025
- **Defenses:** Windows Defender enabled, Sysmon installed

## Attacker Details
- **Machine:** Kali Linux
- **IP:** 192.168.1.10
- **Tool Used:** `nmap`

## Nmap Command
```bash
nmap -sS -sV -O -Pn 192.168.1.2
```

## Key Results
- **Open Ports:** 22, 135, 445
- **Closed:** 3389
- **Service Versions:** OpenSSH 9.2, Windows RPC, SMB
- **OS Detection:** Windows Server 2022 or 2025

## Diagram
![Nmap Recon Diagram](nmap_recon_diagram.png)