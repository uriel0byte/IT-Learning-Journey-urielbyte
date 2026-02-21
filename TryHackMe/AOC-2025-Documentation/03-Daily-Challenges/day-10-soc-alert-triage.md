# Day 10: SOC Alert Triaging - Tinsel Triage

## 📋 Quick Facts
- **Date Completed:** December 10, 2025
- **Time Spent:** 3 hours
- **Difficulty:** ★★★★ (Hard)
- **Category:** SIEM / SOC Operations / Cloud Security
- **Room URL:** https://tryhackme.com/room/azuresentinel-aoc2025-a7d3h9k0p2

---

## 🎯 Challenge Overview

The Best Festival Company's SOC was in chaos—screens flickered with red and orange warnings as alerts flooded in like a digital thunderstorm. Something strange was happening across the Azure environment, and whispers spread: the Evil Easter Bunnies were behind it. Playing the role of McSkidy, I triaged 8 incidents (4 high-severity, 4 medium-severity) using Microsoft Sentinel, a cloud-native SIEM platform. I systematically prioritized alerts using the 4-factor model, investigated high-severity privilege escalation attacks across multiple Linux hosts (app-01, app-02, websrv-01, storage-01), correlated events using KQL queries, and reconstructed complete attack chains from initial root SSH logins through privilege escalation to kernel module persistence.

**Learning Objectives:**
- Understand the importance of alert triage and prioritization in SOC
- Explore Microsoft Sentinel to review and analyze security alerts
- Correlate logs to identify real attacker activities and determine verdicts
- Practice real-world SOC analyst workflows

---

## 💡 What I Learned

### The Critical Importance of Alert Triage

**The Problem: "It's Raining Alerts"**

When alerts flood in, jumping straight into each one isn't efficient:
- Some alerts are **noise** (benign activity misclassified)
- Others are **false positives** (detection rules need tuning)
- A few indicate **real threats in progress** (need immediate action)

**Alert Triaging Definition:**
The systematic process of assessing and prioritizing alerts to:
- Identify which deserve immediate attention
- Determine which can be deprioritized
- Decide which can be safely ignored temporarily

**Goal:** Separate chaos from clarity → focus time and resources where it truly matters.

### The Four Key Triage Factors

| Factor | Question | Why It Matters | Action |
|--------|----------|---------------|---------|
| **Severity Level** | How bad? | Indicates urgency + business risk | Start with Critical/High first |
| **Timestamp & Frequency** | When? | Identifies ongoing attacks or patterns | Build timeline |
| **Attack Stage** | Where in lifecycle? | Shows attacker progression | Understand their objective |
| **Affected Asset** | Who/what is hit? | Prioritizes by asset criticality | Protect high-value targets |

**Summary of Dimensions:**
```
Severity    → How bad?
Time        → When?
Context     → Where in attack lifecycle?
Impact      → Who or what is affected?
```

### 6-Step Investigation Methodology

**After triage identifies priority alerts, follow this process:**

**Step 1: Investigate Alert in Detail**
- Open alert, review entities, event data, detection logic
- Confirm if activity represents real malicious behavior

**Step 2: Check Related Logs**
- Examine relevant log sources
- Look for patterns or unusual actions aligning with alert

**Step 3: Correlate Multiple Alerts**
- Identify other alerts involving same user, IP, device
- Correlation reveals broader attack sequences

**Step 4: Build Context and Timeline**
- Combine timestamps, user actions, affected assets
- Reconstruct sequence of events
- Determine if attack is ongoing or contained

**Step 5: Decide on Next Action**
- **Escalate:** If IOCs exist
- **Investigate further:** If more evidence needed
- **Close/Suppress:** If confirmed false positive (update rules)

**Step 6: Document Findings**
- Record analysis, decisions, remediation steps
- Documentation strengthens processes, supports improvement

### Microsoft Sentinel (Cloud-Native SIEM)

**What it is:** Cloud-native Security Information and Event Management (SIEM) + Security Orchestration, Automation, and Response (SOAR) platform.

**Key Capabilities:**
- Collects data from Azure services, applications, connected sources
- Detects, investigates, responds to threats in real-time
- Provides visibility into Azure tenant activity
- Efficient pivoting between alerts

**Interface Components:**

