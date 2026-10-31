<div align="center">

# 🪟 Windows 10 Lab Setup – Authorized Target Machine

### NetworkWalks Cybersecurity Internship · Batch B084J · Week 01 · PMx Extra Project

![Windows 10](https://img.shields.io/badge/Windows_10-Target_VM-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![VMware](https://img.shields.io/badge/VMware-Workstation_17-607078?style=for-the-badge&logo=vmware&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-Attacker_VM-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Networking](https://img.shields.io/badge/Network-VMnet2_NAT-0A66C2?style=for-the-badge)
![Ethical Hacking](https://img.shields.io/badge/Ethical_Hacking-Authorized_Only-2EA44F?style=for-the-badge)
![NetworkWalks](https://img.shields.io/badge/NetworkWalks-Batch_B084J-FF6A00?style=for-the-badge)

</div>

---

## 📑 Table of Contents

1. [Project Title and Overview](#1--project-title-and-overview)
2. [Project Objectives](#2--project-objectives)
3. [Lab Architecture](#3--lab-architecture)
4. [Hardware and Software Requirements](#4--hardware-and-software-requirements)
5. [Lab Configuration Table](#5--lab-configuration-table)
6. [Windows 10 VM Setup](#6--windows-10-vm-setup)
7. [VMware Network Configuration](#7--vmware-network-configuration)
8. [Windows 10 Static IP Configuration](#8--windows-10-static-ip-configuration)
9. [Connectivity Testing](#9--connectivity-testing)
10. [Troubleshooting](#10--troubleshooting)
11. [Screenshots and Evidence](#11--screenshots-and-evidence)
12. [Learning Outcomes](#12--learning-outcomes)
13. [Security Considerations and Disclaimer](#13--security-considerations-and-disclaimer)
14. [Conclusion](#14--conclusion)

---

## 1. 📌 Project Title and Overview

**Project:** Windows 10 Lab Setup (Week 1 – PMx Extra Project)
**Program:** NetworkWalks Cybersecurity Program · **Batch:** B084J · **Author:** Rajatava Ghosh

This is the extra project that follows my Week 1 **PM1 – Kali Linux lab**. In PM1 I built an isolated VMware lab with a Kali Linux security-testing machine on a custom NAT network (VMnet2). In this project I add a **Windows 10 virtual machine** to the same network as an **authorized target system**, give it a **static IP address**, and verify that it can talk to the gateway, to Kali Linux and to the internet.

> 🔗 **Related project:** [PM1 – Cybersecurity Lab Setup (Kali Linux + VMnet2)](https://github.com/Hypo46/NETWORKWALKS-B084J-WK1-PM1-CYBERSECURITY-LAB-SETUP)

> 📝 **Evidence policy:** Every result in this README is backed by a screenshot in this repository. Anything not yet proven is marked **TODO** or **verify** rather than claimed.

---

## 2. 🎯 Project Objectives

- ✅ Download a Windows 10 ISO from Microsoft's official download page.
- ✅ Create a Windows 10 x64 virtual machine in VMware Workstation.
- ✅ Install Windows 10 and complete first sign-in.
- ✅ Place the VM on the lab subnet `10.0.0.0/24` and assign the static IP `10.0.0.10`.
- ✅ Verify connectivity with `ipconfig` and `ping` (gateway, Kali Linux, internet and DNS).
- 📌 Document the setup so the Windows 10 VM can be reused as a target for authorized practice in later modules.

---

## 3. 🏗️ Lab Architecture

| Component | Role |
|---|---|
| 💻 **Host machine** | Windows 11 PC that runs VMware |
| 🖥️ **VMware Workstation** | Hypervisor hosting both virtual machines |
| 🪟 **Windows 10 VM** | Target machine for authorized cybersecurity practice (`10.0.0.10`) |
| 🐉 **Kali Linux VM** | Security-testing machine (`10.0.0.2`) |
| 🌐 **Custom NAT network (VMnet2)** | Shared lab network `10.0.0.0/24` with gateway `10.0.0.1` |

```text
┌────────────────────────────────────────────────────────────────────┐
│  Windows 11 Host  ·  VMware Workstation                            │
│                                                                    │
│  ┌──────────────────┐      ┌───────────────────────────┐           │
│  │ Kali Linux VM    │      │  VMnet2 (Custom NAT)      │           │
│  │ 10.0.0.2/24      ├─────►│  Subnet   10.0.0.0/24     │───────────┼──► Internet
│  │ (Security tester)│      │  Gateway  10.0.0.1        │           │
│  └──────────────────┘      │  DNS used by VMs: 8.8.8.8 │           │
│  ┌──────────────────┐      │                           │           │
│  │ Windows 10 VM    ├─────►│                           │           │
│  │ 10.0.0.10/24     │      └───────────────────────────┘           │
│  │ (Target machine) │                                              │
│  └──────────────────┘                                              │
└────────────────────────────────────────────────────────────────────┘
```

---

## 4. 🧰 Hardware and Software Requirements

| Category | Details |
|---|---|
| Host OS | Windows 11 |
| Hypervisor | VMware Workstation 17 (the screenshots show the Player edition; VM hardware version shown as `Workstation 17.x`) |
| Guest OS | Windows 10 x64, ISO from Microsoft (version shown on the download page: *Windows 10 2023 Update – Version 22H2*) |
| Security VM | Kali Linux (built in PM1) |
| Windows 10 VM resources (at creation) | 2 CPU cores · 4096 MB memory · 40 GB disk |
| VM storage location | `F:\Network Walks VM\Windows 10` |
| Browser | Used to download the ISO; browser developer tools were open on the download page |
| Host CPU / RAM / free disk | ⚠️ *Verify – not shown in screenshots* |

---

## 5. ⚙️ Lab Configuration Table

| Component | Configuration | Evidence |
|---|---|---|
| Host OS | Windows 11 | Project details |
| Virtualization | VMware Workstation 17 | Figure 3 |
| Guest OS | Windows 10 x64 (build `10.0.19045.2965`) | Figures 3, 6 |
| VM name | `Windows 10 x64` | Figure 3 |
| Virtual network | Custom NAT – VMnet2 | PM1 repo; adapter screenshot is a **TODO** for this VM |
| Network | `10.0.0.0/24` | Figure 6 |
| Gateway | `10.0.0.1` | Figure 6 |
| Windows 10 IP | `10.0.0.10` (static) | Figure 6 |
| Subnet mask | `255.255.255.0` | Figure 6 |
| DNS server | `8.8.8.8` (preferred) | Figure 6 |
| Kali Linux IP | `10.0.0.2` | PM1 repo; Figure 7 |
| Windows 10 network adapter | `Ethernet0` – Intel(R) 82574L Gigabit Network Connection | Figure 6 |
| Windows user profile | `NetworkWalks` | Figures 5, 6 |
| Windows 10 role | Target machine for authorized practice | Project details |
| Kali Linux role | Security-testing machine | Project details |

---

## 6. 🪟 Windows 10 VM Setup

### 6.1 Downloading or Preparing the Windows 10 ISO

The ISO was obtained from Microsoft's Windows 10 download page (`microsoft.com/en-in/software-download/windows10ISO`).

1. Open the Windows 10 ISO download page.
2. Under **Select edition**, choose **Windows 10 (multi-edition ISO)**.
3. Confirm and pick the product language. The next page shows **Windows 10 English International**.
4. Choose the **64-bit Download** (the VM was created as *Windows 10 x64*).

> ℹ️ The page explains that visitors on an operating system that does not support the Media Creation Tool are routed here to download a disc image (ISO) instead. In the screenshots the browser's developer tools are open in device-emulation mode on this page. ⚠️ *Verify this is the method you used before keeping this note.*
>
> ⏱️ Microsoft's download links are valid for **24 hours** after creation (the page in Figure 2 shows its expiry time), so download the ISO right away.

![Microsoft Windows 10 ISO download page showing Select edition: Windows 10 (multi-edition ISO), Version 22H2](images/01-windows10-iso-download-page.png)

*Figure 1 – `01-windows10-iso-download-page.png`: Microsoft's Windows 10 ISO page with "Windows 10 (multi-edition ISO)" selected under Select edition.*

![Microsoft download page offering Windows 10 English International 32-bit and 64-bit downloads, links valid for 24 hours](images/02-windows10-iso-download-links.png)

*Figure 2 – `02-windows10-iso-download-links.png`: Download links for Windows 10 English International (32-bit and 64-bit), valid for 24 hours.*

### 6.2 Creating the VM in VMware Workstation

The VM was created with the **New Virtual Machine Wizard**. The final "Ready to Create Virtual Machine" screen shows:

| Wizard setting | Value |
|---|---|
| Name | Windows 10 x64 |
| Location | `F:\Network Walks VM\Windows 10` |
| Version | Workstation 17.x |
| Operating System | Windows 10 x64 |
| Hard Disk | 40 GB |
| Memory | 4096 MB |
| Network Adapter | **NAT** (wizard default at creation) |
| Other Devices | 2 CPU cores, CD/DVD, USB Controller, Printer, Sound Card |
| Power on after creation | ✅ Enabled |

The wizard notes that finishing will **create the VM and start installing Windows 10 x64, then VMware Tools**.

> ⚠️ The adapter shows plain **NAT** at this stage. It is switched to the custom VMnet2 network in [Section 7](#7--vmware-network-configuration).

![VMware New Virtual Machine Wizard Ready to Create Virtual Machine screen for Windows 10 x64 with 40 GB disk and 4096 MB memory](images/03-vmware-new-vm-wizard-summary.png)

*Figure 3 – `03-vmware-new-vm-wizard-summary.png`: New Virtual Machine Wizard summary for the Windows 10 x64 VM.*

> 📌 **TODO – screenshot needed:** the wizard step where the Windows 10 ISO file is selected (not in the repository yet).

### 6.3 Installing Windows 10

After the VM powered on, the Windows 10 boot screen appeared and the installation continued until the first sign-in.

![Windows 10 boot screen with Windows logo and loading spinner inside the VM](images/04-windows10-boot-screen.png)

*Figure 4 – `04-windows10-boot-screen.png`: Windows 10 starting up inside the VMware VM.*

> ⚠️ **Verify / add:** Windows edition chosen (Home/Pro), installation type, and whether VMware Tools finished installing. These details are not shown in the screenshots, so they are not stated here.

### 6.4 Initial Configuration

The first sign-in screen shows the **NetworkWalks** user profile with the **Welcome** message while Windows prepares the desktop. The command prompts in later screenshots run as `C:\Users\NetworkWalks`.

![Windows 10 sign-in screen showing the NetworkWalks user and Welcome message](images/05-windows10-first-login-welcome.png)

*Figure 5 – `05-windows10-first-login-welcome.png`: First sign-in as the NetworkWalks user.*

---

## 7. 🌐 VMware Network Configuration

### 7.1 Custom VMnet2 NAT Network

The lab network was created in **PM1** and is reused unchanged here:

| Setting | Value |
|---|---|
| Network | vmnet2 (custom NAT) |
| Subnet IP / mask | `10.0.0.0` / `255.255.255.0` |
| Gateway IP | `10.0.0.1` |

See the PM1 repository for the VMnet2 NAT Settings screenshots.

### 7.2 Connecting Windows 10 to the Correct Virtual Network

Because the wizard created the VM with the default **NAT** adapter, the adapter must be attached to the custom network so that Windows 10 and Kali Linux share the same subnet:

1. Shut down the Windows 10 VM (or open its settings while it is powered off).
2. Open **Virtual Machine Settings → Hardware → Network Adapter**.
3. Select **Custom: Specific virtual network**.
4. Choose the VMnet2 network from the drop-down (shown as **Network Walls (NAT)** in the PM1 Kali VM settings).
5. Click **OK** and power the VM on.

> 📌 **TODO – screenshot needed:** the Windows 10 VM's *Network Adapter* settings showing the Custom VMnet2 selection. Until it is added, the evidence that the VM is on the lab network is indirect: it has an address in `10.0.0.0/24` and receives replies from `10.0.0.1` and `10.0.0.2` (Figures 6 and 7).
> `images/TODO-windows10-network-adapter-settings.png`

---

## 8. 🔢 Windows 10 Static IP Configuration

The static address was set in **Network Connections → Ethernet0 → Properties → Internet Protocol Version 4 (TCP/IPv4)**:

| Field | Value |
|---|---|
| Mode | **Use the following IP address** |
| IP address | `10.0.0.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.0.0.1` |
| DNS mode | **Use the following DNS server addresses** |
| Preferred DNS server | `8.8.8.8` |
| Alternative DNS server | *(empty)* |

**Steps (GUI):**

1. Press `Win + R`, type `ncpa.cpl` and press Enter.
2. Right-click **Ethernet0** → **Properties**.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**.
4. Enter the values from the table above and click **OK**.

**Optional equivalent from an Administrator Command Prompt** *(not shown in the screenshots; shown only for reference)*:

```cmd
netsh interface ip set address name="Ethernet0" static 10.0.0.10 255.255.255.0 10.0.0.1
netsh interface ip set dns name="Ethernet0" static 8.8.8.8
```

![Windows 10 Command Prompt showing ipconfig output and ping to 10.0.0.2 beside the Ethernet0 IPv4 properties dialog with 10.0.0.10, 255.255.255.0, 10.0.0.1 and DNS 8.8.8.8](images/06-windows10-static-ip-and-ipconfig.png)

*Figure 6 – `06-windows10-static-ip-and-ipconfig.png`: Static IPv4 settings for Ethernet0 and the matching `ipconfig` output. A ping to Kali (`10.0.0.2`) is also visible.*

---

## 9. ✅ Connectivity Testing

All commands below were run in **Command Prompt** on the Windows 10 VM.

```cmd
ipconfig
ping 10.0.0.1
ping 10.0.0.2
ping networkwalks.com
```

| # | Command | What it verifies | Result | Evidence |
|---|---|---|---|---|
| 1 | `ipconfig` | Static settings applied to `Ethernet0` | ✅ IPv4 `10.0.0.10`, mask `255.255.255.0`, gateway `10.0.0.1` | Figure 6 |
| 2 | `ping 10.0.0.1` | Reachability of the VMnet2 NAT gateway | ✅ 4 sent, 4 received, 0% loss (< 1 ms) | Figure 7 |
| 3 | `ping 10.0.0.2` | Windows 10 → Kali Linux communication | ✅ 4 sent, 4 received, 0% loss, avg 1 ms (TTL=64). An earlier run in Figure 6 stopped with Ctrl+C after 3 of 3 replies | Figures 6, 7 |
| 4 | `ping networkwalks.com` | DNS resolution + internet access | ✅ Resolved to `192.232.216.135`; 4 sent, 4 received, 0% loss, avg 287 ms | Figure 7 |
| 5 | `ping 8.8.8.8` | Internet reachability without DNS | 📝 Not captured – **TODO** | – |
| 6 | `nslookup networkwalks.com` | DNS lookup through `8.8.8.8` | 📝 Not captured – **TODO** (optional) | – |
| 7 | **From Kali:** `ping -c 4 10.0.0.10` | Kali Linux → Windows 10 communication | 📝 Not tested yet – **TODO** (see [Troubleshooting](#10--troubleshooting) for the Windows Firewall) | – |

**Reading the results**

- Replies from `10.0.0.1` and from `networkwalks.com` show **TTL=128**, the default for Windows-style replies, while replies from `10.0.0.2` show **TTL=64**, the default for a Linux host such as Kali.
- A successful `ping networkwalks.com` proves both **DNS resolution** and **outbound internet access** from the Windows 10 VM, so the `8.8.8.8` DNS setting is working.
- Only the **Windows 10 → Kali** direction was tested. Do not assume the reverse direction works until row 7 is run.

![Windows 10 Command Prompt with ping results for 10.0.0.2, 10.0.0.1 and networkwalks.com all showing 0% packet loss](images/07-windows10-connectivity-tests.png)

*Figure 7 – `07-windows10-connectivity-tests.png`: Ping tests to Kali Linux (`10.0.0.2`), the gateway (`10.0.0.1`) and `networkwalks.com`, all with 0% loss.*

> 📌 **TODO – screenshots needed:** `ping 8.8.8.8` from Windows 10, and `ping -c 4 10.0.0.10` from Kali Linux.

---

## 10. 🛠️ Troubleshooting

### Issues seen during this lab

| # | Symptom | Cause | Fix |
|---|---|---|---|
| 1 | `ping -c 4 google.com` → *"Access denied. Option -c requires administrative privileges."* | `-c` is the **Linux** count option. In Windows `ping`, `-c` means something else and needs admin rights | On Windows use `-n`: `ping -n 4 google.com` |
| 2 | Typing only `10.0.0.2` → *"'10.0.0.2' is not recognized as an internal or external command"* | An IP address alone is not a command | Run `ping 10.0.0.2` |

### Common problems for this setup

| Problem | How to check | Fix |
|---|---|---|
| 🔥 **Windows Firewall blocks ICMP ping** (Kali cannot ping Windows 10 even though Windows can ping Kali) | Run `ping 10.0.0.10` from Kali; "Request timed out"-style failures while Windows 10 itself has network access | In this isolated lab only, allow inbound ICMPv4 echo from an Administrator Command Prompt: `netsh advfirewall firewall add rule name="Allow ICMPv4-In (Lab)" protocol=icmpv4:8,any dir=in action=allow` and remove it later if you don't need it |
| 🔌 **Incorrect VM network adapter** (NAT/Bridged instead of VMnet2) | Check **VM Settings → Network Adapter**; Windows cannot reach `10.0.0.1` or Kali | Select **Custom: Specific virtual network** and choose the VMnet2 network |
| 🔢 **IP address or gateway errors** | Run `ipconfig` and compare with the table in Section 8 | Correct `10.0.0.10`, `255.255.255.0` and `10.0.0.1`; make sure no other VM uses the same IP |
| 🌐 **Internet or DNS not working** | `ping 8.8.8.8` works but `ping networkwalks.com` fails → DNS problem; both fail → gateway/NAT problem | Re-enter DNS `8.8.8.8`; confirm the gateway replies; check the VMnet2 NAT settings in VMware |

---

## 11. 📸 Screenshots and Evidence

| Fig. | File | What it shows | Section |
|---|---|---|---|
| 1 | `images/01-windows10-iso-download-page.png` | Windows 10 ISO page, multi-edition ISO selected | 6.1 |
| 2 | `images/02-windows10-iso-download-links.png` | 32-bit / 64-bit download links, 24-hour validity | 6.1 |
| 3 | `images/03-vmware-new-vm-wizard-summary.png` | VM creation summary (40 GB, 4096 MB, 2 cores, NAT) | 6.2 |
| 4 | `images/04-windows10-boot-screen.png` | Windows 10 booting | 6.3 |
| 5 | `images/05-windows10-first-login-welcome.png` | First sign-in as NetworkWalks | 6.4 |
| 6 | `images/06-windows10-static-ip-and-ipconfig.png` | Static IPv4 dialog + `ipconfig` + ping to Kali | 8 |
| 7 | `images/07-windows10-connectivity-tests.png` | Pings to Kali, gateway and `networkwalks.com` | 9 |

**Still to add (TODO):**

- [ ] Wizard step selecting the Windows 10 ISO
- [ ] Windows 10 VM → Network Adapter set to the custom VMnet2 network
- [ ] `ping 8.8.8.8` from Windows 10
- [ ] `ping -c 4 10.0.0.10` from Kali Linux

---

## 12. 🧠 Learning Outcomes

- Preparing a Windows 10 ISO and creating a Windows 10 x64 VM with VMware's New Virtual Machine Wizard.
- Understanding why a VM created on the default **NAT** adapter must be moved onto the custom **VMnet2** network to share a subnet with Kali Linux.
- Configuring a **static IPv4 address, mask, gateway and DNS** on Windows 10 and confirming it with `ipconfig`.
- Using `ping` to test layer-3 connectivity step by step: gateway → other VM → internet/DNS.
- Recognizing OS differences in tools: Windows `ping -n` vs Linux `ping -c`, and TTL 128 vs 64.
- Understanding that a successful ping in one direction does not prove the other direction, because host firewalls can block ICMP.

---

## 13. 🔐 Security Considerations and Disclaimer

> ⚠️ **This is an educational lab. Use it only for authorized security testing.**

- ✅ The Windows 10 VM is a **target machine for authorized practice** inside a private lab network that I own and control.
- ❌ Do not use any tool or technique practiced in this lab against systems, networks or people without **explicit written permission**.
- 🕰️ **Windows 10 is no longer supported with regular security updates by Microsoft.** The download page itself encourages upgrading to Windows 11. Treat this VM as intentionally exposed practice equipment: keep it on the isolated VMnet2 network, do not store personal data or real credentials on it, and do not bridge it to a real network.
- 🔥 If the Windows Firewall is relaxed to allow ping, do so only for lab testing and re-enable the stricter setting afterwards.
- 🧹 Blur or crop personal information (browser bookmarks, profile pictures, account names) before publishing screenshots.
- 📚 This repository is for learning and documentation only. The author accepts no responsibility for misuse.

---

## 14. 🏁 Conclusion

The Windows 10 virtual machine was created in VMware Workstation, given the static address `10.0.0.10/24` with gateway `10.0.0.1` and DNS `8.8.8.8`, and verified from Command Prompt. It reaches the VMnet2 gateway, Kali Linux (`10.0.0.2`) and the internet, including DNS resolution of `networkwalks.com`.

The lab now has both a security-testing machine (Kali Linux) and a target machine (Windows 10) on the same controlled network. Remaining checks, the Kali → Windows ping and the VM adapter screenshot, are listed as TODO items above and will be added as evidence in this repository.

---

<div align="center">

### 👤 Rajatava Ghosh

🎓 Cybersecurity Intern – NetworkWalks Cybersecurity Program, Batch B084J

[![GitHub](https://img.shields.io/badge/GitHub-RaxingR-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/RaxingR)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Rajatava_Ghosh-0A66C2?style=for-the-badge)](https://www.linkedin.com/in/rajatava-ghosh-265aa6316/)

**⭐ Built for learning. Practiced ethically. ⭐**

*Week 1 · PMx Extra Project · NetworkWalks Cybersecurity Internship*

</div>
