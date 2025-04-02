# Server Build and Windows Server 2025 Installation with adding Sysmon

This document details the process of installing Windows Server 2025 on my existing PC for use as a cybersecurity home lab server, including the addition of Sysmon for advanced monitoring.

## Hardware Specifications

* **Processor:** Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz
* **RAM:** 16.0 GB
* **System Type:** 64-bit operating system, x64-based processor
* **SSD:** Samsung 840EVO 120GB

**Note:** This server is running on a repurposed desktop PC.

## Windows Server 2025 Installation Details

* **Edition:** Windows Server 2025 Standard Evaluation
* **Version:** 24H2
* **Installed On:** 1/8/2025
* **OS Build:** 26100.1742
* **Experience:** Windows Feature Experience Pack 1000.26100.18.0

## Windows Server 2025 Installation Process

1.  **Prepare the Installation Media:**
    * Downloaded the Windows Server 2025 ISO from the Microsoft Evaluation Center.
    * Used Rufus to create a bootable USB drive from the ISO.

2.  **Boot from USB:**
    * Plugged the USB drive into the PC.
    * Entered the BIOS settings and changed the boot order to prioritize the USB drive.

3.  **Windows Server Setup:**
    * The Windows Server 2025 setup wizard started.
    * Selected "Windows Server 2025 Standard (Desktop Experience)" for a full GUI installation.
    * Accepted the license agreement.
    * Chose "Custom: Install Windows only (advanced)."

4.  **Disk Partitioning:**
    * Selected the primary drive for the OS installation.
    * Created a primary partition for the OS.

5.  **Installation Process:**
    * Windows Server 2025 installation began.
    * Waited for the installation to complete.

## Network Configuration

* **IP Address:** (x.x.x.x)
* **Subnet Mask:** (x.x.x.x)
* **Gateway:** (x.x.x.x)
* **DNS:** (x.x.x.1)

## Sysmon Integration

1.  **Sysmon Installation:**
    * Downloaded Sysmon from the Microsoft Sysinternals website.
    * Installed Sysmon using the following command: `Sysmon64.exe -accepteula -i sysmonconfig.xml` (where `sysmonconfig.xml` is the configuration file).
2.  **Sysmon Configuration:**
    * Added the `sysmonconfig.xml` file to the repository.
    * The configuration file is designed to capture key security events, including process creation, network connections, and file modifications.
    * Sysmon logs are directed to the Windows Event Log under "Applications and Services Logs > Microsoft > Windows > Sysmon > Operational."
3.  **Log Analysis:**
    * Will be using windows event viewer, and powershell scripts located in the `scripts` folder to analyze logs.

## Security Considerations

* Enabled Windows Firewall.
* Implemented Sysmon for advanced system monitoring.

## Troubleshooting

* (Document any issues and solutions encountered here.)

## Diagrams

* **Network Diagram:** (Insert a network diagram created with Cisco Packet Tracer or draw.io here.)

[Back to README](README.md)
