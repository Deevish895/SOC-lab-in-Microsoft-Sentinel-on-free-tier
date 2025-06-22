# 🖥️ 02 - Linux Syslog Gateway + AMA + Sentinel Connectors (Beginner GUI Flow)

This guide reflects a **realistic, GUI-based configuration** of a SOC lab where Palo Alto firewall logs are ingested into Microsoft Sentinel using:

- **Linux VM** as Syslog receiver
- **Azure Monitor Agent (AMA)**
- **Data Collection Rules (DCR)** from the Sentinel connector blade
- **Content Hub** and **Connector configuration**
- **No manual rule creation or CLI DCR deployment**

---

# 🔌 **Understanding Sentinel Connectors & Data Collection Rules (DCR)**

In this SOC lab, we used **two different connectors** on the **Linux syslog gateway** to ingest and parse CEF-formatted logs from a Palo Alto Firewall into Microsoft Sentinel.

---

## 🔹 Setup Overview

| Component            | What You Did |
|----------------------|---------------|
| Syslog Connector     | Used for ingesting logs via AMA |
| CEF Connector        | Used for parsing CEF-formatted Palo Alto logs |
| rsyslog on Linux     | Configured to receive logs on port 514 from Palo Alto |
| AMA Agent            | Installed on Linux to forward data to Sentinel |
| Data Collection Rules| Created for both connectors using GUI |

---

## 🔹 Why Two Connectors?

- **Syslog Connector via AMA** collects raw syslog messages from Linux (general logging)
- **Common Event Format (CEF) Connector via AMA** specifically parses CEF messages from Palo Alto
- Each requires a **separate DCR**
- Both run **on the same Linux VM**

---

## 🛠️ Step-by-Step Configuration

### ✅ Step 1: Install Syslog Connector

- Go to **Microsoft Sentinel → Content Hub → Search → Syslog → Install**

✅ AMA gets installed on the VM

 ![con1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/1.Configure%20Syslog%20Connector/con1.png)

 ![con2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/1.Configure%20Syslog%20Connector/con2.png)

 ![con3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/1.Configure%20Syslog%20Connector/con3.png)

 ![con4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/1.Configure%20Syslog%20Connector/con4.png)
 
---

### ✅ Step 2: Configure **Syslog Connector + DCR**
- Go to Data Collection Rule
- Click **+ Create data collection rule**
- Scope: Linux VM
- Severity: All
- Facility: You can leave default (or add if customized)
- Destination: Log Analytics Workspace

#Verify the AMA Agent 
- Go to Virtual Machine → Select Machine → Setting → Extension + application → You will see: **AMA Agent**

#Verify the The Syslogs of Linux In the Sentinel
- Go to **Sentinel → Logs → KQL Mode**
- Search ```Syslog```

✅ This DCR enables raw syslog ingestion (for Linux monitoring or general logs)

 ![dcr1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr1.png)

 ![dcr2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr2.png)

 ![dcr3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr3.png)

 ![dcr4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr4.png)

 ![dcr5](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr5.png)

 ![dcr6](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr6.png)

 ![dcr7](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr7.png)

 ![dcr8](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr8.png)

 ![dcr9](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr9.png)

 ![dcr10](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcr10.png)

 ![dcrverifify](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/dcrverifify.png)

 ![log-verify](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/07.Syslog/2.Configure%20Data%20Collection%20Rule/log%20verify.png)


---

### ✅ Step 3: Configure **CEF Connector + DCR**

- Go to ** Sentinel → Data Connectors → Common Event Format → Manage → Common Event Format(CEF) via AMA → Open Connector Page**
- Open connector page
- Select same **Linux VM**
- Click **+ Create data collection rule**
- Scope: Linux VM
- Destination: Log Analytics Workspace

**After Completing these steps Verify On Linux Machine: There you will see 2 jason file 1 for syslog DCR and 2nd for CEF DCR in which the DCR rule Id will be available** 

```sudo -i
   cd /etc/opt/microsoft/azuremonitoragent/config-cache/configchunks/
   ls
```

✅ This DCR enables parsing of CEF logs from Palo Alto (sent over syslog)

 ![cef-con1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![cef-con2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![cef-con3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![cef-con4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![cef-con5](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![cef-con6](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![cef-con7](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![cef-con8](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

![DCR-verify-on-linux](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/08.Configure%20CEF%20Connector%20And%20DCR/cef-con1.png).

  

---


### ✅ Step 4: Configure **Log Forwarder On Linux**

- Go to ** Sentinel → Data Connectors → Common Event Format → Manage → Common Event Format(CEF) via AMA → Open Connector Page**
- Open connector page
- Select same **Linux VM**
- Click **+ Create data collection rule**
- Scope: Linux VM
- Destination: Log Analytics Workspace


---


### ✅ Step 4: Configure **rsyslog on Linux**

1. SSH into your Linux VM  
2. Edit `/etc/rsyslog.conf` or `/etc/rsyslog.d/99-cef.conf`  
3. Add listener configuration (TCP or UDP):

```bash
# For TCP
module(load="imtcp")
input(type="imtcp" port="514")

# Or for UDP
module(load="imudp")
input(type="imudp" port="514")












---

### 🟢 Step 5: Configure Linux Syslog Receiver (CEF Format)

On your Linux VM (via SSH or Azure Bastion), run the official Microsoft script:

```bash
curl -s https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py | sudo python3
```



---

### 🟢 Step 6: Allow Syslog Traffic on Port 514 In NSG

#### In Azure:

- Go to your Linux VM → **Networking → Inbound Port Rules**
- Add rule:
  - Protocol: TCP & UDP
  - Port: 514
  - Priority: lower than deny rules
  - Action: Allow

#### In Linux VM:

```bash
sudo ufw allow 514/tcp
sudo ufw allow 514/udp
```
