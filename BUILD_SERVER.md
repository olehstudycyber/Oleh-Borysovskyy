# Server Build and Windows Server 2025 Installation

This document details the process of installing Windows Server 2025 on my existing PC for use as a cybersecurity home lab server.

## Hardware Specifications

* **Processor:** Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz
* **RAM:** 16.0 GB
* **System Type:** 64-bit operating system, x64-based processor
* **SSD** Samsung 840EVO 120GB

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
* **DNS:** (x.x.x.1.)

## Troubleshooting

* (Document any issues and solutions encountered.)

## Security Considerations

* Enabled Windows Firewall 



## Diagrams

* **Network Diagram:** (Insert a network diagram created with Cisco Packet Tracer or draw.io here.)

**Important Notes:**

* Replace the placeholder network configuration values with your actual network settings.
* Fill in the sections regarding disk partitioning, troubleshooting, and security considerations based on your specific setup.
* If you have pictures of the pc, feel free to add them.
* This version correctly displays your hardware and operating system information.

[Back to README](README.md)
