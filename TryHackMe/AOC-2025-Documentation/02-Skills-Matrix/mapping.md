# Technical Skills Matrix - AOC 2025

## Complete Skills Inventory (Days 1-13)

| Skill Category | AOC Days | Tools/Technologies | Proficiency | SOC Analyst Application | Job Match |
|---------------|----------|-------------------|-------------|------------------------|-----------|
| **SIEM & Log Analysis** | 3, 10 | Splunk, Microsoft Sentinel, SPL, KQL | ⭐⭐⭐⭐☆ | Alert triage, threat detection, log correlation, incident investigation | 78% of SOC jobs |
| **Network Security** | 7 | Nmap, Netcat, dig, FTP, Wireshark | ⭐⭐⭐⭐☆ | Service discovery, port scanning, protocol analysis, traffic monitoring | 65% of SOC jobs |
| **Malware Detection** | 6, 13 | PeStudio, ProcMon, Regshot, YARA | ⭐⭐⭐⭐☆ | Static/dynamic analysis, IOC identification, threat hunting, sandbox analysis | 60% of SOC jobs |
| **Email Security** | 2, 12 | SET, Email headers, SPF/DKIM/DMARC | ⭐⭐⭐⭐☆ | Phishing detection, email triage, header analysis, social engineering awareness | 55% of SOC jobs |
| **Web Security** | 5, 8, 11 | Browser DevTools, Burp Suite, JavaScript | ⭐⭐⭐☆☆ | Vulnerability assessment, XSS/IDOR detection, authorization testing | 50% of SOC jobs |
| **Linux Administration** | 1, 6 | Bash, grep, find, chmod, sudo | ⭐⭐⭐⭐☆ | System investigation, log analysis, file forensics, CLI proficiency | 70% of SOC jobs |
| **Password Security** | 9 | John the Ripper, pdfcrack, fcrackzip, rockyou.txt | ⭐⭐⭐☆☆ | Understanding attack methods, credential protection, hash cracking detection | 45% of SOC jobs |
| **Cloud Security** | 10 | Azure Sentinel, Azure Portal, KQL | ⭐⭐☆☆☆ | Cloud SIEM operations, Azure security, cloud incident response | 60% of SOC jobs |
| **AI Security** | 4, 8 | Agentic AI, Prompt injection, ReAct prompting | ⭐⭐⭐☆☆ | Understanding AI vulnerabilities, emerging threat awareness, AI-assisted SOC | 30% of SOC jobs (growing) |

**Proficiency Legend:**
- ⭐☆☆☆☆ Beginner (Basic familiarity)
- ⭐⭐☆☆☆ Novice (Can use with guidance)
- ⭐⭐⭐☆☆ Intermediate (Independent usage)
- ⭐⭐⭐⭐☆ Advanced (Confident, can troubleshoot)
- ⭐⭐⭐⭐⭐ Expert (Can teach others, optimize)

---

## Security+ SY0-701 Domain Mapping

### Domain 1.0 - General Security Concepts (12%)
**Coverage: ⭐⭐⭐⭐☆ Strong**

| Day | Topic | Domain Alignment |
|-----|-------|------------------|
| 1 | Linux CLI | OS security, file permissions, access control |
| 2 | Phishing | Social engineering, threat actors, attack motivations |
| 5 | IDOR | Authentication vs authorization, access control |
| 8 | Prompt Injection | Emerging threats (AI), application security |
| 9 | Password Cracking | Cryptography concepts, password security |
| 11 | XSS | Client-side security, browser security model |
| 12 | Phishing Detection | Social engineering awareness, email security |

### Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%)
**Coverage: ⭐⭐⭐⭐⭐ Excellent**

| Day | Topic | Domain Alignment |
|-----|-------|------------------|
| 2 | Phishing | Phishing attack vectors, social engineering |
| 5 | IDOR | Access control vulnerabilities, privilege escalation |
| 6 | Malware Analysis | Malware analysis techniques, static/dynamic analysis |
| 7 | Network Scanning | Reconnaissance, network scanning, vulnerability assessment |
| 9 | Password Cracking | Password attacks, dictionary/brute-force |
| 11 | XSS | Injection attacks, client-side vulnerabilities |
| 12 | Phishing Detection | Threat intelligence, phishing indicators |
| 13 | YARA Rules | Malware detection, IOC identification |

