# 🛠️ 01 - Azure Setup and VM Configuration (GUI-Based)

This guide walks you through the GUI-based setup of a SOC lab using Microsoft Sentinel and Palo Alto firewall logs. It is written for beginners who are building their first threat detection lab.

---

## 🎯 Objective

We will create:
- A Resource Group
- A Log Analytics Workspace (LAW)
- A Microsoft Sentinel instance
- A Virtual Network (VNet)
- One Linux VM (Syslog Gateway for CEF)
- One Windows VM (for simulated attacks)

---

## ✅ Step 1: Create Resource Group

1. Go to the [Azure Portal](https://portal.azure.com)
2. In the top search bar, search for **"Resource Groups"**
3. Click **+ Create**
4. Enter:
   - **Subscription**: Free Trial / Pay-As-You-Go
   - **Resource Group Name**: `SOC-PA-Sentinel-RG`
   - **Region**: East US (or closest region)
5. Click **Review + Create** → **Create**

📸 *[Insert Screenshot: Resource Group Creation]*

---

## ✅ Step 2: Create Log Analytics Workspace (LAW)

1. In Azure Portal, search for **"Log Analytics workspaces"**
2. Click **+ Create**
3. Fill:
   - **Resource Group**: `SOC-PA-Sentinel-RG`
   - **Name**: `SOC-LAW`
   - **Region**: East US
4. Click **Review + Create** → **Create**

📸 *[Insert Screenshot: LAW creation]*

---

## ✅ Step 3: Enable Microsoft Sentinel

1. Search for **Microsoft Sentinel**
2. Click **+ Add**
3. Choose workspace: `SOC-LAW`
4. Click **Add Microsoft Sentinel**

📸 *[Insert Screenshot: Sentinel attached to workspace]*

---

## ✅ Step 4: Create Virtual Network (VNet)

1. Search for **Virtual Networks** → **+ Create**
2. Enter:
   - **Name**: `SOC-VNET`
   - **Address Space**: `10.0.0.0/16`
   - **Subnet Name**: `SOC-Subnet`
   - **Subnet Address Range**: `10.0.1.0/24`
   - **Resource Group**: `SOC-PA-Sentinel-RG`
3. Click **Review + Create** → **Create**

📸 *[Insert Screenshot: VNet creation]*

---

## ✅ Step 5: Create Linux VM (Syslog Gateway)

1. Search for **Virtual Machines** → **+ Create**
2. Configure:
   - **Name**: `Syslog-Gateway-VM`
   - **Region**: East US
   - **Image**: Ubuntu 22.04 LTS
   - **Size**: B1s or B2s
   - **Username**: `azureuser`
   - **Authentication**: Password or SSH
   - **VNet**: `SOC-VNET`, Subnet: `SOC-Subnet`
3. Under **Inbound Ports**, select: Allow all (lab only)
4. Click **Review + Create** → **Create**

📸 *[Insert Screenshot: Linux VM config]*

---

## ✅ Step 6: Create Windows VM (For Attacks)

1. Go to **Virtual Machines** → **+ Create**
2. Configure:
   - **Name**: `Windows-Attacker-VM`
   - **Region**: East US
   - **Image**: Windows Server 2022
   - **Username/Password**
   - **VNet/Subnet**: Same as above
   - **Size**: B2s or higher
3. Allow RDP (3389) in inbound ports
4. Click **Review + Create** → **Create**

📸 *[Insert Screenshot: Windows VM config]*

---

## ✅ Step 7: Verify Everything

- Go to **Resource Group** → You should see:
   - `SOC-VNET`
   - `SOC-LAW`
   - 2 VMs
   - Microsoft Sentinel linked

📸 *[Insert Screenshot: Resource Group Overview]*

---

## ✅ Next Steps:

➡️ Go to: **02-AMA-CEF-Syslog-Setup.md**  
We’ll now configure:
- CEF logging on Linux
- Palo Alto log forwarding
- AMA and DCR

---

## 🙌 Author

**Deepak Vishwakarma**  
> A cybersecurity enthusiast documenting hands-on SOC projects to help beginners get started.