**Incidents Tab (Threat Management):**
- Centralized dashboard of triggered incidents
- Severity filtering (Informational → Critical)
- Timeline view of incident creation

**Alert Details View:**
- Events count (how many triggered this alert)
- Creation timestamp
- Entities involved (hosts, users, IPs)
- Attack tactic classification (MITRE ATT&CK)
- "View full details" button → deeper investigation

**Evidence Section:**
- Raw event data behind alerts
- Actual commands executed
- Timestamps of suspicious activity
- Logs from affected systems

**Log Analytics:**
- Custom KQL queries for deep-dive investigation
- Access to custom log tables (e.g., `Syslog_CL`)

**Investigation Tools:**
- Similar incidents detection
- Incident timeline reconstruction
- Entity correlation across alerts

### Understanding Related Alerts (Attack Chain Reconstruction)

**Critical Concept:**
Multiple alerts linked to same entity (machine, user, IP) typically indicate **different stages of the same intrusion**, not isolated incidents.

**Example — Attack Chain on app-02:**

| Alert | Attack Stage | What It Reveals |
|-------|--------------|-----------------|
| Root SSH Login from External IP | Initial Access | Attacker gained remote access |
| SUID Discovery | Privilege Escalation (Recon) | Attacker looking for escalation paths |
| Kernel Module Insertion | Persistence | Attacker ensuring survival across reboots |

**Why This Matters:**
- Traces complete attack path (access → escalation → persistence)
- Shows attacker progression and objectives
- Prioritizes response based on how far they've gotten

**Application:**
When app-02 shows 3 separate alerts, don't treat as 3 isolated issues — this is **one coordinated attack** with multiple stages.

### KQL (Kusto Query Language) — NEW and CHALLENGING

**What is KQL:**
Query language for Microsoft Sentinel (similar to SPL in Splunk, but different syntax).

**Basic Query Structure:**
```kql
set query_now = datetime(2025-10-30T05:09:25.9886229Z);
Syslog_CL
| where host_s == 'app-02'
| project _timestamp_t, host_s, Message
```

**Breaking it down:**
- `set query_now =` → Sets time reference point
- `Syslog_CL` → Custom log table (Linux system logs)
- `|` → Pipe operator (chains commands like SPL)
- `where host_s == 'app-02'` → Filters for specific host
- `project` → Selects which columns to display

**KQL Operators I Learned:**

| Operator | Purpose | Example |
|----------|---------|---------|
| `\|` | Pipe (chain commands) | `Syslog_CL \| where ...` |
| `where` | Filter results | `where host_s == 'app-02'` |
| `project` | Select columns | `project _timestamp_t, host_s` |
| `==` | Equality | `host_s == 'app-02'` |
| `datetime()` | Time formatting | `datetime(2025-10-30...)` |

**What I Found Using KQL (app-02 Investigation):**

Suspicious event sequence:
1. `cp` (copy) command → Created shadow file backup
2. User "Alice" → Added to sudoers group
3. backupuser account → Modified by root
4. `malicious_mod.ko` → Kernel module inserted
5. Root user → Successful SSH authentication

**Analysis:** This is NOT normal system operations. This is privilege escalation + persistence behavior.

### Privilege Escalation Alerts Investigated

**High-Severity Alerts Triaged:**
- **Linux PrivEsc - Kernel Module Insertion** (3 events, 3 entities, Privilege Escalation)
- **Linux PrivEsc - Polkit Exploit Attempt**
- **Linux PrivEsc - Sudo Shadow Access**
- **Linux PrivEsc - User Added to Sudo Group**

**Affected Hosts:**
- app-01
- app-02
- websrv-01
- storage-01

**Attack Patterns Identified Across Hosts:**

| Attack Stage | Technique | Example Finding |
|-------------|-----------|-----------------|
| Initial Access | Root SSH from external IPs | Successful authentication from untrusted sources |
| Privilege Escalation (Recon) | SUID binary discovery | Searching for escalation opportunities |
| Privilege Escalation (Execution) | User added to sudoers | Alice account granted admin rights |
| Privilege Escalation (Execution) | Shadow file access | Credential harvesting attempts |
| Persistence | Kernel module insertion | malicious_mod.ko loaded at boot |

