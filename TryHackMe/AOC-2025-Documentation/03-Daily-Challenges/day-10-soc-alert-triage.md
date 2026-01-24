# Day 10: SOC Alert Triaging - Tinsel Triage

## 📋 Quick Facts
- **Date Completed:** December 10, 2025
- **Time Spent:** 3 hours
- **Difficulty:** ★★★★ (Hard)
- **Category:** SIEM / SOC Operations / Cloud Security
- **Room URL:** https://tryhackme.com/room/azuresentinel-aoc2025-a7d3h9k0p2

---

## 🎯 Challenge Overview

This challenge simulated a real SOC (Security Operations Center) scenario where TBFC's Azure environment was under attack by the Evil Easter Bunnies. Alerts were flooding in, and I played the role of McSkidy triaging incidents using Microsoft Sentinel, a cloud-native SIEM platform. I learned systematic alert prioritization, investigated high-severity privilege escalation alerts, correlated events across multiple hosts using KQL (Kusto Query Language), and reconstructed attack chains from initial access to persistence.

**Learning Objectives:**
- Understand the importance of alert triage and prioritization in a SOC environment
- Explore Microsoft Sentinel to review and analyze security alerts
- Correlate logs to identify real attacker activities and determine alert verdicts
- Practice real-world SOC analyst workflows

---

## 💡 What I Learned

### The Importance of Alert Triage

**The Problem:** When alerts flood in, jumping into each one isn't efficient. Not all alerts are equal:
- Some are noise
- Others are false positives
- A few may indicate real threats in progress

**Alert Triaging:** The process of systematically assessing and prioritizing alerts to:
- Identify which alerts deserve immediate attention
- Determine which can be deprioritized
- Decide which can be safely ignored temporarily

**Goal:** Separate chaos from clarity, allowing analysts to focus time and resources where it truly matters.

### The Four Key Triage Factors

When multiple alerts appear, analysts need a consistent method to assess and prioritize them quickly.

**1. Severity Level**
- Review alert's severity rating: Informational → Low → Medium → High → Critical
- **Why it matters:** Indicates urgency of response and potential business risk
- **What I do:** Start with Critical/High severity alerts first

**2. Timestamp and Frequency**
- Identify when alert was triggered
- Check for related activity before and after that time
- **Why it matters:** Helps identify ongoing attacks or patterns of repeated behavior
- **What I do:** Build a timeline of events

**3. Attack Stage**
- Determine which stage of attack lifecycle the alert indicates:
  - Reconnaissance (information gathering)
  - Initial Access (entry point)
  - Privilege Escalation (gaining higher permissions)
  - Persistence (maintaining access)
  - Data Exfiltration (stealing data)
- **Why it matters:** Gives insight into how far the attacker has progressed and their objective
- **What I do:** Understand attacker progression

**4. Affected Asset**
- Identify the system, user, or resource involved
- Assess its importance to operations
- **Why it matters:** Prioritizes response based on asset's criticality and potential impact
- **What I do:** Protect high-value targets first

**Summary:** These four factors represent essential dimensions of triage:
- **Severity:** How bad?
- **Time:** When?
- **Context:** Where in the attack lifecycle?
- **Impact:** Who or what is affected?

### Investigation Methodology (6-Step Process)

After identifying which alerts deserve attention, follow these steps:

**1. Investigate the Alert in Detail**
- Open the alert and review entities, event data, detection logic
- Confirm whether activity represents real malicious behavior

**2. Check Related Logs**
- Examine relevant log sources
- Look for patterns or unusual actions that align with the alert

**3. Correlate Multiple Alerts**
- Identify other alerts involving same user, IP address, or device
- Correlation often reveals broader attack sequence or coordinated activity

**4. Build Context and Timeline**
- Combine timestamps, user actions, and affected assets
- Reconstruct sequence of events
- Determine if attack is ongoing or contained

**5. Decide on Next Action**
- **Escalate:** If indicators of compromise (IOCs) exist
- **Investigate further:** If more evidence or correlation needed
- **Close/Suppress:** If confirmed false positive (update detection rules)

**6. Document Findings and Lessons Learned**
- Keep clear record of analysis, decisions, remediation steps
- Proper documentation strengthens processes and supports continuous improvement

### Microsoft Sentinel (Cloud-Native SIEM)

**What it is:** Microsoft Sentinel is a cloud-native Security Information and Event Management (SIEM) and Security Orchestration, Automation, and Response (SOAR) platform.

