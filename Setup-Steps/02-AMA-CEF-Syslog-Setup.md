# 🖥️ 02 - Linux Syslog Gateway + AMA + Sentinel Connectors (Beginner GUI Flow)

This guide reflects a **realistic, GUI-based configuration** of a SOC lab where Palo Alto firewall logs are ingested into Microsoft Sentinel using:

- **Linux VM** as Syslog receiver
- **Azure Monitor Agent (AMA)**
- **Data Collection Rules (DCR)** from the Sentinel connector blade
- **Content Hub** and **Connector configuration**
- **No manual rule creation or CLI DCR deployment**

---

## 🔗 Reference Flow You Followed

This setup closely follows a beginner-friendly and GUI-based approach:

1. Installed Palo Alto solution from **Sentinel Content Hub**
2. Used **Manage** on the connector page to configure AMA and DCR
3. Used official Microsoft script to configure syslog receiver (CEF)
4. Allowed inbound Syslog ports
5. Configured Palo Alto firewall to forward logs to the Linux gateway
6. Verified data ingestion in Sentinel via KQL

---

## ✅ Step-by-Step Configuration

---

### 🟢 Step 1: Install Palo Alto Solution via Content Hub

1. Go to **Microsoft Sentinel → Content hub**
2. Search for **"Palo Alto Networks (CEF)"**
3. Click **Install**
4. After installation, click **Manage Content**

---

### 🟢 Step 2: Open Palo Alto CEF Connector

1. Go to **Microsoft Sentinel → Data connectors**
2. Search and open: **Palo Alto Networks (CEF)**
3. Click **Open connector page**

---

### 🟢 Step 3: Install Azure Monitor Agent (AMA)

1. On the connector page, under **Instructions**, click **Install agent**
2. Select your **Linux VM (Syslog Gateway)**
3. Click **Install**

✅ AMA will be deployed automatically via Azure backend

---

### 🟢 Step 4: Create DCR (Data Collection Rule)

1. On the same connector page, click **Add data collection rule**
2. Fill the fields:
   - Facility: `local4`
   - Severity: All (Info, Notice, Warning, etc.)
   - Scope: your **Linux Syslog VM**
   - Destination: your **Log Analytics workspace**

✅ This configures which logs AMA will route to Sentinel

---

### 🟢 Step 5: Configure Linux Syslog Receiver (CEF Format)

On your Linux VM (via SSH or Azure Bastion), run the official Microsoft script:

```bash
curl -s https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Forwarder_AMA_installer.py | sudo python3
```



---

### 🟢 Step 6: Allow Syslog Traffic on Port 514

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