**Complete Attack Flow:**
```
External SSH → Gain access as root
       ↓
SUID discovery → Find escalation paths
       ↓
Add user to sudoers → Create backup admin account
       ↓
Access shadow file → Harvest credentials
       ↓
Insert kernel module → Ensure persistence
       ↓
Attacker maintains access even after reboot
```

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Microsoft Sentinel** - Cloud-native SIEM (Azure)
2. **KQL (Kusto Query Language)** - Log querying and analysis
3. **Azure Portal** - Cloud infrastructure management
4. **Syslog_CL** - Custom log table for Linux system logs

### Techniques
- **Alert triage** (4-factor systematic prioritization)
- **Incident correlation** (linking alerts by common entities)
- **Timeline reconstruction** (building attack sequences)
- **KQL log analysis** (deep-dive investigation)
- **Attack chain mapping** (initial access → persistence)
- **Entity analysis** (tracking users, hosts, IPs across alerts)
- **Evidence validation** (confirming malicious vs. false positive)

---

## 🤔 Challenges I Faced

**Lots of Content — Everything is New:**
This was overwhelming. Volume of information to process was significant. Almost everything was new territory.

**KQL is Hard:**
Particularly challenging because **I have no programming background**. Only similar experience was SPL from Day 3, but **I forgot most of Day 3** by Day 10. Starting fresh with a new query language without programming foundation was difficult.

**Specific Challenges:**
- **New SIEM platform:** Microsoft Sentinel vs. Splunk (different interface, workflow)
- **Cloud environment:** Azure portal navigation unfamiliar
- **Query syntax:** KQL operators (`|`, `where`, `project`) confusing initially
- **Alert correlation:** Linking multiple alerts to same entity took time to grasp
- **Attack chain thinking:** Visualizing progression (access → escalation → persistence)

**What Made It Take 3 Hours:**
- Reading/re-reading triage methodology
- Trial and error with KQL queries
- Understanding Sentinel interface navigation
- Correlating 8+ incidents across 4 hosts
- Answering detailed investigation questions

**Overall:** Still fun despite difficulty! Learning real SOC workflows and cloud SIEM was valuable. Hands-on incident investigation made concepts click better than theory alone.

---

## ✅ How This Helps My Career

**THIS IS THE MOST IMPORTANT CHALLENGE FOR MY SOC ANALYST CAREER GOAL.**

### Why Alert Triage Matters

**Statistics:**
- **90% of SOC Analyst job postings** mention alert triage/incident investigation
- Alert triage = **#1 daily responsibility** of SOC Analysts
- This challenge simulates **real SOC work** more than any previous day

**Direct SOC Analyst Applications:**

**Daily Operations:**
- Triage incoming alerts using 4-factor model (Severity, Time, Stage, Impact)
- Prioritize which incidents need immediate attention
- Correlate multiple alerts → identify attack campaigns
- Investigate high-severity privilege escalation alerts
- Document findings, escalate to incident response team

**Cloud Security (High Demand):**
- Microsoft Sentinel experience (Azure cloud SIEM)
- 60% of companies use cloud infrastructure (Azure, AWS, GCP)
- Cloud security skills in high demand and growing
- Understanding cloud-native SIEM platforms sets me apart

**SIEM Skills (Industry-Standard):**
- Alert correlation across multiple data sources
- Log analysis using query languages (KQL ≈ SPL)
- Timeline reconstruction from raw events
- Evidence validation, false positive reduction

**Incident Investigation Methodology:**
- Systematic 6-step investigation process
- Attack chain mapping (access → escalation → persistence)
- Entity tracking (users, hosts, IPs)
- Documentation and escalation procedures

**Real-World Scenarios This Mirrors:**
- Multiple simultaneous alerts
- Privilege escalation attacks
- Linux server compromises
- Cloud environment threats
- Time pressure to triage effectively

**Career Skills Developed:**
- ✅ **SIEM proficiency:** Microsoft Sentinel (cloud), Splunk (on-prem from Day 3)
- ✅ **Query languages:** KQL (Azure), SPL (Splunk)
- ✅ **Cloud platforms:** Azure Portal, cloud security concepts
- ✅ **Incident response:** Triage → Investigation → Escalation → Documentation
- ✅ **Critical thinking:** Distinguishing real threats from false positives

