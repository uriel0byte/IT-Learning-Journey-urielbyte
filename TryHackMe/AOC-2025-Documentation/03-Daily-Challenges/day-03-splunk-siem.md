# Day 3: Splunk Basics - Did you SIEM?

## 📋 Quick Facts
- **Date Completed:** December 3, 2025
- **Time Spent:** 3 hours
- **Difficulty:** ★★★☆ (Hard)
- **Category:** SIEM / Log Analysis / Defensive Security
- **Room URL:** https://tryhackme.com/room/splunkforloganalysis-aoc2025-x8fj2k4rqp

---

## 🎯 Challenge Overview

This challenge introduced SIEM (Security Information and Event Management) operations using Splunk, the industry-leading log analysis platform. The scenario involved investigating a ransomware attack by King Malhare's Bandit Bunnies on The Best Festival Company (TBFC) systems. I analyzed web traffic and firewall logs to trace the complete attack chain from initial reconnaissance to data exfiltration.

**Learning Objectives:**
- Ingest and interpret custom log data in Splunk
- Create and apply custom field extractions
- Use Search Processing Language (SPL) to filter and refine search results
- Conduct a real investigation to uncover key insights

---

## 💡 What I Learned

### Splunk SIEM Fundamentals
This was my **first time using Splunk** and working with SPL (Search Processing Language). I learned how to:
- Navigate the Splunk interface (Search & Reporting app)
- Query logs using `index=main` and `sourcetype` filters
- Interpret field extractions (`client_ip`, `user_agent`, `path`, `status`)
- Use the timeline visualization to identify traffic spikes (attack windows)
- Correlate events across multiple data sources (`web_traffic` and `firewall_logs`)

### Attack Chain Investigation
I traced the complete attack progression through log analysis:

**1. Reconnaissance (Footprinting)**
- Attacker probed for exposed configuration files (`/.env`, `/.git`, `/phpinfo`)
- Used low-level tools like `curl` and `wget`
- Received 404/403/401 errors (failed attempts)

**2. Enumeration (Vulnerability Testing)**
- Path traversal attempts (`../../etc/passwd`)
- Open redirect testing
- Active vulnerability scanning beyond simple reconnaissance

**3. Exploitation (SQL Injection)**
- Automated attack using `sqlmap` tool (identified via user agent)
- Time-based SQL injection with `SLEEP(5)` payloads
- Successful exploitation confirmed by HTTP 504 status codes

**4. Data Exfiltration**
- Downloaded large compressed files (`backup.zip`, `logs.tar.gz`)
- Used tools like `curl`, `zgrab` for bulk data extraction

**5. Ransomware Deployment (RCE)**
- Uploaded webshell (`shell.php`)
- Executed ransomware binary (`bunnylock.bin`)
- Achieved Remote Code Execution (RCE)

**6. C2 Communication**
- Established outbound connection to attacker's C2 server
- Confirmed via firewall logs showing `ACTION=ALLOWED` and `REASON=C2_CONTACT`
- Calculated total bytes exfiltrated using `stats sum(bytes_transferred)`

### SPL Query Techniques
I learned to write effective SPL queries for threat hunting:

```spl
# Basic filtering
index=main sourcetype=web_traffic

# Exclude benign traffic
user_agent!=*Mozilla* user_agent!=*Chrome*

# Focus on specific attacker IP
client_ip="<ATTACKER_IP>" AND path IN ("/.env", "/.git*")

# Correlate across data sources
sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="<ATTACKER_IP>"

# Aggregate and calculate
| stats count by client_ip | sort -count
| stats sum(bytes_transferred) by src_ip
```

**Key SPL Functions Learned:**
- `timechart span=1d count` - Visualize events over time
- `stats count by field` - Aggregate data
- `sort -count | reverse` - Order results
- `table _time, field1, field2` - Display specific fields
- `sum()` - Calculate totals

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Splunk Enterprise** - SIEM platform for log ingestion and analysis
2. **SPL (Search Processing Language)** - Query language for Splunk
3. **Timeline Visualization** - Graph events to identify attack windows
4. **Field Extraction** - Parse log data into structured fields

### Techniques
- Log correlation across multiple sources (`web_traffic` + `firewall_logs`)
- Anomaly detection (identifying traffic spikes and suspicious user agents)
- Attack chain reconstruction (tracing attacker progression)
- Threat hunting (filtering benign traffic to focus on malicious activity)
- Data aggregation (calculating totals, grouping by IP)
- Timeline analysis (identifying peak attack periods)

---

## 🤔 Challenges I Faced

**SPL Syntax Learning Curve:** This was my first time using any SIEM query language. I struggled with SPL syntax for about **1 hour**, trying to remember the correct operators (`!=`, `AND`, `OR`, `IN`) and function syntax (`stats`, `timechart`, `sort`). 

**Remembering vs. Understanding:** I initially tried to memorize SPL commands, but then I realized this was my first exposure—I needed to focus on understanding the logic, not memorization. I reminded myself this is a skill I'll develop over time through the roadmap I've planned for SIEM training.

**Log Correlation:** Understanding how to pivot between `web_traffic` logs (attacker reconnaissance) and `firewall_logs` (C2 communication) required thinking about how different data sources complement each other in an investigation.

**Filtering Noise:** Real-world logs contain massive amounts of benign traffic. Learning to filter out legitimate user agents (Mozilla, Chrome, Safari, Firefox) to focus on suspicious activity was critical for efficient analysis.

---

## ✅ How This Helps My Career

SIEM expertise appears in **78% of SOC Analyst job postings**, making it the #1 technical requirement. This challenge gave me hands-on experience with:

**Real SOC Analyst Workflows:**
- Alert triage (identifying suspicious activity from large datasets)
- Threat hunting (proactive searching for indicators of compromise)
- Incident investigation (reconstructing attack timelines)
- Log correlation (connecting dots across multiple data sources)

**Splunk Proficiency:**
- Industry-standard SIEM platform used by Fortune 500 companies
- SPL query writing (essential skill for daily SOC operations)
- Dashboard interpretation and timeline analysis

**Attack Pattern Recognition:**
- Understanding attacker TTPs (Tactics, Techniques, Procedures)
- Recognizing reconnaissance → exploitation → exfiltration progression
- Identifying C2 communication patterns

**Interview Talking Point:** "I've conducted hands-on SIEM investigations using Splunk, where I analyzed web traffic and firewall logs to reconstruct a complete ransomware attack chain—from initial SQL injection through C2 communication and data exfiltration. I can write SPL queries to hunt for threats, correlate logs across multiple sources, and identify attack patterns in large datasets."

---

## 🔗 Security+ Connection

**Domain 4.0 - Security Operations (28%):** SIEM usage, log analysis, monitoring, threat detection, incident investigation, and alert triage.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Attack techniques (SQL injection, webshells, ransomware), reconnaissance methods, and exploitation tactics.

---

## 📸 Evidence

![Splunk Timeline Analysis](../07-Screenshots/day-03/traffic-spike-timeline.png)
*Identified suspicious traffic spike indicating attack window using Splunk timeline visualization*

![SPL Query - Attacker IP](../07-Screenshots/day-03/attacker-ip-correlation.png)
*Used SPL to isolate attacker IP and trace activity across reconnaissance, exploitation, and exfiltration phases*

![C2 Communication Detection](../07-Screenshots/day-03/c2-firewall-logs.png)
*Correlated firewall logs to confirm outbound C2 communication from compromised server*

---