**Capabilities:**
- Collects data from Azure services, applications, and connected sources
- Detects, investigates, and responds to threats in real-time
- Provides visibility into Azure tenant activity
- Allows efficient pivoting from one alert to another

**Key Features Used:**
- **Incidents Tab:** View triggered incidents with severity filtering
- **Threat Management:** Centralized incident dashboard
- **Evidence Section:** Raw event data behind alerts
- **Investigation Tools:** Correlation and timeline analysis
- **Log Analytics:** Custom KQL queries for deep-dive investigation

### Understanding Related Alerts (Attack Chain Reconstruction)

**Critical Concept:** Multiple alerts linked to the same entity (machine, user, IP) typically indicate different stages of the same intrusion, not isolated incidents.

**Example Attack Chain on app-02:**

| Alert | Attack Stage | What It Suggests |
|-------|--------------|------------------|
| **Root Login from External IP** | Initial Access | Attacker gained remote SSH access to system |
| **SUID Discovery** | Privilege Escalation | Attacker looked for ways to escalate privileges |
| **Kernel Module Insertion** | Persistence | Attacker installed malicious kernel module for persistence |

**Why This Matters:** By analyzing which alerts share the same entities, we can:
- Trace the attack path from initial access to persistence
- Understand attacker progression
- Prioritize response based on attack stage

### KQL (Kusto Query Language) - NEW and CHALLENGING

**What is KQL:** Query language used in Microsoft Sentinel (similar to SPL in Splunk, but different syntax).

**Basic Query Structure:**

```kql
set query_now = datetime(2025-10-30T05:09:25.9886229Z);
Syslog_CL
| where host_s == 'app-02'
| project _timestamp_t, host_s, Message
```

**What this does:**
- Sets a time reference point
- Queries the `Syslog_CL` custom log table
- Filters for specific host (`app-02`)
- Projects (displays) only timestamp, host, and message fields

**KQL Operators I Learned:**
- `|` - Pipe operator (like SPL, chains commands)
- `where` - Filters results (like SQL WHERE)
- `project` - Selects which columns to display
- `==` - Equality comparison
- `datetime()` - Time formatting function

**What I Found Using KQL:**
Investigating `app-02`, I discovered this suspicious sequence:
1. Execution of `cp` (copy) command to create shadow file backup
2. Addition of user account "Alice" to sudoers group
3. Modification of backupuser account by root
4. Insertion of `malicious_mod.ko` kernel module
5. Successful SSH authentication by root user

**Analysis:** This sequence suggests privilege escalation and persistence behavior, not normal system operations.

### Privilege Escalation Alerts Investigated

**High-Severity Alerts Triaged:**
- **Linux PrivEsc - Kernel Module Insertion** (3 events, 3 entities, Privilege Escalation tactic)
- **Linux PrivEsc - Polkit Exploit Attempt**
- **Linux PrivEsc - Sudo Shadow Access**
- **Linux PrivEsc - User Added to Sudo Group**

**Affected Hosts:**
- app-01
- app-02
- websrv-01
- storage-01

**Attack Patterns Identified:**
- Root SSH logins from external IPs (Initial Access)
- SUID binary discovery (Privilege Escalation reconnaissance)
- Kernel module insertion (Persistence)
- Sudoers group modification (Privilege Escalation)
- Shadow file access (Credential harvesting)

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Microsoft Sentinel** - Cloud-native SIEM platform (Azure)
2. **KQL (Kusto Query Language)** - Log querying and analysis
3. **Azure Portal** - Cloud infrastructure management interface
4. **Syslog_CL** - Custom log table for Linux system logs

### Techniques
- **Alert triage** - Systematic prioritization using 4-factor model
- **Incident correlation** - Linking alerts by common entities
- **Timeline reconstruction** - Building sequence of events
- **Log analysis** - Deep-dive investigation using KQL queries
- **Attack chain mapping** - Identifying progression from initial access to persistence
- **Entity analysis** - Tracking users, hosts, IPs across multiple alerts
- **Evidence validation** - Confirming malicious activity vs. false positives

---

## 🤔 Challenges I Faced

**Lots of Content - Everything is New:** This challenge was overwhelming because almost everything was new to me. The volume of information to process was significant.

**KQL Query Language is Hard:** KQL was particularly challenging because I have **no background in programming** or anything related to coding. The only similar experience was SPL from Day 3, but **I forgot most of Day 3** by the time I reached Day 10. Starting fresh with a new query language without programming foundations was difficult.

