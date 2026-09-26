# NETWORKWALKS: Cybersecurity Lab Setup - Week 1

**Student:** Ibrahim Saminu  
**Course:** Network Walks  
**Week:** 1 - Practical Milestone 1  
**Lab Type:** Local Penetration Testing & Network Security Environment

---

## 📋 Project Overview

This repository documents the complete setup and configuration of a **isolated cybersecurity laboratory environment** for hands-on network security research, packet analysis, and ethical hacking exercises. The lab is built using VirtualBox with Kali Linux as the attack platform in a controlled NAT Network to ensure safety and separation from production systems.

---

## 🎯 Lab Objectives

- ✅ Install and configure Oracle VirtualBox 7.0 on Windows host
- ✅ Deploy Kali Linux 2026 as the primary attack/testing platform
- ✅ Configure isolated NAT Network for controlled environment
- ✅ Establish secure network connectivity between host and VMs
- ✅ Test network functionality and connectivity
- ✅ Document setup process, errors, and troubleshooting solutions
- ✅ Create reproducible cybersecurity sandbox environment

---

## 🛠️ Tools & Technologies

| Component | Version | Purpose |
|-----------|---------|---------|
| **Hypervisor** | Oracle VirtualBox 7.0 | Virtual machine platform |
| **Attack OS** | Kali Linux 2026 | Penetration testing framework |
| **Host OS** | Windows | Development machine |
| **Network Type** | NAT Network | Isolated network segment |
| **IP Subnet** | 10.0.0.0/24 | Lab network range |

---

## 🏗️ Lab Architecture

```text
┌─────────────────────────────────────────────────┐
│         Windows Host Machine (10.0.0.x)         │
│                                                 │
│  ┌─────────────────────────────────────────┐  │
│  │   VirtualBox Hypervisor Engine 7.0      │  │
│  │                                         │  │
│  │  ┌─────────────────────────────────┐   │  │
│  │  │  NAT Network (10.0.0.0/24)      │   │  │
│  │  │                                 │   │  │
│  │  │  Gateway: 10.0.0.1              │   │  │
│  │  │  DNS: 8.8.8.8 (Google DNS)      │   │  │
│  │  │                                 │   │  │
│  │  │  ┌─────────────────────────┐   │   │  │
│  │  │  │  Kali Linux 2026        │   │   │  │
│  │  │  │  IP: 10.0.0.2/24        │   │   │  │
│  │  │  │  vCPU: 2 cores          │   │   │  │
│  │  │  │  RAM: 2-4 GB            │   │   │  │
│  │  │  │  Storage: 20+ GB        │   │   │  │
│  │  │  └─────────────────────────┘   │   │  │
│  │  │                                 │   │  │
│  │  └─────────────────────────────────┘   │  │
│  │                                         │  │
│  └─────────────────────────────────────────┘  │
│                                                 │
└─────────────────────────────────────────────────┘
```

---

## 📊 Network Configuration Table

| Parameter | Value | Description |
|-----------|-------|-------------|
| **Network Type** | NAT Network | Isolated, NAT-enabled network |
| **Subnet CIDR** | 10.0.0.0/24 | Private network range |
| **Gateway IP** | 10.0.0.1 | VirtualBox NAT gateway |
| **DNS Server** | 8.8.8.8 | Google Public DNS |
| **Kali Linux IP** | 10.0.0.2/24 | Attack platform address |
| **Host Connectivity** | NAT | Bidirectional, isolated from host |
| **External Access** | Restricted | Controlled outbound only |

---

## 📦 VirtualBox 7.0 Installation & Setup

### Step 1: Download & Install VirtualBox
1. Download Oracle VirtualBox 7.0 from virtualbox.org
2. Choose Windows installer for your system
3. Run the installer and follow the setup wizard
4. Install VirtualBox Extension Pack (recommended)
5. Reboot your Windows machine

### Step 2: Create NAT Network
1. Open VirtualBox in **Expert Mode** (not Basic Mode)
   - Important: Use **Expert Mode** to access Network settings