**Interview Talking Point:** "I have hands-on experience with SOC alert triage using Microsoft Sentinel in Azure cloud environments. I can systematically prioritize alerts using a 4-factor model: severity, timestamp, attack stage, and affected asset. I've investigated real privilege escalation attack chains across multiple Linux hosts, correlated alerts to identify coordinated intrusions, and used KQL to perform deep-dive log analysis that revealed complete attack progressions from initial SSH access through privilege escalation to kernel module persistence. I understand the complete SOC analyst workflow from initial triage through detailed investigation, evidence validation, escalation decisions, and documentation. This hands-on experience directly applies to the daily responsibilities of monitoring, triaging, and investigating security alerts in a production SOC environment, which is why this challenge is the most valuable for my career goal."

---

## 🔗 Security+ Connection

**Domain 4.0 - Security Operations (28%):** SIEM operations, alert triage, incident investigation, log analysis, threat hunting, incident response procedures, documentation.

**Domain 3.0 - Security Architecture (18%):** Cloud security architecture (Azure), SIEM deployment, security monitoring infrastructure.

---

## 📸 Evidence

**Note:** Lab environment credentials expired before screenshots could be captured. Documentation based on hands-on completion during active session.

### Investigation Summary - Microsoft Sentinel SOC Triage

**Incidents Dashboard Review:**
- Accessed Microsoft Sentinel via Azure Portal → Threat Management → Incidents tab
- Triaged 8 total incidents (4 high-severity, 4 medium-severity)
- High-severity alerts focused on Linux privilege escalation tactics
- Applied severity filtering to prioritize critical alerts first
- Expanded incident view to examine full details including entities, timestamps, and attack classifications

**Alert Details Investigated:**
Each high-severity incident revealed:
- Event count (typically 3 events per privilege escalation alert)
- Multiple entities involved (hosts, user accounts, processes)
- MITRE ATT&CK tactic classification (Privilege Escalation, Persistence)
- Creation timestamps showing recent attack activity
- Similar incidents linked to same affected hosts

**Affected Infrastructure:**
- **app-01:** Linux application server
- **app-02:** Linux application server  
- **websrv-01:** Linux web server
- **storage-01:** Linux storage server

All four hosts showed signs of coordinated privilege escalation attacks.

---

### KQL Log Analysis - Attack Chain Reconstruction

**Query Executed:**
```kql
set query_now = datetime(2025-10-30T05:09:25.9886229Z);
Syslog_CL
| where host_s == 'app-02'
| project _timestamp_t, host_s, Message
```

**Findings from app-02 Investigation:**

Chronological attack sequence identified:
1. **Shadow File Backup:** `cp` command executed to create backup of `/etc/shadow` (credential harvesting preparation)
2. **Privilege Escalation:** User account "Alice" added to sudoers group (admin rights granted)
3. **Account Modification:** backupuser account modified by root (alternate access method)
4. **Persistence Mechanism:** `malicious_mod.ko` kernel module inserted (survives reboots)
5. **Attacker Access:** Root user successful SSH authentication confirmed

**Analysis:**
This sequence demonstrates sophisticated multi-stage intrusion:
- Initial access → Privilege escalation → Persistence
- Matches MITRE ATT&CK framework progression
- Not normal system administration activity
- Required immediate incident response escalation

---

### Alert Correlation - Entity-Based Threat Hunting

**Correlation Methodology Applied:**
Identified multiple alerts linked to same entities (hosts, users, IPs) indicating coordinated attack campaign rather than isolated incidents.

**Example - app-02 Alert Clustering:**

| Alert Type | Attack Stage | Key Evidence |
|-----------|--------------|--------------|
| Root SSH Login from External IP | Initial Access | Successful authentication from untrusted source |
| SUID Discovery | Privilege Escalation (Recon) | Enumeration of escalation opportunities |
| Kernel Module Insertion | Persistence | malicious_mod.ko loaded for boot survival |

**Additional Hosts Investigated:**

**websrv-01:**
- Kernel module insertion detected
- Unusual command execution by ops user identified
- Similar privilege escalation pattern to app-02

**storage-01:**
- External SSH login from suspicious source IP
- Root access from untrusted network location
- Part of coordinated multi-host compromise

**app-01:**
- Root SSH login from external IP
- Multiple users added to sudoers group (Alice + additional account)
- Privilege escalation persistence confirmed