**What Made It Hard:**
- **New SIEM platform** - Microsoft Sentinel vs. Splunk (different interface, different workflow)
- **Cloud environment** - Azure portal navigation was unfamiliar
- **Query syntax** - KQL operators (`|`, `where`, `project`) were confusing at first
- **Alert correlation** - Understanding how to link multiple alerts to same entity
- **Attack chain thinking** - Visualizing progression from initial access → privilege escalation → persistence

**What Made It Take 3 Hours:**
- Reading and re-reading triage methodology
- Trial and error with KQL queries
- Understanding Sentinel interface navigation
- Correlating 8+ incidents across 4 hosts
- Answering detailed investigation questions

**Overall Experience:** Still fun to explore despite the difficulty! Learning real SOC workflows and cloud SIEM was valuable even though it was challenging. The hands-on incident investigation made the concepts click better than just reading theory.

---

## ✅ How This Helps My Career

**This is THE most important challenge so far for my SOC Analyst career goal.**

**Why Alert Triage Matters:**
- **90% of SOC Analyst job postings** mention alert triage/incident investigation
- Alert triage is the **#1 daily responsibility** of SOC Analysts
- This challenge simulates **real SOC work** more than any previous day

**Direct SOC Analyst Applications:**

**Daily Operations:**
- Triage incoming alerts using 4-factor model (Severity, Time, Attack Stage, Impact)
- Prioritize which incidents need immediate attention
- Correlate multiple alerts to identify attack campaigns
- Investigate high-severity privilege escalation alerts
- Document findings and escalate to incident response team

**Cloud Security (High Demand):**
- Microsoft Sentinel experience (Azure cloud SIEM)
- 60% of companies use cloud infrastructure (Azure, AWS, GCP)
- Cloud security skills are in high demand and growing
- Understanding cloud-native SIEM platforms sets me apart

**SIEM Skills (Industry-Standard):**
- Alert correlation across multiple data sources
- Log analysis using query languages (KQL, similar to SPL)
- Timeline reconstruction from raw events
- Evidence validation and false positive reduction

**Incident Investigation Methodology:**
- Systematic 6-step investigation process
- Attack chain mapping (initial access → privilege escalation → persistence)
- Entity tracking (users, hosts, IPs)
- Documentation and escalation procedures

**Real-World Scenarios:**
This challenge mirrors actual SOC work:
- Multiple simultaneous alerts
- Privilege escalation attacks
- Linux server compromises
- Cloud environment threats
- Time pressure to triage effectively

**Career Skills Developed:**
- **SIEM proficiency** - Microsoft Sentinel (cloud), previously learned Splunk (on-prem)
- **Query languages** - KQL (Azure), SPL (Splunk)
- **Cloud platforms** - Azure Portal, cloud security concepts
- **Incident response** - Triage → Investigation → Escalation → Documentation
- **Critical thinking** - Distinguishing real threats from false positives

**Interview Talking Point:** "I have hands-on experience with SOC alert triage using Microsoft Sentinel in Azure cloud environments. I can systematically prioritize alerts using severity, timestamp, attack stage, and affected asset analysis. I've investigated real privilege escalation attack chains, correlated multiple alerts to identify coordinated intrusions, and used KQL to perform deep-dive log analysis. I understand the complete SOC analyst workflow from initial triage through investigation, escalation, and documentation. This experience directly applies to the daily responsibilities of monitoring, triaging, and investigating security alerts in a production SOC environment."

---

## 🔗 Security+ Connection

**Domain 4.0 - Security Operations (28%):** SIEM operations, alert triage, incident investigation, log analysis, threat hunting, incident response procedures, documentation.

**Domain 3.0 - Security Architecture (18%):** Cloud security architecture (Azure), SIEM deployment, security monitoring infrastructure.

---

## 📸 Evidence

![Microsoft Sentinel Incidents Dashboard](../07-Screenshots/day-10/sentinel-incidents-overview.png)
*Reviewed 8 incidents (4 high-severity, 4 medium-severity) in Microsoft Sentinel, prioritizing privilege escalation alerts*

![KQL Log Analysis - app-02](../07-Screenshots/day-10/kql-attack-chain-app02.png)
*Used KQL query to investigate app-02, revealing attack chain: shadow backup → Alice added to sudoers → kernel module insertion → root SSH login*

![Alert Correlation Timeline](../07-Screenshots/day-10/alert-correlation-entities.png)
*Correlated multiple alerts across same entities (hosts, users, IPs) to map complete attack progression from initial access to persistence*

---