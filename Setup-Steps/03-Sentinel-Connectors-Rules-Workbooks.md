# 🔧 02a - Configure Palo Alto Firewall to Forward Logs in CEF Format

To ingest logs into Microsoft Sentinel via a Linux syslog gateway, Palo Alto must be configured to forward logs in **CEF (Common Event Format)** via Syslog.

---

## 📍 Step 1: Create Syslog Server Profile

1. Log in to Palo Alto Web UI
2. Navigate to:
   - **Device → Server Profiles → Syslog**
3. Click **Add**
4. Configure: Servers
   - **Name**: `Sentinel-CEF`
   - **Syslog Server**: IP address of your Linux VM (Syslog Gateway)
   - **Transport**: UDP or TCP (must match your Linux config)
   - **Port**: `514`
   - **Format**: **BSD (Use CEF format)**
5. Configure: Custom Log Format
   - Click And And Manually add CEF format From
      

✅ Click **OK** and **Commit** changes

---

## 📍 Step 2: Create Log Forwarding Profile

1. Go to:
   - **Objects → Log Forwarding**
2. Click **Add**
3. **Name** it: `CEF-Forwarding`
4. Under **Log Settings** (e.g., Traffic, Threat, System):
   - Click **Add** under each
   - Enable forwarding to your **Syslog Profile (`Sentinel-CEF`)**
   - Optionally filter logs (e.g., only critical or all)

✅ Click **OK** and **Commit** changes

---

## 📍 Step 3: Apply Log Forwarding to Security Policies

1. Go to:
   - **Policies → Security**
2. Edit your active allow/deny rules
3. Under **Actions → Log Forwarding**, select: `CEF-Forwarding`
4. Apply to:
   - Threat Prevention logs (Intrusion, Virus, etc.)
   - Traffic logs (session start/end)
   - URL filtering logs

✅ Click **OK** and **Commit** your policies

---

## 🧪 Verification

After configuration:

- SSH into your Linux Syslog VM
- Run:



