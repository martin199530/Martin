# 🔐 Basic Alert Triage Workflow for a Level 1 Cybersecurity Analyst

Let’s assume you're using a SIEM like Splunk, Microsoft Sentinel, or IBM QRadar, and you receive the following alert:

**Alert Example:**  
> *"Multiple Failed Login Attempts Detected"*

---

## ✅ Step 1: Check the Alert Details

- **Alert Type:** Failed login attempts  
- **Source IP:** 45.77.12.88  
- **Destination IP:** 10.0.0.5 (internal server)  
- **Username Involved:** `admin_test`  
- **Time Range:** Last 5 minutes  
- **Number of Attempts:** 50

---

## 🧠 Step 2: Add Context

- **Source IP internal or external?**  
  → External IP = suspicious  
- **Is the username valid and active?**  
  → `admin_test` = test account (possibly lower risk)  
- **Is the source IP blacklisted or malicious?**  
  → Check using tools like:
  - [VirusTotal](https://www.virustotal.com)
  - [AbuseIPDB](https://www.abuseipdb.com)
  → Result: IP is **malicious**
- **Are other accounts affected?**  
  → Yes, 3 other accounts targeted from the same IP

---

## 🚦 Step 3: Classify the Alert

Use a simple severity scale:

- 🔴 **High** = Immediate action required  
- 🟠 **Medium** = Needs more investigation  
- 🟢 **Low** = Likely benign or informational

**Classification for this example:**  
🔴 **High** — External brute-force attempt from a known malicious IP

---

## 📩 Step 4: Take Initial Action

Summarize findings for escalation:

```text
Alert: Multiple failed logins to admin_test  
Time: 10:30 AM - 10:35 AM  
Source IP: 45.77.12.88 (blacklisted)  
Destination: 10.0.0.5  
Accounts affected: 4  
Initial Risk: High - Brute-force attempt from malicious external IP  
Next Action: Escalated to L2 for deeper investigation and potential IP block
