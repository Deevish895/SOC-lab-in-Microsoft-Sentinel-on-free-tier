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
   - **Name**: `SOC-VNET`
   - **Address Space**: `10.0.0.0/16`
   - **Subnet Name**: `SOC-Subnet`
   - **Subnet Address Range**: `10.0.1.0/24`
   - **Resource Group**: `SOC-PA-Sentinel-RG`
3. Click **Review + Create** → **Create**

📸 *[Insert Screenshot: VNet creation]*

![vnet1](https://github.com/user-attachments/assets/ca7f2894-06c2-4a49-a4f2-f4697dab7521)

![vnet2](https://github.com/user-attachments/assets/3a8eda16-6714-4c8a-835a-44677e261443)

![vnet3](https://github.com/user-attachments/assets/2c956ed0-32ed-44bf-928d-1610924fd83d)

![vnet4](https://github.com/user-attachments/assets/1620a830-8a49-4900-83ed-3f4a827cbff5)

![vnet5](https://github.com/user-attachments/assets/a39dcf42-1c8e-4491-8a2e-464112705ef7)

![vnet6](https://github.com/user-attachments/assets/95ff2fc7-8c72-4885-b98d-ff62bc6ac0d8)


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

![vmlin1](https://github.com/user-attachments/assets/1f551cbd-22e0-4079-889c-e5ce388f219d)

![vmlin2](https://github.com/user-attachments/assets/269376d0-7bed-4386-b961-cfe24ad90109)

![vmlin3](https://github.com/user-attachments/assets/029b07ca-1dc4-4ddf-9c01-d4b165b24593)

![vmlin4](https://github.com/user-attachments/assets/de556a1c-4df5-4d8e-aa33-ec78745e8bda)

![vmlin5](https://github.com/user-attachments/assets/89835d93-a3f2-48f4-928d-35dda18fde24)

![vmlin6](https://github.com/user-attachments/assets/04a145bb-6182-4070-898d-fa19b0289593)

![vmlin7](https://github.com/user-attachments/assets/acef1c19-e3a2-4a78-b1c6-99fd4e571f97)

![vmlin8](https://github.com/user-attachments/assets/d07b7f8b-98cd-4b72-aeb4-c354dcc7b741)

![vmlin9](https://github.com/user-attachments/assets/97d6ba9a-9e23-4aaa-a8db-ec40705474e2)

![vmlin10](https://github.com/user-attachments/assets/f327e44a-fbfa-4158-96b0-76d6a97b23cd)

![vmlin11](https://github.com/user-attachments/assets/db0089a4-323e-4f02-a94f-eef43cbd1c36)

![lin1](https://github.com/user-attachments/assets/ad6a405a-32dd-4c73-be75-b9e0d858eaec)

![lin2](https://github.com/user-attachments/assets/d2f28691-d211-454a-a266-a29f568e7f0a)



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

