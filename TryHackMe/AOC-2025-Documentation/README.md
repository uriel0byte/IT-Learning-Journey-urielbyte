# TryHackMe Advent of Cyber 2025 - Complete Documentation

![AOC 2025 Certificate](./09-Certificates/aoc-2025-certificate.png)

[![Days Completed](https://img.shields.io/badge/Days%20Completed-24%2F24-success)]()
[![Certificate](https://img.shields.io/badge/Certificate-Earned-blue)]()
[![Event](https://img.shields.io/badge/Event-December%202025-orange)]()

## Quick Stats

- **Status:** Days 1-13 Complete | Days 14-24 In Progress
- **Start Date:** December 1, 2025
- **Completion:** 54% (13/24 days)
- **Tools Mastered:** 25+
- **Categories:** SIEM, Malware Analysis, Web Security, Cloud, AI Security

---

## 🎯 Overview

I completed TryHackMe's **Advent of Cyber 2025**—a 24-day intensive cybersecurity challenge that ran throughout December 2025. This repository documents my learning journey, practical skills gained, and how these experiences align with my Security+ certification goals and aspiration to become a SOC Analyst.

### What is Advent of Cyber?

Advent of Cyber is TryHackMe's annual beginner-friendly cybersecurity event featuring daily hands-on challenges. The 2025 event covered offensive security, defensive security, DFIR, and cloud security with a focus on real-world scenarios.

### My Achievement

- ✅ Completed all 24 daily challenges
- ✅ Earned certificate of completion
- ✅ Invested 60+ hours in practical cybersecurity training
- ✅ Gained hands-on experience with 15+ industry-standard security tools
- ✅ Developed skills directly applicable to SOC Analyst roles

## 📊 Skills Developed (Days 1-13)

### Defensive Security
![SIEM](https://img.shields.io/badge/SIEM-Splunk%20%26%20Sentinel-green)
![Alert Triage](https://img.shields.io/badge/SOC-Alert%20Triage-blue)
![Email Security](https://img.shields.io/badge/Email-Phishing%20Detection-purple)
![YARA](https://img.shields.io/badge/Detection-YARA%20Rules-orange)
- SIEM (Splunk, Microsoft Sentinel) - Days 3, 10
- Email Security (Phishing Detection) - Days 2, 12
- Alert Triaging (Azure Sentinel) - Day 10
- YARA Rules (Malware Detection) - Day 13

### Offensive Security
![Phishing](https://img.shields.io/badge/Social-Engineering-red)
![Web Exploitation](https://img.shields.io/badge/Web-XSS%20%26%20IDOR-red)
![Network Scanning](https://img.shields.io/badge/Network-Nmap-yellow)
- Phishing Campaigns (SET) - Day 2
- Web Exploitation (XSS, IDOR) - Days 5, 11
- Network Scanning (Nmap) - Day 7

### DFIR & Malware
![Malware Analysis](https://img.shields.io/badge/Malware-Static%20%26%20Dynamic-darkred)
![YARA](https://img.shields.io/badge/Detection-YARA-orange)
- Static/Dynamic Analysis (PeStudio, ProcMon) - Day 6
- YARA Pattern Matching - Day 13


### Emerging Tech
![AI Security](https://img.shields.io/badge/AI-Security%20%26%20Exploitation-lightblue)
- AI Security & Exploitation - Days 4, 8

### Tools & Technologies
![Linux](https://img.shields.io/badge/Linux-CLI-black)
![Cloud](https://img.shields.io/badge/Cloud-Azure%20Sentinel-blue)
![Password Cracking](https://img.shields.io/badge/Passwords-John%20%26%20Hashcat-darkgreen)


## 📖 Repository Structure

```
/AOC-2025-Documentation
│
├── README.md (This file)
├── /01-Executive-Summary
│   └── overview.md
├── /02-Skills-Matrix
│   └── mapping.md
├── /03-Daily-Challenges
│   ├── day-01-linux-cli.md
│   ├── day-02-phishing.md
│   ├── ... (all 24 days)
│   └── day-24-curl-exploitation.md
├── /04-Case-Studies
│   ├── case-study-splunk-log-analysis.md
│   ├── case-study-soc-alert-triage.md
│   └── case-study-network-discovery.md
├── /05-Technical-Skills
│   └── tools-inventory.md
├── /06-Learning-Journey
│   ├── narrative.md
│   └── reflections.md
├── /07-Screenshots
│   ├── day-01/
│   └── ... (organized by day)
├── /08-Resources
│   └── references.md
└── /09-Certificates
    └── aoc-2025-certificate.pdf
```

## 🎯 Highlighted Case Studies

### [Day 3: Splunk Log Analysis - Did you SIEM?](./04-Case-Studies/case-study-splunk-log-analysis.md)
Analyzed web traffic and firewall logs using Splunk, identified attack chains from reconnaissance to data exfiltration, and detected SQL injection and ransomware staging attempts.

**Skills:** SPL (Search Processing Language), anomaly detection, log correlation, incident investigation

### [Day 10: SOC Alert Triaging](./04-Case-Studies/case-study-soc-alert-triage.md)
Practiced real SOC analyst workflows using Microsoft Sentinel for alert prioritization and investigation in cloud environments.

**Skills:** SIEM analysis, alert triage, Azure security, incident escalation

### [Day 7: Network Discovery with Nmap](./04-Case-Studies/case-study-network-discovery.md)
Performed network reconnaissance using Nmap to discover services, identify open ports, and map network infrastructure.

**Skills:** Network scanning, service enumeration, protocol analysis, reconnaissance

## 🛠️ Technical Skills Inventory

### SIEM & Log Analysis
- Splunk (SPL queries, dashboard creation, log correlation)
- Microsoft Sentinel (Azure-based SIEM)
- Anomaly detection and pattern recognition
- Alert triage and investigation

### Network Security
- Nmap (port scanning, service discovery)
- Wireshark (packet analysis)
- Network protocol understanding
- Traffic pattern analysis

### Offensive Security
- Web exploitation techniques
- IDOR vulnerabilities
- XSS (Cross-Site Scripting)
- Phishing campaign creation
- Social engineering tactics

### Cloud Security
- Microsoft Azure security services
- Cloud-based SIEM operations
- AWS security fundamentals

### Operating Systems
- Linux command-line interface
- Windows security concepts
- System administration tasks

### Incident Response
- Attack chain analysis
- Threat hunting methodologies
- C2 (Command & Control) detection
- Forensic investigation techniques

## 🎓 Security+ SY0-701 Connection

This documentation demonstrates practical application of Security+ domains:

- **Domain 1.0** (12%): Social engineering, authentication, authorization, cryptography
- **Domain 2.0** (22%): Phishing, malware, vulnerabilities, password attacks, injection
- **Domain 3.0** (18%): OS security, network architecture, cloud security, web apps
- **Domain 4.0** (28%): **SIEM, log analysis, alert triage, incident response, threat hunting**
- **Domain 5.0** (20%): Limited coverage (technical focus)

**Strong Coverage:** Domains 2.0 and 4.0 = **50% of Security+ exam weight**


## 📈 Security+ Certification Alignment

This AOC 2025 experience directly supports my Security+ (SY0-701) preparation:

| Security+ Domain | AOC Days | Skills Gained |
|-----------------|----------|---------------|
| **Domain 1.0** - General Security Concepts | Days 2, 5, 11 | Authentication, authorization, attack types |
| **Domain 2.0** - Threats & Vulnerabilities | Days 2, 5, 11, 24 | Phishing, XSS, IDOR, web exploitation |
| **Domain 3.0** - Security Architecture | Days 7, 10 | Network architecture, cloud security |
| **Domain 4.0** - Security Operations | Days 3, 10, 22 | SIEM, alert triage, threat hunting, C2 detection |

## 📝 Learning Journey

### Why I Participated
As an ILS student transitioning to cybersecurity, I needed practical, hands-on experience to complement my Security+ theoretical studies. AOC 2025 provided structured daily challenges that built progressively from foundational to advanced concepts.

### What I Learned
- **Technical Skills:** SIEM operations, log analysis, network scanning, web exploitation
- **Problem-Solving:** Systematic investigation methodologies, attack chain analysis
- **Professional Skills:** Documentation, technical writing, time management
- **Tool Proficiency:** Splunk, Nmap, Wireshark, cURL, Azure Sentinel

### Growth & Challenges
The event started with accessible Linux basics and gradually increased in complexity. Days 3 (Splunk) and 10 (Azure Sentinel) were particularly challenging, requiring deeper understanding of log correlation and cloud security. These challenges pushed me to research extensively and develop persistence when facing obstacles.

### Connection to Career Goals
Every skill learned aligns directly with SOC Analyst responsibilities: alert triage, log analysis, incident investigation, and threat detection. This practical experience complements my Security+ preparation and demonstrates to recruiters that I can apply theoretical knowledge in real scenarios.

## 📊 Quantifiable Achievements

- ✅ Completed 24 consecutive daily challenges
- ✅ Analyzed 100+ security scenarios across multiple attack vectors
- ✅ Gained hands-on experience with 15+ security tools
- ✅ Invested 60+ hours in practical cybersecurity training
- ✅ Documented comprehensive portfolio with 10,000+ words
- ✅ Created 5+ detailed case studies demonstrating analytical skills
- ✅ Investigated 24 mock security incidents from detection to resolution

## 📊 Challenge Overview (Days 1-13 Detailed)

| Day | Title | Category | Difficulty | Tools | Status |
|-----|-------|----------|------------|-------|--------|
| 1 | Linux CLI | Foundational | ★☆☆☆ | Bash, grep, find | ✅ Complete |
| 2 | Phishing | Offensive | ★★☆☆ | SET, SMTP | ✅ Complete |
| 3 | Splunk SIEM | Defensive | ★★★☆ | Splunk, SPL | ✅ Complete |
| 4 | AI in Security | Emerging Tech | ★★★☆ | AI agents | ✅ Complete |
| 5 | IDOR | Web Security | ★★★☆ | DevTools, Burp | ✅ Complete |
| 6 | Malware Analysis | DFIR | ★★★☆ | PeStudio, ProcMon | ✅ Complete |
| 7 | Network Scanning | Network Sec | ★★☆☆ | Nmap, Netcat | ✅ Complete |
| 8 | Prompt Injection | AI Security | ★★★☆ | Agentic AI | ✅ Complete |
| 9 | Password Cracking | Cryptography | ★★★☆ | John, pdfcrack | ✅ Complete |
| 10 | Alert Triaging | Cloud SIEM | ★★★★ | MS Sentinel, KQL | ✅ Complete |
| 11 | XSS | Web Security | ★★★☆ | Browser DevTools | ✅ Complete |
| 12 | Phishing Detection | Email Security | ★★★☆ | Email headers | ✅ Complete |
| 13 | YARA Rules | DFIR | ★★★☆ | YARA engine | ✅ Complete |
| 14-24 | TBD | Various | TBD | TBD | 🔄 In Progress |

**Legend:** ★☆☆☆ Easy | ★★☆☆ Easy-Medium | ★★★☆ Medium | ★★★★ Medium-Hard

---

## 🔗 Connect With Me

- **GitHub:** [github.com/uriel0byte](https://github.com/uriel0byte)
- **LinkedIn:** []
- **TryHackMe:** []
- **Email:** poseidon.smash@gmail.com

## 📜 License

This documentation is for educational and portfolio purposes. All challenges and content belong to TryHackMe. No flags or direct solutions are shared in compliance with TryHackMe's policies.

---

*Last Updated: January, 15 2026*
