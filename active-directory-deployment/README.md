# Enterprise Windows Infrastructure Home Lab — Active Directory Deployment

## What this demonstrates
End-to-end deployment and hardening of a Windows Server-based AD environment
that mirrors a small business domain — the same core skills used in
day-to-day sysadmin work: domain setup, OU/GPO design, DNS/DHCP, and
centralized security monitoring.

## Environment
- Hypervisor: Hyper-V (host) + VMware Workstation (nested testing)
- VMs: DC01 (Windows Server 2025 - AD DS, DNS, DHCP), CLIENT01/CLIENT02
  (Windows 11 - domain-joined), SIEM01 (Wazuh + Security Onion)
- Network: isolated internal switch, 10.10.10.0/24

## What I built
- Promoted DC01 to a domain controller, configured AD DS with a
  department-based OU structure (IT, Finance, Ops) to scope GPOs cleanly
  rather than applying policy at the domain root
- Configured DNS (forward/reverse zones) and DHCP with reservations for
  infrastructure VMs
- Built Group Policy objects for password policy, screen lock timeout, and
  restricted software installation, linked per-OU
- Joined CLIENT01/CLIENT02 to the domain and verified policy application
  with `gpresult /r`
- Deployed Wazuh SIEM and Security Onion to centralize log collection from
  DC01 and both clients; enabled Sysmon on all endpoints for process-level
  visibility
- Ran Nessus and OpenVAS scans against the environment, documented findings,
  and remediated the two highest-severity issues (SMBv1 still enabled on
  one client, weak local admin password on another)

## Screenshots
[dsa.msc OU structure] · [gpresult output confirming policy applied] ·
[Wazuh dashboard showing a live alert from CLIENT01] · [Nessus scan
summary before/after remediation]

## Problems I hit and how I fixed them
Initial GPO for screen lock wasn't applying to CLIENT02 — `gpresult /r`
showed it was in the wrong OU after domain join (landed in the default
Computers container instead of the target OU). Fixed by moving the computer
object and re-running `gpupdate /force`, then documented the fix so future
domain-joins go through a checklist that avoids this.

## Scripts
- `New-DeptUsers.ps1` — bulk-creates users from a CSV and places them in the
  correct OU based on department field
- `Get-InactiveComputers.ps1` — reports computer accounts with no login in
  30+ days, for cleanup

## What I'd do differently / next steps
Next iteration: add a second DC for redundancy and test AD replication;
sync this domain to Microsoft Entra ID via Entra Connect to practice hybrid
identity, since that's a growing part of real-world sysadmin work.
