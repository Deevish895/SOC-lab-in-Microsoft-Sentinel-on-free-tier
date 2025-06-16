# 🛡️ 03 - Sentinel Connectors, Analytics Rules, and Workbooks

Now that logs from Palo Alto are successfully reaching Sentinel, it’s time to configure **correlation rules**, enable **normalization via ASIM**, and build **visual dashboards** to monitor and alert.

---

## 🧠 What We’ll Cover

1. Enable **ASIM normalization**
2. Activate built-in **Analytics Rules**
3. View & understand **incidents**
4. Set up **Workbooks** (dashboards)
5. Simulate logs to **trigger alerts**

---

## 🔌 Step 1: Enable ASIM Parsers (Normalization)

ASIM (Advanced Security Information Model) helps Sentinel normalize logs for use in detection rules and queries.

### ✅ Check if ASIM Parser is Installed

1. Go to **Sentinel → Content Hub**
2. Search: `ASIM - Palo Alto`
3. If not installed, click **Install**
4. Confirm you see:
   - `ASimNetworkSession`
   - `ASimAuthentication`
   - Other parsers for Palo Alto

These will parse logs into a standard schema like:

```kql
imNetworkSession
| where EventVendor == "Palo Alto Networks"
