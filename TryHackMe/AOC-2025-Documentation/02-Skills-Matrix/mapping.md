
---

## 📋 Template 4: Skills Matrix

```markdown
# Skills Matrix - AOC 2025

## Overview

This document maps all skills gained during TryHackMe's Advent of Cyber 2025 to:
1. SOC Analyst job requirements
2. Security+ SY0-701 certification domains
3. Industry-standard tools and frameworks

---

## SOC Analyst Skills Mapping

| Skill Category | AOC Days | Tools/Technologies | Proficiency Level | SOC Application | Job Requirement Match |
|---------------|----------|-------------------|-------------------|-----------------|----------------------|
| **SIEM & Log Analysis** | 3, 10, 22 | Splunk, Microsoft Sentinel | ⭐⭐⭐⭐☆ | Alert triage, threat detection, log correlation | 78% of SOC job postings |
| **Network Analysis** | 7, 22 | Nmap, Wireshark | ⭐⭐⭐☆☆ | Traffic analysis, service discovery, protocol understanding | 65% of SOC job postings |
| **Incident Response** | 3, 10, 22 | SIEM platforms, investigation workflows | ⭐⭐⭐☆☆ | Alert escalation, incident investigation, documentation | 85% of SOC job postings |
| **Threat Hunting** | 3, 22 | Splunk, log analysis tools | ⭐⭐⭐☆☆ | Proactive threat detection, C2 identification | 45% of SOC job postings |
| **Linux Administration** | 1 | Bash, command-line tools | ⭐⭐⭐⭐☆ | System investigation, log analysis, file navigation | 70% of SOC job postings |
| **Cloud Security** | 10 | Microsoft Azure, Sentinel | ⭐⭐☆☆☆ | Cloud-based SIEM, Azure security services | 60% of SOC job postings |
| **Web Security** | 5, 11, 24 | cURL, browser developer tools | ⭐⭐⭐☆☆ | Web vulnerability analysis, API testing | 50% of SOC job postings |
| **Social Engineering** | 2 | Social-Engineer Toolkit | ⭐⭐⭐☆☆ | Phishing detection, security awareness | 55% of SOC job postings |
| **Attack Analysis** | 2, 5, 11, 24 | Various exploitation tools | ⭐⭐⭐☆☆ | Understanding attacker TTPs, vulnerability assessment | 70% of SOC job postings |

**Proficiency Legend:**
- ⭐☆☆☆☆ - Awareness (heard of it)
- ⭐⭐☆☆☆ - Novice (basic understanding)
- ⭐⭐⭐☆☆ - Intermediate (can use with guidance)
- ⭐⭐⭐⭐☆ - Proficient (independent usage)
- ⭐⭐⭐⭐⭐ - Expert (can teach others)

---

## Security+ SY0-701 Domain Alignment

### Domain 1.0 - General Security Concepts (12%)

| AOC Day | Topic | Security+ Objective | Skills Gained |
|---------|-------|-------------------|---------------|
| 2 | Phishing | 1.2 - Threat actors and motivations | Social engineering tactics, attack vectors |
| 5 | IDOR | 1.3 - Security concepts | Authentication, authorization, access control |
| 11 | XSS | 1.4 - Security controls | Input validation, client-side security |

**Coverage Assessment:** ⭐⭐⭐⭐☆ (Strong coverage of core concepts)

---

### Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%)

| AOC Day | Topic | Security+ Objective | Skills Gained |
|---------|-------|-------------------|---------------|
| 2 | Phishing | 2.2 - Threat intelligence | Phishing campaign analysis, social engineering |
| 5 | IDOR | 2.3 - Vulnerability types | Access control vulnerabilities |
| 7 | Network Discovery | 2.4 - Reconnaissance | Network scanning, service enumeration |
| 11 | XSS | 2.3 - Vulnerability types | Injection attacks, web vulnerabilities |
| 24 | cURL Exploitation | 2.3 - Vulnerability types | Web exploitation, API security |

**Coverage Assessment:** ⭐⭐⭐⭐⭐ (Excellent practical coverage)

---

### Domain 3.0 - Security Architecture (18%)

| AOC Day | Topic | Security+ Objective | Skills Gained |
|---------|-------|-------------------|---------------|
| 7 | Network Discovery | 3.1 - Network security | Network architecture, service placement |
| 10 | Azure Sentinel | 3.3 - Cloud security | Cloud-based security services, Azure architecture |

**Coverage Assessment:** ⭐⭐⭐☆☆ (Moderate coverage, cloud focus)

---

### Domain 4.0 - Security Operations (28%)

| AOC Day | Topic | Security+ Objective | Skills Gained |
|---------|-------|-------------------|---------------|
| 3 | Splunk Basics | 4.1 - Security operations | SIEM usage, log analysis, monitoring |
| 10 | SOC Alert Triage | 4.3 - Incident response | Alert triage, investigation, escalation |
| 22 | C2 Detection | 4.5 - Threat hunting | Proactive threat detection, traffic analysis |

**Coverage Assessment:** ⭐⭐⭐⭐⭐ (Exceptional hands-on experience)

---

### Domain 5.0 - Security Program Management (20%)

| AOC Day | Topic | Security+ Objective | Skills Gained |
|---------|-------|-------------------|---------------|
| - | [Coverage needed] | 5.1 - Governance | Limited direct coverage |

**Coverage Assessment:** ⭐⭐☆☆☆ (Area for future development)

---

## Tool Proficiency Matrix

### SIEM Platforms

| Tool | Proficiency | AOC Days Used | Key Capabilities | Real-World Usage |
|------|------------|---------------|------------------|------------------|
| **Splunk** | ⭐⭐⭐⭐☆ | 3, 22 | SPL queries, log ingestion, dashboard creation, anomaly detection | Industry-standard SIEM, used by 60% of enterprises |
| **Microsoft Sentinel** | ⭐⭐⭐☆☆ | 10 | Cloud-based SIEM, Azure integration, alert triage | Growing adoption in cloud-first organizations |

---

### Network Tools

| Tool | Proficiency | AOC Days Used | Key Capabilities | Real-World Usage |
|------|------------|---------------|------------------|------------------|
| **Nmap** | ⭐⭐⭐⭐☆ | 7 | Port scanning, service discovery, OS detection | Standard reconnaissance tool for both red/blue teams |
| **Wireshark** | ⭐⭐⭐☆☆ | [If used] | Packet analysis, protocol inspection | Essential for network troubleshooting and forensics |

---

### Operating Systems

| System | Proficiency | AOC Days Used | Key Capabilities | Real-World Usage |
|--------|------------|---------------|------------------|------------------|
| **Linux CLI** | ⭐⭐⭐⭐☆ | 1, [others] | File navigation, text processing, system administration | Critical for SOC analysts - 90% of security tools run on Linux |
| **Windows** | ⭐⭐⭐☆☆ | [If covered] | Event logs, PowerShell, system investigation | 70% of enterprise endpoints run Windows |

---

### Web Security Tools

| Tool | Proficiency | AOC Days Used | Key Capabilities | Real-World Usage |
|------|------------|---------------|------------------|------------------|
| **cURL** | ⭐⭐⭐⭐☆ | 24 | API testing, HTTP request crafting, web exploitation | Essential for API security testing and automation |
| **Browser DevTools** | ⭐⭐⭐☆☆ | 5, 11 | JavaScript debugging, network inspection, DOM manipulation | Standard for web application testing |

---

### Cloud Platforms

| Platform | Proficiency | AOC Days Used | Key Capabilities | Real-World Usage |
|----------|------------|---------------|------------------|------------------|
| **Microsoft Azure** | ⭐⭐☆☆☆ | 10 | Security services, Sentinel, identity management | Second-largest cloud provider, growing enterprise adoption |

---

## Skill Development Timeline

### Week 1 (Days 1-6)
**Focus:** Foundations
- Linux fundamentals
- Phishing and social engineering
- Splunk basics
- IDOR vulnerabilities

**Proficiency Growth:** ⭐☆☆☆☆ → ⭐⭐⭐☆☆

---

### Week 2 (Days 7-12)
**Focus:** Network & Web Security
- Network discovery with Nmap
- SOC alert triage
- XSS vulnerabilities

**Proficiency Growth:** ⭐⭐⭐☆☆ → ⭐⭐⭐⭐☆

---

### Week 3 (Days 13-18)
**Focus:** [To be filled based on actual challenges]

---

### Week 4 (Days 19-24)
**Focus:** Advanced Topics
- C2 detection
- Web exploitation with cURL

**Proficiency Growth:** ⭐⭐⭐⭐☆ → ⭐⭐⭐⭐⭐

---

## MITRE ATT&CK Framework Coverage

### Tactics Covered

| Tactic | AOC Days | Techniques Learned | Defensive Application |
|--------|----------|-------------------|----------------------|
| **Initial Access** | 2 | T1566 (Phishing) | Email security, user training |
| **Execution** | [Day] | [Technique] | Endpoint detection |
| **Persistence** | [Day] | [Technique] | Monitoring, detection |
| **Discovery** | 7 | T1046 (Network Service Discovery) | Network monitoring, anomaly detection |
| **Command & Control** | 22 | T1071 (Application Layer Protocol) | Traffic analysis, C2 detection |
| **Exfiltration** | 3 | [Technique] | Data loss prevention, network monitoring |

---

## Gap Analysis & Future Development

### Strong Areas (⭐⭐⭐⭐+)
- SIEM operations (Splunk)
- Linux command-line
- Log analysis
- Network scanning

### Areas for Improvement (⭐⭐⭐☆☆ or below)
- Cloud security (Azure, AWS)
- Malware analysis
- Forensics tools (Volatility, Autopsy)
- Programming/scripting (Python, PowerShell)

### Recommended Next Steps
1. **TryHackMe SOC Level 1 Path** - Deepen defensive skills
2. **Security+ Certification** - Validate foundational knowledge
3. **Cloud Security Labs** - Strengthen Azure/AWS skills
4. **Home Lab Setup** - Continue practical learning
5. **Python for Security** - Develop automation skills

---

## Employer Value Proposition

### What I Can Do Today
✅ Triage and investigate SOC alerts using SIEM platforms
✅ Analyze logs to identify suspicious activity and attack patterns
✅ Perform network reconnaissance and service discovery
✅ Understand common web vulnerabilities and exploitation techniques
✅ Document investigation findings clearly and professionally
✅ Work comfortably in Linux command-line environments

### What I'm Actively Developing
🔄 Advanced threat hunting methodologies
🔄 Cloud security operations (Azure/AWS)
🔄 Automation and scripting for repetitive tasks
🔄 Malware analysis and reverse engineering basics
🔄 Security+ certification preparation

### Growth Trajectory
📈 Novice → Intermediate in 4 weeks (AOC 2025)
📈 Target: Intermediate → Proficient in 3 months (Security+ + SOC Level 1)
📈 Goal: Job-ready SOC Analyst by Q2 2026

---

*Last Updated: January 2026*
*Based on TryHackMe Advent of Cyber 2025 completion*
