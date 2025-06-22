# 🔧 03 - Configure Palo Alto Firewall to Forward Logs in CEF Format

To ingest logs into Microsoft Sentinel via a Linux syslog gateway, Palo Alto must be configured to forward logs in **CEF (Common Event Format)** via Syslog.

---

## 📍 Step 1: Create Syslog Server Profile

1. Log in to Palo Alto Web UI
2. Navigate to:
   - **Device → Server Profiles → Syslog**
3. Click **Add**
4. Configure: Servers
   - **Name**: `sento-logs`
   - **Syslog Server**: IP address of your Linux VM (Syslog Gateway)
   - **Transport**: UDP or TCP (must match your Linux config)
   - **Port**: `514`
   - **Format**: **BSD (Use CEF format)**
5. Configure: Custom Log Format
   - Click And And Manually add CEF format From
     `https://github.com/pemontto/Palo-Alto-CEF/tree/master/9.1`
    ![cef-pal1](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/11.palo%20alto%20config/cef-pal1.png)

    ![cef-pal2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/11.palo%20alto%20config/cef-pal2.png)


✅ Click **OK** and **Commit** changes

--

## 📍 Step 2: Create Log Forwarding Profile

1. Go to:
   - **Objects → Log Forwarding**
2. Click **Add**
3. **Name** it: `logs-senti`
4. Under **Log Settings** (e.g., Traffic, Threat, System):
   - Click **Add** under each
   - Enable forwarding to your **Syslog Profile (`senti-logs`)**
   - Optionally filter logs (e.g., only critical or all)

✅ Click **OK** and **Commit** changes

![cef-pal3](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/11.palo%20alto%20config/cef-pal3.png)

---

## 📍 Step 3: Apply Log Forwarding to Security Policies

1. Go to:
   - **Policies → Security**
2. Edit your active allow/deny rules
3. Under **Actions → Log Forwarding**, select: `log-senti`
4. Apply to:
   - Threat Prevention logs (Intrusion, Virus, etc.)
   - Traffic logs (session start/end)
   - URL filtering logs

✅ Click **OK** and **Commit** your policies

![cef-pal4](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/11.palo%20alto%20config/cef-pal4.png)

---

## 🧪 Verification

After configuration:

- SSH into your Linux Syslog VM
- Capture messages sent from a logger or a connected device, run this command in the background:
  ```tcpdump -i any port 514 -A -vv &```
- Go to **Sentinel → Search → KQL Mode:**
 ```CommonSecurityLogs```
- 

![verify-senti](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/11.palo%20alto%20config/verify-senti.png)

![veri2](https://github.com/Deevish895/SOC-lab-in-Microsoft-Sentinel-on-free-tier/blob/main/Setup-Steps/setup-images/11.palo%20alto%20config/veri2.png)