2. Go to **File → Tools → Network Manager**
3. Click **Create** to add a new NAT Network
4. Configure as follows:
   - **Network Name:** NatNetwork
   - **CIDR:** 10.0.0.0/24
   - **Gateway:** 10.0.0.1
   - **DNS:** 8.8.8.8

### Step 3: Create Virtual Machine
1. Click **New** in VirtualBox Manager
2. Allocate resources:
   - **vCPU:** 2 cores minimum
   - **RAM:** 2-4 GB
   - **Storage:** 20-30 GB dynamically allocated
3. Attach Kali Linux ISO image
4. Configure network adapter to use the NAT Network created above

---

## 🐧 Kali Linux 2026 Setup

### Step 1: Download Kali Linux ISO
- Download the Kali Linux 2026 ISO from the official Kali website
- Verify checksum if required

### Step 2: VM Creation & Boot
1. Create a new VM with:
   - **OS Type:** Linux → Debian 12.x 64-bit
   - **vCPU:** 2 cores
   - **RAM:** 4 GB
   - **HDD:** 20 GB
   - **Network Adapter:** NAT Network
2. Mount the Kali ISO and boot the VM
3. Complete the installation process and reboot

### Step 3: Post-Installation Configuration
```bash
sudo apt update && sudo apt upgrade -y
ping 8.8.8.8
ip addr show
nslookup google.com
```

---

## 🔧 Network Configuration Details

### Kali Linux Network Setup
```bash
ip link show
ip addr show
route -n
nmcli device show
ping 10.0.0.1
ping google.com
```

### VirtualBox Network Adapter Settings
- **Attachment:** NAT Network
- **Cable Connected:** Enabled
- **Promiscuous Mode:** Allow All

---

## ✅ Connectivity Testing & Results

### Test 1: Gateway Connectivity
```bash
ping -c 4 10.0.0.1
```
Result: Gateway reachable successfully.

### Test 2: DNS Resolution
```bash
nslookup google.com
```
Result: DNS resolution working.

### Test 3: Internet Connectivity
```bash
ping -c 4 google.com
```
Result: Internet connectivity confirmed.

---

## ⚠️ Errors Faced & Troubleshooting Solutions

### Error 1: Network Bar Not Visible in VirtualBox

**Problem:**
- The network settings and NAT networking options were not visible.

**Root Cause:**
- VirtualBox was used in **Basic Mode** instead of **Expert Mode**.

**Solution:**
1. Reopened VirtualBox in **Expert Mode**.
2. Accessed **Tools → Network Manager**.
3. Created the NAT Network manually.
4. Reassigned the VM to the NAT Network.

**Result:** Network configuration became visible and functional.

---

### Error 2: Kali Linux VM Failed to Start

**Problem:**
- The Kali Linux VM would not start properly.

**Root Cause:**
- Incorrect VM configuration and resource settings, combined with missing troubleshooting steps.

**Solution:**
1. Reviewed the admin guidance and troubleshooting instructions.
2. Checked the VM resource allocation and boot configuration.
3. Corrected settings and followed the recommended fix steps.
4. Rebooted the VM after configuration adjustments.

**Result:** Kali Linux booted successfully.

---

## 📸 Screenshots & Documentation

The repository should include screenshots of:
- VirtualBox installation
- NAT Network configuration
- Kali Linux VM settings
- Kali Linux desktop after setup
- Successful connectivity testing output
- Troubleshooting steps and fixes

---

## 🔒 Security & Ethics Statement

This cybersecurity lab environment is configured for:
- Authorized educational learning
- Controlled security research
- Isolated network testing
- Ethical hacking practice

This lab is confined to a private virtual network and must not be connected to production or unauthorized systems.

---

## 📝 Summary & Conclusions

This practical milestone successfully demonstrated how to:
- Install VirtualBox 7.0 on Windows
- Setup Kali Linux 2026 in a controlled environment
- Create a NAT Network with a safe lab configuration
- Resolve common setup and boot issues
- Verify network functionality and connectivity

The environment is now ready for secure networking and ethical testing activities.

---

## 📚 References

- Oracle VirtualBox Documentation
- Kali Linux Official Site
- VirtualBox Network Configuration Guide

---

**Student:** Ibrahim Saminu  
**Week:** 1  
**Status:** Completed ✅
