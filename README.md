# 🛡️ SOC Showcase: Palo Alto Logs to Microsoft Sentinel (2025)

> A beginner-friendly Security Operations Center (SOC) lab setup using **Palo Alto firewall**, **Linux Syslog Gateway**, and **Microsoft Sentinel** in Azure.  
> This guide is built entirely using the **GUI (no scripting required)**, with screenshots, simple steps, and real log ingestion to help anyone from student to professional get hands-on with SIEM.

---

## 📚 Lab Overview

| Component        | Purpose                                  |
|------------------|------------------------------------------|
| Azure VMs        | One Linux (Syslog) + One Windows (Attack) |
| Palo Alto Logs   | Logs sent in CEF format to Syslog Gateway |
| Microsoft Sentinel | Used for log ingestion, detection, workbook, rules |
| AMA + DCR        | Azure Monitoring Agent for log forwarding |
| ASIM             | Used for normalization and KQL queries    |

---

## 🔨 Technologies Used

- Microsoft Azure
- Microsoft Sentinel
- Log Analytics Workspace (LAW)
- Azure Monitor Agent (AMA)
- Palo Alto Firewall (Syslog in CEF format)
- Linux Ubuntu (Syslog Gateway)
- Windows Server VM (for simulated attacks)

---

## 📂 Project Structure

SOC-Showcase-PA-Sentinel-2025/
├── README.md
├── Setup-Steps/
│ ├── 01-Azure-Setup-and-VM-Configuration.md
│ ├── 02-AMA-CEF-Syslog-Setup.md
│ ├── 03-Sentinel-Connectors-Rules-Workbooks.md
├── Attack-Simulation/
│ ├── Simulation-1-BruteForce-WindowsVM.md
├── Screenshots/
│ └── *.png (Add screenshots here)





---

## 🔗 Setup Steps

| Step | File |
|------|------|
| ✅ Azure Setup, VMs, Sentinel | [`01-Azure-Setup-and-VM-Configuration`](./Setup-Steps/01-Azure-Setup-and-VM-Configuration.md) |
| ✅ AMA, CEF, Palo Config      | Coming soon |
| ✅ Sentinel Rules & Dashboards | Coming soon |
| 🚧 Simulated Attacks          | Coming soon |

---

## 🧠 Who Should Use This?

- 🎓 Cybersecurity Students
- 💼 SOC Analyst Trainees
- 🧪 Threat Detection Learners
- 🧰 Anyone new to Microsoft Sentinel or Palo Alto logging

---

## 🙌 Maintained by

**Deepak Vishwakarma**  
📍 India | 🎓 BSc IT | 🛡️ CEH | 🖥️ Cybersecurity Intern  
🔗 [LinkedIn ](https://linkedin.com/in/deepak-vish)  
✉️ vishwakarmadeepak2111@gmail.com

---

> ⭐ **If you find this helpful, give it a star!**  
> 🔁 Fork it and create your own version!
