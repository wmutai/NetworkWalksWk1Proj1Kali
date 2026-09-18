# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000)
![Version](https://img.shields.io/badge/Ver-VirtualBox%20v7.2-0070C0?style=flat-square&labelColor=000000)
![Kali](https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white)
![Skill](https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000)
![Pentest](https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white)
![Skill](https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000)

---

## 📌 Project Overview

This project documents the setup of an **isolated virtual cybersecurity and penetration-testing lab** using VirtualBox and Kali Linux.

The goal is a controlled environment where scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be carried out safely and repeatably. The lab runs on a private virtual network so additional target machines can be added later.

---

## 🎯 Objectives

- Install and configure VirtualBox
- Install/import Kali Linux as a virtual machine
- Create a private NAT Network for the lab
- Configure network connectivity for the Kali VM
- Assign a consistent IP address to the Kali VM
- Verify connectivity and DNS resolution
- Take a clean VM snapshot for recovery
- Document the full setup process
- Prepare the environment for future exercises

---

## 🛡️ Purpose of the Lab

This lab provides an isolated, controlled space for learning and authorized security testing, including:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security tool experimentation

⚠️ **Important:** Use this lab only against systems you own or have explicit written permission to test.

---

## 🏗️ Lab Architecture

<!-- Add a screenshot or diagram here, e.g.: -->
<!-- ![Lab Architecture](./screenshots/architecture.png) -->

Additional target machines can be added to the same virtual network in future projects.

---

## ⚙️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration      |
|---------------------|------------------------|
| 🖥️ Host OS          | *e.g. macOS / Windows 10* |
| 🧠 Host RAM          | *e.g. 16 GB*            |
| ⚡ Processor         | *e.g. Apple M2 / Intel i7* |
| 🧰 Hypervisor        | VirtualBox *(version)* |
| 🐉 Security OS       | Kali Linux *(version)* |
| 🧠 Kali RAM          | *e.g. 2048 MB*          |
| 🌐 Virtual Network   | NAT Network             |
| 📡 Network Address   | *e.g. 10.0.0.0/24*      |
| 🐧 Kali IP Address   | *e.g. 10.0.0.2/24*      |
| 🚪 Default Gateway   | *e.g. 10.0.0.1*         |
| 🌍 DNS Server        | *e.g. 8.8.8.8*          |
| 🔮 Future VM Range   | *e.g. 10.0.0.3–10.0.0.99* |

---

# 🪜 Lab Setup Procedure

## Step 1. Install 7-Zip *(if needed)*

Used to extract the Kali Linux VM package if distributed as a `.7z` archive.

## Step 2. Install VirtualBox

Installed as the hypervisor for the lab.

## Step 3. Create the NAT Network

Configuration:
```
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.2/24
DHCP:         Enabled
IPv6:         Disabled
```

A NAT Network is used (rather than plain NAT) so multiple VMs on the same network can communicate with each other while still reaching the internet — this lets future attacker/target VMs talk to one another.

<!-- ![NAT Network Settings](./screenshots/nat-network.png) -->

## Step 4. Import Kali Linux

Network adapter configuration:
```
Adapter 1
Attached to:   NAT Network
Network:       NatNetwork
Adapter Type:  Intel PRO/1000 MT Desktop
```

VM resources allocated:
```
RAM: 2048 MB
```

<!-- ![Kali Linux VM](./screenshots/kali-import.png) -->

## Step 5. Configure the Kali Linux Network

Example static configuration:
```
IP Address:   10.0.0.2
Subnet Mask:  255.255.255.0
Gateway:      10.0.0.1
DNS:          8.8.8.8
```

<!-- ![Kali Network Settings](./screenshots/kali-network-settings.png) -->

## Step 6. Create a Clean VM Snapshot

Example snapshot name:
#SCREENSHOTS

```
Clean Kali - Network Setup
```

This snapshot is the baseline the VM can be restored to if a future exercise breaks the configuration.

---

# 🔎 Lab Verification

| ✅ Test                     | 🧾 Command                     | 🎯 Expected Result               |
|-----------------------------|---------------------------------|-----------------------------------|
| 🌐 Check IP address          | `ip a`                          | Correct Kali IP displayed         |
| 📡 Test gateway              | `ping 10.0.0.1`                 | Successful replies                |
| 🌍 Test internet connectivity| `ping 8.8.8.8`                  | Successful replies                |
| 🔎 Test DNS resolution       | `nslookup google.com`           | Domain resolves                   |
| 🧰 Verify Nmap                | `nmap --version`                | Nmap version displayed            |
| 🔄 Verify snapshot            | Restore snapshot, run `ip a`    | Baseline configuration restored   |

### Example Results
```
IP Address: 10.0.0.2/24
Gateway:    10.0.0.1
DNS:        8.8.8.8
```

---

# 🐞 Problems Encountered & Solutions

## Problem 1. *(e.g. Internet connectivity after static IP config)*

*Describe the issue you hit.*

Fix used:
```
# example command
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```
> **Note:** Interface/connection names vary by system — check yours before running commands like this.

## Problem 2. *(e.g. VirtualBox VT-x / virtualization error)*

*Describe the issue.*

Resolved by:
1. Restart the computer
2. Enter BIOS/UEFI settings
3. Enable hardware virtualization (Intel VT-x / AMD-V)
4. Save and restart
5. Start the VM again

---

# 💡 What I Learned

### 1. NAT vs NAT Network
*Your takeaway on the difference and why it matters for a multi-VM lab.*

### 2. Virtual Machine Networking
*What you learned about how VirtualBox adapters connect VMs.*

### 3. Static IP Configuration
*What you learned about configuring IP, subnet, gateway, DNS in Kali.*

### 4. VM Snapshots
*Why a clean baseline snapshot matters before risky exercises.*

### 5. Documentation
*Why documenting commands, screenshots, problems, and fixes matters.*

---

# 🔐 Security & Ethical Use

This lab is intended strictly for educational purposes.

---

# 🔗 Tools & Resources

- **VirtualBox:** https://virtualbox.org/wiki/Downloads
- **Kali Linux:** https://kali.org/get-kali
- **7-Zip:** https://7-zip.org/download.html

---

# 👤 Author

**  Willy Mutai
*Intern/ Network Walks/ B083C

LinkedIn: www.linkedin.com/in/kiprono-mutai

---

## 📌 Project Information

**Program:** *e.g. NetworkWalks Cybersecurity* | **Week:** *e.g. 01* | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub
