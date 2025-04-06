

---


# 📘 Example Scenario – CCM Metric Design

## Policy Control
**"All critical systems must be patched within 30 days of a vendor releasing a security update to mitigate vulnerabilities."**

### Context
You’re working at **XYZ Company**, monitoring IT servers and OT devices (e.g., SCADA systems) in the **Cyber Security Operations Centre**.

---

## 🧩 Step-by-Step CCM Metric Design Process

---

### ✅ Step 1: Understand the Policy Control

- **What’s the Rule?**  
  Systems must be patched within 30 days of a patch release.

- **Why?**  
  To reduce the risk of exploits targeting known vulnerabilities (e.g., a zero-day used in ransomware).

- **Scope:**  
  “Critical systems” (e.g., Windows servers, PLCs in the OT environment).

- **Goal:**  
  Measure:
  - *Implementation correctness* (Are patches applied?)
  - *Operating efficiency* (Are they applied fast enough?)

- **Output:**  
  You’ve clarified the intent: ensure **timely patching across IT/OT**.

---

### 📏 Step 2: Define the Metric

- **Metric Name:** `Patch Compliance Rate`

- **What It Measures:**  
  The percentage of critical systems patched within 30 days of a patch release.

- **Formula:**
  ```text
  Patch Compliance Rate = (Number of systems patched within 30 days / Total number of critical systems) × 100
  ```

- **Target:**  
  100% compliance (all systems patched on time).

- **Frequency:**  
  Checked monthly (continuous monitoring with periodic reporting).

- **Output:**  
  A clear, specific metric: `Patch Compliance Rate` with formula and target.

---

### 🛠️ Step 3: Identify Implementation Details

- **What’s “Critical”?**  
  Define systems (e.g., servers in the data center, OT devices like PLCs).

- **Patch Source:**  
  Vendor announcements (e.g., Microsoft Patch Tuesday, Siemens firmware updates).

- **Time Tracking:**  
  Record:
  - Patch release date
  - Patch installation date

- **System Inventory:**  
  Pull from CMDB or OT asset management tool.

- **Output:**  
  Scope of monitoring is defined, including relevant patch events.

---

### 🧰 Step 4: Select Tools and Evidence

- **Tools:**
  - **Tenable Nessus**: Scans for missing patches.
  - **Splunk**: Collects patch deployment logs.
  - **Asset Database**: (e.g., ServiceNow, OT inventory tools)

- **Evidence:**
  - Nessus scan reports (e.g., `Server X missing KB12345`)
  - Patch logs (e.g., `KB12345 installed on 2025-04-10`)
  - Vendor release notices (e.g., Microsoft bulletin from 2025-04-01)

- **Output:**  
  Data collection sources and tools are selected.

---

### 🔄 Step 5: Design Data Acquisition

- **Process:**
  - **Patch Release Date:** Scrape vendor sites / RSS feeds.
  - **System Scans:** Run Nessus weekly.
  - **Log Collection:** Use Splunk for patch logs.
  - **Cross-Reference:** Compare release vs. install dates.
  - **Automation:** Use Python to process and correlate data.

- **Output:**  
  A repeatable, automatable data collection process.

---

### 📊 Step 6: Analyze and Calculate the Metric

- **Sample Data:**
  - Total critical systems: 50 (30 IT, 20 OT)
  - Patch released: April 1, 2025
  - Deadline: May 1, 2025
  - Patched by deadline: 45 systems
  - Unpatched: 5 systems

- **Calculation:**
  ```text
  Patch Compliance Rate = (45 / 50) × 100 = 90%
  ```

- **Analysis:**  
  - 90% is **below** the 100% target.
  - 2 OT devices had no patch available.
  - 3 IT servers faced deployment delays.

- **Output:**  
  Compliance score and root causes for non-compliance.

---

### 📈 Step 7: Report Control Effectiveness

- **Format:**  
  Dashboard (e.g., Splunk) or written report.

- **Content:**
  - Metric: `90% Patch Compliance Rate`
  - Trend: Dropped from 95% last month.
  - Insight: OT vendor delays; IT process issues.

- **Audience:**
  - Control implementors (patch teams)
  - Product owners (OT)
  - Architects (system design issues)

- **Output:**  
  Actionable reporting of control effectiveness.

---

### 🔁 Step 8: Collaborate and Refine

- **Feedback Loop:**
  - **Implementors:** “Why 3 servers late?” ➜ Approval delays ➜ Automate.
  - **Product Owners:** “OT patches missing?” ➜ Escalate to Siemens.
  - **Architects:** “Design OT failover for patching?”

- **Refinement:**  
  Modify metric to distinguish **IT vs. OT systems** if needed.

- **Output:**  
  Improved metric with better scope and precision.

---

## 🧾 Final Metric Definition

- **Name:** Patch Compliance Rate
- **Formula:**
  ```text
  (Systems patched within 30 days / Total critical systems) × 100
  ```

- **Tools:** Nessus, Splunk, asset database  
- **Evidence:** Scan reports, patch logs, vendor release dates  
- **Target:** 100%  
- **Frequency:** Monthly reporting, continuous collection  
- **Action Threshold:**  
  If below 95%, escalate to CCM lead for review.

---
