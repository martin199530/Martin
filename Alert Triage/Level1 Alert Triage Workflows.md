
# 🛡️ Level 1 Analyst Alert Triage Workflows

This document provides simple, actionable triage workflows tailored for a Level 1 Cybersecurity Analyst. Each section covers a common type of alert encountered in a SOC or IT security environment.

---

## 📄 1. Phishing Alert Triage Workflow

**Alert Example:** “User reported a suspicious email with a suspicious link”

### ✅ Step 1: Check Alert Details
- **Sender Email:** unknown@weird-domain.biz  
- **Subject Line:** “Your invoice is ready!”  
- **Link/Attachment?** Yes — links to `http://malicious-phish.com/invoice.html`  
- **Reported By:** user123@example.com  
- **Time Received:** 10:42 AM

### 🧠 Step 2: Add Context
- Does the link lead to a known phishing site? → Check with [VirusTotal](https://virustotal.com)  
- Does the sender spoof a known company? → Look for misspelled domains  
- Is this user a VIP or has access to sensitive data?  
- Are there other reports of similar emails?

### 🚦 Step 3: Classify the Alert
- 🔴 High = Link confirmed malicious + important user targeted  
- 🟠 Medium = Suspicious but not confirmed malicious  
- 🟢 Low = Safe, already blocked or internal test

### 📩 Step 4: Take Initial Action
- Isolate email in email gateway or sandbox it  
- Block the domain if malicious  
- Inform the user to delete and not click  
- Escalate to L2 if threat confirmed

### 🧹 Step 5: Document and Close
- Save email headers, link scans, and actions taken  
- Add to internal phishing indicators if verified

---

## 🦠 2. Malware Detection Alert Triage Workflow

**Alert Example:** “Endpoint Protection detected and quarantined suspicious .exe file”

### ✅ Step 1: Check Alert Details
- **Host:** LAPTOP-IT32  
- **File Name:** `invoice_reader.exe`  
- **Detected By:** Defender ATP  
- **Action Taken:** Quarantined  
- **Time:** 2:15 PM

### 🧠 Step 2: Add Context
- Did the user execute the file?  
- Was it downloaded from email or USB?  
- Is the detection signature reliable?  
- Any unusual behavior (CPU spikes, network traffic, lateral movement)?

### 🚦 Step 3: Classify the Alert
- 🔴 High = Executed malware, lateral movement, suspicious persistence  
- 🟠 Medium = Detected + quarantined before execution  
- 🟢 Low = False positive or test file

### 📩 Step 4: Take Initial Action
- Check logs for post-execution behavior  
- Run endpoint scan or memory dump  
- Isolate the machine if active threat  
- Escalate to L2 if confirmed threat or if uncertainty remains

### 🧹 Step 5: Document and Close
- Record file hash, user activity, and your findings  
- Save scan reports and detection logs  
- Note whether escalation was needed

---

## ☁️ 3. Cloud Security Incident Triage Workflow (AWS/Azure/GCP)

**Alert Example:** “Unusual IAM login detected from unknown location”

### ✅ Step 1: Check Alert Details
- **User Account:** `service-account-01`  
- **Login Time:** 6:22 PM  
- **Source IP:** 103.92.40.10  
- **Location:** Vietnam  
- **Platform:** AWS Management Console

### 🧠 Step 2: Add Context
- Is the source IP suspicious or geo-improbable?  
- Does this account normally log in from there?  
- Is MFA enabled for the user?  
- Are there any API actions that followed the login?

### 🚦 Step 3: Classify the Alert
- 🔴 High = Impossible travel, new country, sensitive role  
- 🟠 Medium = New IP but no suspicious actions  
- 🟢 Low = VPN false positive or known travel

### 📩 Step 4: Take Initial Action
- Disable the access key or lock the account temporarily  
- Review CloudTrail logs (AWS) / Audit Logs (Azure/GCP)  
- Check for any changes to security groups, IAM roles  
- Escalate if risk confirmed

### 🧹 Step 5: Document and Close
- Save IP lookup, logs, actions, and user justification if needed  
- Update internal documentation or risk dashboard

---

> 🔒 These workflows are meant to help guide consistent and effective triage, escalate appropriately, and support documentation in any SOC or IT security environment.