**Attack Pattern Recognition:**
All four hosts showed consistent TTPs (Tactics, Techniques, Procedures):
- External root SSH access (Initial Access)
- SUID binary discovery (Privilege Escalation reconnaissance)
- Sudoers group manipulation (Privilege Escalation execution)
- Kernel module insertion (Persistence)

This pattern indicates:
- Single threat actor or coordinated group
- Systematic infrastructure compromise
- Advanced persistent threat (APT) characteristics
- Requires organization-wide incident response

---

### Key Takeaways from Investigation

**SOC Analyst Workflow Demonstrated:**
1. ✅ Systematic triage using 4-factor model (Severity, Time, Stage, Impact)
2. ✅ Cloud SIEM navigation (Microsoft Sentinel in Azure)
3. ✅ KQL query language for deep-dive log analysis
4. ✅ Entity-based alert correlation across multiple hosts
5. ✅ Attack chain reconstruction (Initial Access → Escalation → Persistence)
6. ✅ MITRE ATT&CK framework mapping
7. ✅ Documentation for incident response escalation

**Skills Validated:**
- Microsoft Sentinel proficiency (cloud-native SIEM)
- KQL query writing and log analysis
- Multi-host incident correlation
- Privilege escalation detection and analysis
- Linux security monitoring
- SOC triage methodology in production-like environment

**Incident Response Recommendation:**
Based on investigation findings, immediate actions required:
- Isolate all four compromised hosts from network
- Preserve forensic evidence (memory dumps, disk images)
- Remove malicious kernel modules
- Audit all user accounts added to sudoers
- Reset all credentials on affected systems
- Search for lateral movement to other infrastructure
- Implement enhanced monitoring for similar attack patterns
- Block external IPs associated with initial SSH access

---

## 📚 Key Takeaways for Future Reference

### Alert Triage 4-Factor Model (Memorize This)

```
Factor 1: SEVERITY
Question: How bad is this?
Scale: Informational → Low → Medium → High → Critical
Action: Always start with High/Critical

Factor 2: TIMESTAMP & FREQUENCY
Question: When did this happen? Repeating?
Purpose: Build timeline, identify ongoing attacks
Action: Check before/after activity

Factor 3: ATTACK STAGE
Question: Where in the kill chain?
Stages: Recon → Access → Escalation → Persistence → Exfiltration
Action: Understand attacker progression

Factor 4: AFFECTED ASSET
Question: Who/what is hit?
Assessment: Criticality to business operations
Action: Prioritize high-value targets
```

### 6-Step Investigation Process (SOC Workflow)

```
1. Investigate Alert Details
   → Entities, event data, detection logic
   → Confirm malicious vs. benign

2. Check Related Logs
   → Examine log sources
   → Look for patterns

3. Correlate Multiple Alerts
   → Same user/IP/device?
   → Broader attack sequence?

4. Build Timeline
   → Combine timestamps + actions
   → Reconstruct events
   → Ongoing or contained?

5. Decide Action
   → Escalate (IOCs exist)
   → Investigate further (need more evidence)
   → Close (false positive)

6. Document
   → Analysis + decisions + remediation
   → Continuous improvement
```

### Microsoft Sentinel Navigation

**Access Path:**
```
Azure Portal → Search "Microsoft Sentinel"
→ Select Sentinel instance
→ Threat Management → Incidents tab
→ << button (expand view)
```

**Alert Detail Workflow:**
```
Incidents tab → Click alert
→ Right panel shows: events, entities, severity, tactics
→ "View full details" button
→ Incident Timeline + Similar Incidents
→ Evidence section → raw event data
```

**Switching to KQL Query Mode:**
```
Evidence section → Events
→ Simple mode dropdown (upper-right)
→ Select "KQL mode"
→ Modify query
→ Run button
```

### KQL Quick Reference (Sentinel)

**Basic Query Template:**
```kql
set query_now = datetime(YYYY-MM-DDTHH:MM:SS.MMMMMMMZ);
Syslog_CL
| where host_s == 'hostname'
| project _timestamp_t, host_s, Message
```

**Essential Operators:**
```kql
| where            # Filter
| project          # Select columns
| sort by          # Order results
| take 10          # Limit results
| summarize count  # Aggregate
```