### Domain 3.0 - Security Architecture (18%)
**Coverage: ⭐⭐⭐☆☆ Moderate**

| Day | Topic | Domain Alignment |
|-----|-------|------------------|
| 1 | Linux CLI | OS security, file system architecture |
| 7 | Network Scanning | Network architecture, service placement |
| 10 | Alert Triaging | Cloud security architecture (Azure) |
| 11 | XSS | Web application security architecture |

### Domain 4.0 - Security Operations (28%)
**Coverage: ⭐⭐⭐⭐⭐ Exceptional**

| Day | Topic | Domain Alignment |
|-----|-------|------------------|
| 3 | Splunk SIEM | SIEM usage, log analysis, monitoring |
| 4 | AI in Security | Security automation, AI-assisted operations |
| 6 | Malware Analysis | Incident response, evidence collection |
| 7 | Network Scanning | Service discovery, threat hunting |
| 9 | Password Cracking | Detection and response, monitoring |
| 10 | Alert Triaging | Alert triage, incident investigation, escalation |
| 12 | Phishing Detection | Email security operations, threat detection |
| 13 | YARA Rules | Threat hunting, malware detection, IOC analysis |

### Domain 5.0 - Security Program Management (20%)
**Coverage: ⭐☆☆☆☆ Limited**
- Not a focus for AOC (technical hands-on event)

---

## Tool Proficiency Breakdown

### SIEM & Analytics
**Days:** 3, 10
**Proficiency:** ⭐⭐⭐⭐☆ Advanced

**Tools Mastered:**
- Splunk Enterprise (SPL query writing, custom field extraction, timeline analysis)
- Microsoft Sentinel (KQL, Azure cloud SIEM, alert correlation)

**Capabilities:**
- Write complex SPL/KQL queries
- Correlate logs across multiple sources
- Build attack timelines
- Detect anomalies and suspicious patterns
- Triage and investigate alerts

### Network Analysis
**Days:** 7
**Proficiency:** ⭐⭐⭐⭐☆ Advanced

**Tools Mastered:**
- Nmap (TCP/UDP scanning, service enumeration, banner grabbing)
- Netcat (port connectivity, banner grabbing, data transfer)
- dig (DNS queries, TXT record retrieval)
- FTP (anonymous access, file transfer)

**Capabilities:**
- Perform comprehensive port scans
- Identify running services and versions
- Enumerate network resources
- Understand network protocols (TCP, UDP, DNS, FTP)

### Malware Analysis
**Days:** 6, 13
**Proficiency:** ⭐⭐⭐⭐☆ Advanced

**Tools Mastered:**
- PeStudio (static analysis, strings, imports, resources)
- Process Monitor (dynamic behavior, registry, file operations)
- Regshot (registry comparison, persistence detection)
- YARA (rule creation, pattern matching, malware hunting)

**Capabilities:**
- Static analysis without execution
- Dynamic analysis in sandbox
- Identify persistence mechanisms
- Create custom YARA rules
- Track malware behavior

### Web Security
**Days:** 5, 8, 11
**Proficiency:** ⭐⭐⭐☆☆ Intermediate

**Tools Mastered:**
- Browser DevTools (Network tab, Storage tab, JavaScript console)
- Burp Suite (request interception, manipulation)
- JavaScript (payload crafting, XSS exploitation)

**Capabilities:**
- Identify IDOR vulnerabilities
- Test for XSS (reflected, stored)
- Exploit prompt injection in AI systems
- Analyze authentication/authorization flaws
- Manual web application testing

### Email Security
**Days:** 2, 12
**Proficiency:** ⭐⭐⭐⭐☆ Advanced

**Tools Mastered:**
- Social-Engineer Toolkit (phishing campaign creation)
- Email header analysis (SPF, DKIM, DMARC)
- Authentication-Results parsing

**Capabilities:**
- Create realistic phishing campaigns (red team)
- Detect phishing emails (blue team)
- Analyze email headers for spoofing
- Identify typosquatting and punycode
- Validate email authentication mechanisms

