# Windows Server 2025 Active Directory Lab Environment  
## Enterprise Systems Administration with Integrated Security Visibility

---

## Overview

This repository documents a Windows Server 2025 Active Directory lab environment built to simulate enterprise-scale systems administration tasks. The lab focuses on identity management, Windows infrastructure services, and administrative automation using PowerShell.

The environment is designed to replicate core responsibilities of a **Junior Systems Administrator**, including domain services configuration, user and group management, Group Policy implementation, and endpoint integration.

A secondary security visibility layer is included using Security Onion to observe network and authentication activity within the domain environment.

---

### Primary Focus
- Windows Server administration
- Active Directory Domain Services (AD DS)
- User, group, and computer management
- Group Policy Object (GPO) configuration
- PowerShell automation for administrative tasks

### Secondary Layer
- Security Onion deployment for passive network monitoring
- Log visibility of authentication and domain activity
- Basic security-aware infrastructure observation

---

## Lab Architecture

**Domain Environment**
- Domain: `corp.local`
- Domain Controller: Windows Server 2025 (LAB-DC01)
- Client Machine: Windows 11 (Dell Inspiron)

**Core Services**
- Active Directory Domain Services (AD DS)
- DNS (integrated with AD)
- DHCP (lab scope configuration)
- Group Policy Management

**Networking**
- NAT + Bridged virtual network configuration
- Internal domain communication between server and client systems

---

## Active Directory Administration

### Domain Structure

The following Organizational Units (OUs) were created to simulate a structured enterprise environment:

- **LabUsers** – Standard user accounts by role/department
- **LabComputers** – Domain-joined endpoint devices
- **LabAdmins** – Privileged administrative accounts

---

### User & Group Management

Test accounts were created to simulate real-world IT administration workflows:

- Standard users:
  - jdoe
  - asmith
  - bwilson

- Administrative account:
  - labadmin (Domain Admins group)

---

### Completed Administrative Tasks

- Domain Controller promotion (LAB-DC01)
- Active Directory Domain Services (AD DS) installation
- DNS role configuration with external forwarders (8.8.8.8)
- Windows 11 client successfully joined to domain
- Organizational Unit (OU) structure implementation
- Basic user and group creation via GUI and PowerShell

---

### In Progress

- Group Policy Object (GPO) configuration:
  - Password policy enforcement
  - Account lockout policy
  - Desktop restriction policies

- PowerShell automation:
  - Bulk user provisioning from CSV
  - Automated group assignment scripts

- Backup and recovery simulation for Active Directory

---

## PowerShell Automation

This lab includes PowerShell scripts to simulate real IT administrative workflows.

Planned scripts include:

- `New-BulkUsers.ps1` – Bulk creation of AD users from CSV
- `Add-UsersToGroups.ps1` – Automated group membership assignment
- `Reset-LabPasswords.ps1` – Password reset automation for test accounts

These scripts demonstrate infrastructure automation and administrative efficiency.

---

## Group Policy Configuration

Group Policy Objects are used to simulate enterprise endpoint control and security policies.

Planned GPO implementations:

- Password complexity and expiration policies
- Account lockout thresholds
- Control Panel and system restriction policies
- Network drive mapping for domain users

---

## Security Visibility Layer (Security Onion)

Security Onion is deployed as a supplemental monitoring tool within the lab environment.

It is used to:
- Observe authentication activity within the domain
- Monitor network traffic between server and client systems
- Provide log visibility into Active Directory operations

This layer is used for **observability purposes only** and is not the primary focus of the lab.

---

## Key Skills Demonstrated

- Active Directory Domain Services (AD DS) administration
- Windows Server 2025 configuration and management
- DNS and DHCP infrastructure services
- Group Policy Object (GPO) design and deployment
- PowerShell-based user and system automation
- Domain-joined client troubleshooting
- Basic network monitoring and log analysis

---

## Career Alignment

This project is aligned with entry-level and junior-level infrastructure roles:

- Junior Systems Administrator
- Windows Server Administrator
- IT Systems Administrator
- Infrastructure Support Engineer

The lab demonstrates practical experience with enterprise Windows environments, identity management systems, and administrative automation workflows.

---

## Next Development Phase

Planned enhancements to this environment:

1. Expand Group Policy implementation to simulate corporate IT policy enforcement
2. Build full PowerShell-based user lifecycle management system
3. Introduce controlled break/fix scenarios (password lockouts, DNS misconfigurations)
4. Document troubleshooting workflows as case studies
5. Expand Security Onion visibility for deeper network observation

---

## Repository Purpose

This repository serves as a structured demonstration of hands-on Windows systems administration skills, replicating real-world enterprise IT infrastructure and operational workflows.
