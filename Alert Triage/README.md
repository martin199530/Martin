# 🛡️ Level 1 Analyst Alert Triage Workflows

This guide provides actionable triage workflows for **Level 1 Cybersecurity Analysts**, focused on three common incident types:
- 📄 Phishing
- 🦠 Malware
- ☁️ Cloud Security

Each workflow includes a breakdown of steps to follow when handling real alerts in a SOC or IT environment.

## 📄 Phishing Alert Triage Workflow

> **Example:** User reports a suspicious email with a malicious-looking link

### ✅ Step 1: Check Alert Details
- **Sender Email:** `unknown@weird-domain.biz`
- **Subject Line:** `Your invoice is ready!`
- **Link/Attachment?** Yes — links to `http://malicious-phish.com/invoice.html`
- **Reported By:** `user123@example.com`
- **Time Received:** 10:42 AM

### 🧠 Step 2: Add Context
- 🔍 Check link reputation on [VirusTotal](https://virustotal.com)
- 🧐 Is the domain a spoof or typo?
- 👤 Is the user a VIP?
- 📬 Any other reports of this email?

### 🚦 Step 3: Classify the Alert
- 🔴 **High:** Confirmed malicious + sensitive user
- 🟠 **Medium:** Suspicious but unclear
- 🟢 **Low:** Safe or blocked internally

### 📩 Step 4: Take Action
- Quarantine or sandbox the email
- Block the domain if confirmed
- Notify the user
- Escalate to L2 if malicious

### 🧹 Step 5: Document & Close
- Save headers, links, evidence
- Update threat intel feeds or email filters

## 🦠 Malware Detection Alert Triage Workflow

> **Example:** Endpoint protection quarantines a suspicious executable

### ✅ Step 1: Check Alert Details
- **Host:** `LAPTOP-IT32`
- **File Name:** `invoice_reader.exe`
- **Detected By:** Defender ATP
- **Action Taken:** Quarantined

### 🧠 Step 2: Add Context
- Was the file executed?
- How was it introduced (email, USB)?
- Any suspicious processes or traffic?

### 🚦 Step 3: Classify the Alert
- 🔴 **High:** Executed with signs of compromise
- 🟠 **Medium:** Quarantined before execution
- 🟢 **Low:** False positive or known file

### 📩 Step 4: Take Action
- Analyze logs and behavior
- Run full scan
- Isolate the endpoint if needed
- Escalate if threat confirmed

### 🧹 Step 5: Document & Close
- Save hash, detection logs, and actions taken

## ☁️ Cloud Security Incident Triage Workflow

> **Example:** IAM login from an unusual country

### ✅ Step 1: Check Alert Details
- **User:** `service-account-01`
- **IP Address:** `103.92.40.10`
- **Login Location:** Vietnam
- **Platform:** AWS Console

### 🧠 Step 2: Add Context
- 🔐 Is MFA enabled?
- 📍 Is this geo-location normal?
- 🕵️‍♂️ Any sensitive actions or changes?

### 🚦 Step 3: Classify the Alert
- 🔴 **High:** New country, no MFA, critical user
- 🟠 **Medium:** Unusual IP but no damage
- 🟢 **Low:** Known travel or VPN usage

### 📩 Step 4: Take Action
- Lock account or disable key
- Review CloudTrail or audit logs
- Escalate if needed

### 🧹 Step 5: Document & Close
- Record logs, IP info, and justification
- Update incident register or SIEM tags

## ⚠️ Important Notes
These playbooks are designed for quick triage and escalation. Always follow your organization’s Incident Response Plan (IRP) and escalation matrix.

## 📘 Contribution
*Maintained by a cybersecurity analyst for junior SOC roles. Pull requests are welcome!*

