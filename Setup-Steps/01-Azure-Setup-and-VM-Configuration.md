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
   - **Resource Group Name**: `Home-Soc`
   - **Region**: East US (or closest region)
5. Click **Review + Create** → **Create**

📸 *[Demonstrated Screenshots]*

![1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/01.Create%20Resource%20Group/1.png)

![2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/01.Create%20Resource%20Group/2.png)

![3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/01.Create%20Resource%20Group/3.png)

![4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/01.Create%20Resource%20Group/4.png)

![5](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/01.Create%20Resource%20Group/5.png)

![6](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/01.Create%20Resource%20Group/6.png)

![7](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/01.Create%20Resource%20Group/7.png)







---

## ✅ Step 2: Create Log Analytics Workspace (LAW)

1. In Azure Portal, search for **"Log Analytics workspaces"**
2. Click **+ Create**
3. Fill:
   - **Resource Group**: `Home-Soc`
   - **Name**: `HomeSoc-Logspace`
   - **Region**: East US
4. Click **Review + Create** → **Create**

📸 *[Demonstrated Screenshots]*

![8](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/02.Configure%20Log%20Analytic%20Workspace/8.png)

![9](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/02.Configure%20Log%20Analytic%20Workspace/9.png)

![10](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/02.Configure%20Log%20Analytic%20Workspace/10.png)

![11](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/02.Configure%20Log%20Analytic%20Workspace/11.png)

---

## ✅ Step 3: Enable Microsoft Sentinel

1. Search for **Microsoft Sentinel**
2. Click **+ Create**
3. Choose workspace: `HomeSoc-Logspace`
4. Click **Add Microsoft Sentinel**

📸 *[Demonstrated Sceernshots for Enabling Sentinel]*

   ![sent1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/03.Configure%20Sentinel/sent1.png)

   ![sent2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/03.Configure%20Sentinel/sent2.png)

   ![sent3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/03.Configure%20Sentinel/sent3.png)

   ![sent4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/03.Configure%20Sentinel/sent4.png)

   


---

## ✅ Step 4: Create Virtual Network (VNet)

1. Search for **Virtual Networks** → **+ Create**
2. Enter:
   - **VIrtual Network Name**: `HomeSocVnet`
   - **Address Space**: `Default 10.0.0.0/16`
   - **Subnet Name**: `SOC-Subnet`
   - **Subnet Address Range**: `10.0.1.0/24`
   - **Resource Group**: `Home-Soc`
3. Click **Review + Create** → **Create**

📸 *[Insert Screenshot: VNet creation]*

![vnet1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/04.Configure%20Virtual%20Network/vnet1.png)

![vnet2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/04.Configure%20Virtual%20Network/vnet2.png)

![vnet3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/04.Configure%20Virtual%20Network/vnet3.png)

![vnet4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/04.Configure%20Virtual%20Network/vnet4.png)

![vnet5](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/04.Configure%20Virtual%20Network/vnet5.png)

![vnet6](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/04.Configure%20Virtual%20Network/vnet6.png)


---

## ✅ Step 5: Create Linux VM (Syslog Gateway)

1. Search for **Virtual Machines** → **+ Create**
2. Configure:
   - **Virtual Machine Name**: `Linux-CEF`
   - **Resource Group**: Select `Home-Soc`
   - **Region**: East US
   - **Image**: Ubuntu 22.04 LTS
   - **Size**: B1s or B2s
   - **Authentication**: Password
   - **Username**: `azureuser`
4.  Under **Disk**:
   - **Os Disk Size **: As per your need I chose Default
   - **OS Disk Type**: Select Premium
   - **Select**: Delete With VM
5.  Under **Networking**:
   - **Virtual Network**: Select That we created `HomeSocVnet`
   - ** Subnet**: `Default`
   - **Select**: Delete With VM
   -  Under **Inbound Ports**, select: Allow all or We will configure in NSG part (lab only)
6. Click **Review + Create** → **Create**
7. Verify Your Public IP and take SSH

📸 *[Linux VM config]*

![vmlin1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin1.png)

![vmlin2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin2.png)

![vmlin3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin3.png)

![vmlin4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin4.png)

![vmlin5](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin5.png)

![vmlin6](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin6.png)

![vmlin7](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin7.png)

![vmlin8](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin8.png)

![vmlin9](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlin9.png)

![vmlin10](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlinVerify.png)

![vmlin11](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/06.Configure%20Linux%20VM/vmlinVerify2.png)




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
![1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/05.Configure%20Windows%20VM/vm1.png)
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