**Common Filters:**
```kql
where host_s == 'app-02'              # Exact match
where Message contains 'sudo'          # Substring search
where _timestamp_t > datetime(...)     # Time filter
```

### Attack Chain Recognition Patterns

**Privilege Escalation Attack Sequence:**
```
Stage 1: Initial Access
- Root SSH from external IP
- Successful authentication
→ Detection: Unusual source IP, time-of-day

Stage 2: Privilege Escalation (Recon)
- SUID binary discovery
- Searching for escalation paths
→ Detection: Enumeration commands

Stage 3: Privilege Escalation (Execution)
- User added to sudoers
- Shadow file accessed
→ Detection: File modifications

Stage 4: Persistence
- Kernel module insertion
→ Detection: Unusual kernel activity
```

**Red Flags to Watch:**
- Root logins from external/unexpected IPs
- Users added to sudoers group
- Shadow file (`/etc/shadow`) access attempts
- Kernel module insertion (`insmod`, `.ko` files)
- Backup of sensitive files (`cp /etc/shadow`)

### Entity Correlation Strategy

**When Multiple Alerts Fire:**
```
Step 1: Identify common entities
- Same host?
- Same user?
- Same source IP?

Step 2: Check timestamps
- Close together? (likely same attack)
- Spread out? (different attacks or persistent threat)

Step 3: Map to attack stages
- Access → Escalation → Persistence?

Step 4: Prioritize
- Early stages + ongoing = URGENT
- Late stages + old timestamps = investigate but not emergency
```

### Linux Privilege Escalation Indicators

**Commands to Flag:**
```bash
find / -perm -4000          # SUID binary discovery
usermod -aG sudo <user>     # Add user to sudoers
echo '<user> ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers  # Sudoers modification
cp /etc/shadow              # Shadow file backup
insmod <module>.ko          # Kernel module insertion
modprobe <module>           # Kernel module loading
```

**Files to Monitor:**
```
/etc/passwd           # User accounts
/etc/shadow           # Password hashes
/etc/sudoers          # Sudo permissions
/etc/ssh/sshd_config  # SSH configuration
/lib/modules/         # Kernel modules
```

### Cloud SIEM vs. On-Prem SIEM

**Microsoft Sentinel (Cloud):**
- Azure-native integration
- KQL query language
- Cloud-scale data ingestion
- SOAR capabilities built-in
- Pay-as-you-go pricing

**Splunk (On-Prem from Day 3):**
- Self-hosted or cloud
- SPL query language
- Established market leader
- Extensive app ecosystem
- License by data volume

**Key Similarity:**
Both require systematic triage, correlation, investigation, and documentation workflows.

### SOC Analyst Daily Workflow (Based on This Challenge)

```
Morning Shift Start:
1. Check incident dashboard
2. Review overnight alerts
3. Triage by 4-factor model
4. Prioritize high-severity first

Investigation:
5. Open alert details
6. Check evidence/raw logs
7. Correlate related alerts
8. Build attack timeline
9. Validate true positive vs. false positive

Action:
10. Escalate (if IOCs found)
11. Document findings
12. Update ticket
13. Move to next alert

End of Shift:
14. Handoff notes to next shift
15. Update SOC metrics
```

### Interview Preparation — SOC Triage

**Questions to Expect:**

**Q: "How do you prioritize alerts when you have 50+ incidents?"**
A: "I use a 4-factor triage model: severity level, timestamp/frequency, attack stage, and affected asset. I start with critical/high severity, focus on alerts showing ongoing activity or late-stage attacks like persistence, and prioritize alerts affecting business-critical assets."

**Q: "Walk me through your incident investigation process."**
A: "I follow a 6-step process: [describe each step from methodology above]"

**Q: "How do you identify if multiple alerts are part of the same attack?"**
A: "I look for common entities—same host, user, or source IP. I check timestamps to see if they're close together. Then I map them to attack stages to see if they form a logical progression like initial access, privilege escalation, then persistence."

**Q: "Have you used Microsoft Sentinel?"**
A: "Yes, I have hands-on experience triaging incidents in Sentinel. I've used KQL to investigate Linux privilege escalation attacks, correlated multiple alerts across entities, and reconstructed attack timelines from raw log data."

---
