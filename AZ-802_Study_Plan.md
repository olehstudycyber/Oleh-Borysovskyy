# AZ-802 Study Plan (Administering Windows Server)

**Note on timing:** AZ-802 is in beta as of mid-2026, consolidating AZ-800 + AZ-801. Microsoft hasn't published official domain weightings yet, so this plan is built from the announced skills-measured areas (identity, management, compute, networking, storage, security, high availability/DR, monitoring) plus the new AI-infrastructure content Microsoft has flagged. Check the official study guide on Microsoft Learn before you finalize your schedule — the exact breakdown may shift as it moves toward general availability.

**Starting point:** Your home lab already covers AD DS, DNS, DHCP, Group Policy, Hyper-V, VMware, and PowerShell — so weeks 1–2 are lighter review rather than new material. The heavier lift is the hybrid/Azure-integration layer (Entra Connect, Azure Arc, Azure Monitor) and high-availability/DR, which your lab doesn't touch yet. Week 0 below is a low-effort head start on the Azure side, tied to a Virtual Training Day you've already registered for.

---

## Week 0: Azure Fundamentals (AZ-900) — kickoff
*Registered: Microsoft Virtual Training Day — Introduction to Microsoft Azure, July 20, 2026, 12:00–4:00 PM ET.*

- Attend the Virtual Training Day (cloud concepts, Azure architecture, networking, storage, identity, management/governance)
- Within 1–2 weeks after: schedule and take the AZ-900 exam using the 50%-off code from the training day, before it expires
- **Why this matters for AZ-802:** AZ-900 covers the Azure-side concepts (compute, networking, storage, identity, shared responsibility model) that your home lab doesn't touch yet — this is real groundwork for the hybrid/Azure-integration parts of AZ-802 (Entra Connect, Azure Arc, Azure Monitor, Azure File Sync), not a detour from it
- **Lab task:** none required — this week is training + exam only. If time allows, create a free Azure account and click through the portal to match what you saw in the training (resource groups, a basic VM, storage account) so the concepts aren't purely theoretical

## Week 1–2: Identity foundations + hybrid identity
*Lab already covers most of this — extend rather than rebuild.*

- Review: AD DS deployment, OUs, GPOs, trusts (you have this)
- New: Deploy Microsoft Entra Connect / Entra Connect Sync in your lab, sync your existing AD users to a free Entra ID tenant
- New: Configure password hash sync vs. pass-through authentication; understand password writeback
- New: Certificate services basics (AD CS) if not already in your lab
- **Lab task:** Sync your existing domain to Entra ID and document the sync topology

## Week 3: Windows Server management tooling
- Windows Admin Center — install and manage your lab servers through it instead of RDP/Server Manager
- Azure Arc — onboard your on-prem VMs to Azure Arc, explore Arc-enabled management
- PowerShell DSC (Desired State Configuration) basics if you haven't used it
- **Lab task:** Onboard 2–3 lab servers to Azure Arc; screenshot the inventory view for your writeup

## Week 4: Compute — VMs and containers
- Hyper-V deep dive: checkpoints, replication, dynamic memory, nested virtualization
- Windows containers basics (you likely haven't touched this) — pull and run a Windows container image
- Azure VM migration concepts (even if you don't migrate anything for real, understand the workflow)
- **Lab task:** Stand up one Windows container alongside your VMs; note the difference in resource footprint

## Week 5: Hybrid networking
- On-prem: routing, VPN concepts, DNS you already know
- New: Azure Public DNS, Azure Private DNS, Azure DNS Private Resolver — integrate with your lab DNS
- New: Site-to-site VPN concepts between on-prem and Azure (can simulate with Azure free tier)
- **Lab task:** Set up Azure Private DNS and resolve a lab hostname through it

## Week 6: Storage and file services
- Storage Spaces, Storage Replica, DFS Namespaces/Replication
- Azure File Sync — sync a lab file share to an Azure Storage account
- iSCSI targets, storage QoS basics
- **Lab task:** Configure Azure File Sync between your lab and an Azure storage account (free tier covers this)

## Week 7: High availability and disaster recovery
*This is the area your current lab covers least — give it extra time.*

- Failover clustering fundamentals — build a 2-node cluster in your lab if hardware allows
- Storage Spaces Direct (S2D) concepts
- Azure Site Recovery for DR scenarios
- Backup strategies: Windows Server Backup vs. Azure Backup
- **Lab task:** Build a basic failover cluster (even a simple file server cluster) and document the failover test

## Week 8: Security hardening + monitoring
*Your Wazuh/Sysmon/Nessus experience gives you a head start here — this is mostly translating existing skills to the Microsoft-native tools.*

- Microsoft Defender for Cloud — enable on your Arc-onboarded servers
- Azure Monitor + Log Analytics — pipe lab server logs in
- Azure Update Manager — patch management across hybrid servers
- Security baselines and hardening (compare to what you already do with Defender/Wazuh)
- **Lab task:** Connect Azure Monitor to your lab servers and build one basic alert rule

## Week 9: AI-infrastructure content (new to AZ-802)
- This is flagged as new material not in AZ-800/801 — official guidance is still emerging
- Check the Microsoft Learn study guide directly for this section once finalized, since it's the area most likely to catch underprepared candidates off guard
- Likely focus: infrastructure considerations for hosting AI workloads (compute sizing, storage throughput, networking for GPU/inference workloads) rather than AI model development itself

## Week 10: Review and practice exams
- Take a full-length practice exam, identify weak domains
- Re-review weak areas using Microsoft Learn modules
- Re-do any lab tasks you rushed through
- Schedule the exam once you're consistently scoring 80%+ on practice tests

---

## General tips
- **Use Microsoft Learn's free learning paths** as your primary source — they're built directly from the same team that writes the exam.
- **Hands-on beats reading.** Every week above has a lab task — don't skip these even if you feel confident on theory. AZ-802 questions tend to be scenario-based.
- **Track skills-measured updates.** Since this is a beta exam, the official skills outline may be revised before general availability — check back before your final review week.
- **Renewal note:** if you already hold AZ-800 or AZ-801 by the time you read this, you can use the AZ-802 renewal assessment instead of taking the full exam — check your specific situation on Microsoft Learn.