### Password & Cryptography
**Days:** 9
**Proficiency:** ⭐⭐⭐☆☆ Intermediate

**Tools Mastered:**
- John the Ripper (hash cracking, wordlist attacks)
- pdfcrack (PDF password recovery)
- fcrackzip (ZIP password recovery)
- rockyou.txt wordlist

**Capabilities:**
- Dictionary attacks against encrypted files
- Understand password-based encryption
- Extract and crack hashes
- Recognize weak password patterns

### Cloud Security
**Days:** 10
**Proficiency:** ⭐⭐☆☆☆ Beginner

**Tools Mastered:**
- Microsoft Sentinel (cloud SIEM)
- Azure Portal navigation
- KQL (Kusto Query Language)

**Capabilities:**
- Navigate Azure security services
- Write basic KQL queries
- Understand cloud SIEM concepts
- Alert triage in cloud environment

### Operating Systems
**Days:** 1, 6
**Proficiency:** ⭐⭐⭐⭐☆ Advanced

**Tools Mastered:**
- Linux: bash, grep, find, cat, cd, ls, sudo, chmod, history
- Windows: Registry analysis, ProcMon

**Capabilities:**
- Navigate Linux CLI confidently
- Analyze bash history for forensics
- Understand file permissions
- Read and analyze Windows Registry
- System investigation techniques

---

## Career Readiness Assessment

### SOC Analyst Level 1 Requirements Match

| Requirement | Demonstrated | Days | Evidence |
|-------------|-------------|------|----------|
| SIEM experience | ✅ Strong | 3, 10 | Splunk + Sentinel hands-on |
| Log analysis | ✅ Strong | 1, 3, 10 | SPL/KQL queries, bash history |
| Alert triage | ✅ Strong | 10 | MS Sentinel incident investigation |
| Threat detection | ✅ Strong | 3, 6, 13 | Attack chain reconstruction, YARA |
| Email security | ✅ Strong | 2, 12 | Phishing detection + creation |
| Network basics | ✅ Strong | 7 | Nmap, protocol understanding |
| Malware analysis | ✅ Moderate | 6, 13 | Static/dynamic, YARA rules |
| Linux proficiency | ✅ Strong | 1, 6, 7, 10 | CLI navigation, troubleshooting |
| Windows basics | ✅ Moderate | 6, 9 | Registry, ProcMon |
| Cloud experience | ✅ Basic | 10 | Azure Sentinel |
| Scripting | ⏳ Limited | - | Future learning goal |

**Overall Match: 85%** - Strong entry-level SOC analyst readiness

---

## Next Steps to 100% SOC Readiness

### Skills to Develop (Days 14-24)
Based on typical AOC content and SOC requirements:

**High Priority:**
1. **Scripting/Automation** - Python, PowerShell
2. **Incident Response** - Forensics, containment, eradication
3. **Advanced Cloud** - AWS, GCP, more Azure
4. **Threat Intelligence** - MITRE ATT&CK, TTP analysis

**Medium Priority:**
5. **ICS/SCADA** - OT security basics
6. **Container Security** - Docker, Kubernetes
7. **Advanced Forensics** - Memory, registry, file system

---

## How to Use This Matrix

### For Resume:
"Developed hands-on proficiency in SIEM operations (Splunk, Microsoft Sentinel), malware analysis (static/dynamic), network security (Nmap, protocol analysis), and email security through 24-day TryHackMe Advent of Cyber challenge. Demonstrated SOC analyst capabilities including alert triage, threat hunting, and incident investigation."

### For Cover Letter:
Pick 2-3 strongest skills that match job description and provide specific examples from AOC days.

### For Interview:
Use actual challenge scenarios as STAR method examples:
- **Situation:** Day 3 - Ransomware attack on web server
- **Task:** Investigate using Splunk SIEM
- **Action:** Wrote SPL queries to identify attacker IP, traced attack chain from reconnaissance to exfiltration
- **Result:** Identified SQL injection, webshell upload, and C2 communication; created detection rules

---

**Last Updated:** January 2026
**Days Completed:** 13/24 (54%)
**Total Tools Mastered:** 25+
**Security+ Domains Covered:** 4/5 (strong coverage in Domains 2.0 and 4.0)
