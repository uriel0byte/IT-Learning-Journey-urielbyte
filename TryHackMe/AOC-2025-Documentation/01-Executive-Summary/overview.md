# Executive Summary - TryHackMe Advent of Cyber 2025

## Overview

This document provides an expanded executive summary of my completion of TryHackMe's Advent of Cyber 2025, a 24-day intensive cybersecurity challenge that took place throughout December 2025. This portfolio demonstrates practical, hands-on skills applicable to Security Operations Center (SOC) Analyst positions and validates my commitment to entering the cybersecurity field.

---

## Event Background

### What is Advent of Cyber?

Advent of Cyber is TryHackMe's flagship annual cybersecurity event designed to make security training accessible and engaging through daily hands-on challenges. The 2025 edition featured:

- **Duration:** 24 days (December 1-31, 2025)
- **Accessibility:** Free participation, beginner-friendly
- **Format:** Daily challenges released at 4pm GMT
- **Prize Pool:** $150,000+ in prizes
- **Completion Certificate:** Awarded for finishing all challenges
- **Global Participation:** Thousands of participants worldwide

### Event Scope

The 2025 event covered a comprehensive range of cybersecurity domains:

**Defensive Security:**
- SIEM operations and log analysis
- SOC alert triage and investigation
- Digital forensics and incident response (DFIR)
- Threat hunting methodologies
- Security monitoring
- C2 beacon detection and analysis

**Offensive Security:**
- Web application exploitation
- Network reconnaissance
- Social engineering and phishing
- Vulnerability assessment
- API security testing
- Command-line exploitation

**Cloud Security:**
- Microsoft Azure security services
- Cloud-based SIEM (Microsoft Sentinel)
- AWS IAM and S3 security
- Container security (Docker)
- Cloud infrastructure protection

**Emerging Technologies:**
- AI agents in security operations
- Automated vulnerability detection
- Machine learning for threat detection
- Prompt injection attacks

**ICS/OT Security:**
- SCADA systems
- PLC operations
- Modbus protocol
- Industrial control systems

---

## My Achievement

### Completion Status

✅ **24/24 days completed** (100% completion rate)  
✅ **Certificate of completion earned**  
✅ **All challenges solved independently**  
✅ **Comprehensive documentation created**

### Time Investment

- **Total hours:** 60+ hours of hands-on training
- **Daily commitment:** 2-3 hours per challenge
- **Documentation:** 45+ additional hours creating this portfolio
- **Period:** December 1-31, 2025 (plus January 2026 for documentation)

### Personal Context

I completed this challenge while:
- Pursuing Security+ certification (SY0-701)
- Transitioning from ILS studies to cybersecurity career
- Balancing academic commitments
- Managing time during the holiday season

This demonstrates my ability to maintain consistency, manage competing priorities, and commit to professional development even during challenging periods.

---

## Key Skills Developed

### SIEM & Log Analysis (Primary Focus)
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **Splunk:** Search Processing Language (SPL), dashboard creation, log ingestion, anomaly detection
- **Microsoft Sentinel:** Cloud-based SIEM operations, Azure integration, alert triage
- **RITA & Zeek:** C2 detection, network traffic analysis, PCAP processing
- **Log Correlation:** Identifying attack chains across multiple data sources
- **Anomaly Detection:** Spotting suspicious patterns in large datasets
- **Incident Investigation:** Tracing attacker activity from initial access to exfiltration

**Real-World Application:** These skills directly address the #1 requirement in SOC Analyst job postings, which mention SIEM expertise in 78% of listings.

**Covered in:** Days 3, 10, 15, 22

---

### Network Security & Analysis
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **Nmap:** Port scanning, service discovery, OS detection, network mapping
- **Wireshark:** Packet capture analysis, protocol inspection
- **RITA:** Beacon detection, threat hunting on network traffic
- **Zeek:** Network monitoring, connection analysis, IDS capabilities
- **Network Protocols:** TCP/IP, HTTP, MQTT, understanding of OSI model
- **Service Enumeration:** Identifying running services and potential vulnerabilities
- **Traffic Analysis:** Detecting C2 (Command & Control) communications

**Real-World Application:** Essential for understanding network-based attacks and defending infrastructure.

**Covered in:** Days 7, 22, 24

---

### Web Application Security
**Proficiency Level:** ⭐⭐⭐☆☆ (Intermediate)

- **IDOR Vulnerabilities:** Understanding access control weaknesses
- **XSS (Cross-Site Scripting):** Client-side injection attacks, payload crafting
- **Race Conditions:** Timing attacks, parallel request exploitation
- **cURL Exploitation:** Direct HTTP manipulation, API testing
- **Web Forensics:** Analyzing web attack patterns in logs (Apache + Sysmon)
- **Authentication/Authorization:** Security model understanding

**Real-World Application:** Web applications are the #1 attack surface for modern organizations.

**Covered in:** Days 5, 11, 15, 20, 24

---

### Social Engineering & Phishing
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **Phishing Campaign Creation:** Using Social-Engineer Toolkit (SET)
- **Social Engineering Tactics:** Understanding psychological manipulation
- **Detection Techniques:** Identifying phishing indicators, email header analysis
- **Email Forensics:** SPF/DKIM/DMARC validation, spoofing detection
- **Security Awareness:** User training concepts

**Real-World Application:** Phishing is involved in 90% of successful breaches.

**Covered in:** Days 2, 12

---

### Digital Forensics & Incident Response
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **Windows Registry Forensics:** Registry Explorer, hive analysis, persistence detection
- **Web Attack Forensics:** Apache logs, Sysmon correlation, command injection detection
- **Malware Analysis:** HTA files, VBScript analysis, static analysis techniques
- **Code Deobfuscation:** PowerShell, Base64, XOR, ROT13, multi-layer decoding
- **C2 Detection:** RITA, Zeek, beacon analysis, DNS tunneling identification
- **Attack Chain Reconstruction:** Identifying attacker progression through logs

**Real-World Application:** DFIR skills are critical for incident response teams and SOC escalation paths.

**Covered in:** Days 15, 16, 18, 21, 22

---

### Malware Analysis & Detection
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **Static Analysis:** PeStudio, strings analysis, PE headers, imports/exports examination
- **Dynamic Analysis:** Process Monitor, Regshot, sandbox analysis, behavior tracking
- **YARA Rules:** Pattern matching, IOC identification, threat hunting, custom rule creation
- **Persistence Detection:** Registry analysis, startup locations, scheduled tasks
- **HTA Malware:** HTML Application analysis, embedded VBScript detection

**Real-World Application:** Essential for malware triage and threat intelligence operations.

**Covered in:** Days 6, 13, 21

---

### Cryptography & Encoding
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **CyberChef:** Multi-layer deobfuscation, encoding chains, cryptographic operations
- **Encoding Schemes:** Base64, XOR, ROT13, URL encoding, hexadecimal
- **Password Cracking:** John the Ripper, dictionary attacks, wordlist usage (rockyou.txt)
- **File Encryption:** pdfcrack, fcrackzip, attacking password-protected files
- **Hash Analysis:** Understanding password-based encryption, hash identification

**Real-World Application:** Understanding encoding is essential for malware analysis and data exfiltration detection.

**Covered in:** Days 9, 17, 18, 21

---

### Cloud Security (AWS + Azure)
**Proficiency Level:** ⭐⭐⭐☆☆ (Intermediate)

- **AWS IAM:** Privilege escalation, role assumption (AssumeRole), policy analysis
- **AWS S3:** Bucket enumeration, data exfiltration, misconfiguration detection
- **Microsoft Azure:** Basic navigation, service understanding, Azure security services
- **Azure Sentinel:** Cloud-native SIEM operations, KQL queries
- **Container Security:** Docker escape techniques, daemon API exploitation
- **Cloud Security Concepts:** Shared responsibility model, cloud-specific threats

**Real-World Application:** Cloud security is now essential as 95% of organizations use multi-cloud environments.

**Covered in:** Days 10, 14, 23

---

### ICS/OT Security
**Proficiency Level:** ⭐⭐☆☆☆ (Novice-Intermediate)

- **SCADA Systems:** Understanding industrial control systems, operational technology
- **PLC Operations:** Programmable Logic Controller basics, functionality
- **Modbus TCP Protocol:** Reading/writing coils, holding registers, protocol interaction
- **Python for ICS:** Using pymodbus library for protocol automation
- **Industrial Security:** Understanding attacks on critical infrastructure

**Real-World Application:** Critical infrastructure protection is increasingly important as ICS/OT systems face cyber threats.

**Covered in:** Day 19

---

### AI Security & Emerging Threats
**Proficiency Level:** ⭐⭐⭐☆☆ (Intermediate)

- **AI for Red Team:** Exploit generation, attack automation
- **AI for Blue Team:** Log analysis, anomaly detection
- **Prompt Injection:** Exploiting LLM vulnerabilities, agent manipulation, function leaking
- **Agentic AI Security:** Understanding AI agent attack surfaces

**Real-World Application:** As organizations adopt AI tools, understanding AI security vulnerabilities becomes critical.

**Covered in:** Days 4, 8

---

### Linux Administration
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **Command Line:** File navigation, text processing, system administration
- **Bash Commands:** grep, find, cat, chmod, sudo, history analysis
- **Log Analysis:** Using CLI tools to parse and analyze logs
- **System Investigation:** File system forensics, bash history analysis

**Real-World Application:** 90% of security tools run on Linux; essential for SOC work.

**Covered in:** Day 1 and throughout the event

---

### Incident Response & Threat Hunting
**Proficiency Level:** ⭐⭐⭐⭐☆ (Proficient)

- **Alert Triage:** Prioritizing security alerts by severity and impact
- **Investigation Workflows:** Systematic approach to incident analysis
- **Threat Hunting:** Proactive searching for threats using behavioral indicators
- **Attack Chain Analysis:** Understanding attacker progression and motivations
- **C2 Detection:** Identifying command and control infrastructure communication

**Real-World Application:** Core SOC Analyst responsibilities.

**Covered in:** Days 3, 10, 22

---

## Quantifiable Achievements

| Metric | Achievement |
|--------|----------------|
| **Challenges Completed** | 24/24 (100%) |
| **Training Hours** | 60+ hours |
| **Security Incidents Analyzed** | 24+ mock scenarios |
| **Tools Used** | 50+ security tools |
| **Documentation Created** | 15,000+ words |
| **Case Studies Written** | 3-5 detailed investigations |
| **Screenshots Captured** | 50+ sanitized images |
| **GitHub Commits** | 30+ portfolio updates |

---

## Alignment with Career Goals

### Target Role: SOC Analyst I / Junior SOC Analyst

**Typical Requirements → My AOC 2025 Coverage:**

| Job Requirement | AOC 2025 Skills Gained | Evidence |
|-----------------|------------------------|----------|
| SIEM experience (Splunk, Sentinel) | ✅ Hands-on Splunk and Sentinel usage | Days 3, 10, 22 |
| Log analysis and correlation | ✅ Attack chain reconstruction from logs | Day 3 case study |
| Alert triage and investigation | ✅ SOC workflow practice | Day 10 case study |
| Network security fundamentals | ✅ Nmap, Wireshark, protocol analysis | Day 7 case study |
| Incident response basics | ✅ Investigation methodologies | Days 3, 10, 22 |
| Linux/Windows administration | ✅ Command-line proficiency | Day 1 + throughout |
| Communication skills | ✅ Professional documentation | This entire portfolio |
| Security certifications | 🔄 Security+ in progress | Exam scheduled Q1 2026 |

**Match Rate: 90%+** of typical SOC Analyst I requirements

---

### Security+ Certification Preparation

**CompTIA Security+ SY0-701 Coverage:**

| Domain | Weight | AOC 2025 Coverage | Strength |
|--------|--------|-------------------|----------|
| **1.0 - General Security Concepts** | 12% | Days 2, 5, 9, 11, 17, 18 | ⭐⭐⭐⭐☆ |
| **2.0 - Threats & Vulnerabilities** | 22% | Days 2, 5, 6, 7, 11, 12, 13, 14, 15, 18, 19, 20, 21, 22, 23, 24 | ⭐⭐⭐⭐⭐ |
| **3.0 - Security Architecture** | 18% | Days 1, 7, 10, 14, 16, 19, 23 | ⭐⭐⭐⭐☆ |
| **4.0 - Security Operations** | 28% | Days 3, 6, 10, 12, 13, 15, 16, 21, 22 | ⭐⭐⭐⭐⭐ |
| **5.0 - Security Program Management** | 20% | Limited coverage | ⭐⭐☆☆☆ |

**Overall Alignment:** AOC 2025 provides strong practical reinforcement for 70% of Security+ exam content, particularly in Security Operations and Threats/Vulnerabilities—the highest-weighted domains.

---

## Professional Value Proposition

### What I Can Deliver Today

As a result of completing AOC 2025 and creating this documentation, I can:

✅ **Triage and investigate security alerts** using industry-standard SIEM platforms  
✅ **Analyze logs systematically** to identify attack patterns and anomalies  
✅ **Perform network reconnaissance** and understand attacker methodologies  
✅ **Investigate incidents** from detection through analysis to documentation  
✅ **Work comfortably in Linux environments** for security operations  
✅ **Communicate technical findings clearly** through professional documentation  
✅ **Understand common attack vectors** and defensive strategies  
✅ **Learn new tools quickly** as demonstrated by mastering 50+ tools in 24 days

### What Sets Me Apart

**1. Hands-On Practical Experience**
Unlike candidates with only theoretical knowledge, I have documented practical experience analyzing real security scenarios.

**2. Professional Documentation Skills**
This portfolio demonstrates my ability to communicate technical concepts clearly—a critical but often overlooked SOC analyst skill.

**3. Self-Directed Learning**
I independently identified this training opportunity, committed to daily challenges during the holiday season, and created comprehensive documentation without being required to.

**4. Strategic Alignment**
Every skill I developed connects directly to both Security+ certification objectives and SOC Analyst job requirements—I'm learning with purpose.

**5. Persistence and Consistency**
Completing all 24 challenges during December while managing other commitments demonstrates the reliability and persistence required in SOC operations.

---

## Learning Journey Highlights

### Week 1: Foundations
Started with Linux basics and fundamental concepts. The Splunk challenge (Day 3) was particularly impactful—my first exposure to real SIEM operations. Initially struggled with SPL syntax but invested extra research time to understand log correlation principles.

**Key Breakthrough:** Realizing that log analysis isn't about memorizing commands, but understanding attacker behavior patterns.

### Week 2: Expanding Skills
Network discovery (Day 7) and SOC alert triage (Day 10) solidified my understanding of defensive operations. Day 10's Azure Sentinel challenge was frustrating due to infrastructure issues but taught me resilience when tools don't work perfectly.

**Key Breakthrough:** Understanding that SOC work involves working with imperfect information and making decisions under pressure.

### Week 3: Building Confidence
Web security challenges (XSS, IDOR) connected offensive and defensive perspectives. Understanding how vulnerabilities are exploited makes me better at detecting exploitation attempts.

**Key Breakthrough:** Defensive security requires thinking like an attacker.

### Week 4: Advanced Concepts
Docker container escape (Day 14), forensics (Days 15, 16), CyberChef deobfuscation (Day 17), ICS/SCADA (Day 19), race conditions (Day 20), HTA malware (Day 21), C2 detection (Day 22), AWS security (Day 23), and cURL exploitation (Day 24) pushed me beyond comfort zones. These challenges required synthesizing skills from earlier days and introduced entirely new domains like industrial control systems and advanced cloud security.

**Key Breakthrough:** Cybersecurity is about connecting dots across multiple data sources—no single indicator tells the whole story. The ability to pivot between offensive and defensive perspectives strengthens both.

---

## Challenges Overcome

### Technical Challenges
- **Splunk SPL Syntax:** Spent 3+ extra hours mastering search language
- **Azure Infrastructure Issues:** Day 10 had known issues; required patience and alternative approaches
- **Network Protocol Understanding:** Needed additional research on MQTT and advanced HTTP concepts
- **ICS/SCADA Concepts:** Industrial systems were unfamiliar; required conceptual understanding before practical application

### Time Management
- **Holiday Season Conflicts:** Completed challenges during family obligations
- **Daily Consistency:** Maintained 24-day streak despite scheduling challenges
- **Security+ Studies:** Balanced AOC with certification preparation

### Personal Growth
- **Impostor Syndrome:** Overcame feeling "not technical enough" for cybersecurity
- **Persistence:** Pushed through days when challenges felt overwhelming
- **Documentation Discipline:** Committed to documenting while knowledge was fresh

---

## Portfolio Structure Overview

This portfolio is organized to provide multiple entry points depending on reader interest:

**For Recruiters (5-minute scan):**
→ Main README.md + This Executive Summary

**For Hiring Managers (15-minute review):**
→ Skills Matrix + 3 Case Studies

**For Technical Interviewers (30+ minutes):**
→ Daily Challenge Documentation + Technical Deep-Dives

**For Peer Learners:**
→ Learning Journey Narrative + Resources

---

## Next Steps in My Cybersecurity Journey

### Immediate (Q1 2026)
- [ ] Complete Security+ certification (exam scheduled March 2026)
- [ ] Continue TryHackMe SOC Level 1 learning path
- [ ] Build home lab for continued hands-on practice
- [ ] Apply for SOC Analyst I / Junior SOC Analyst positions

### Short-Term (Q2-Q3 2026)
- [ ] Gain entry-level SOC experience
- [ ] Pursue TryHackMe Junior SOC Analyst certification
- [ ] Contribute to cybersecurity community (writeups, mentoring)
- [ ] Deepen Azure/AWS cloud security knowledge

### Long-Term (2026-2027)
- [ ] Achieve 1 year SOC experience
- [ ] Pursue CompTIA CySA+ certification
- [ ] Develop specialization (DFIR, Threat Hunting, or Cloud Security)
- [ ] Transition to SOC Analyst II role

---

## Contact & Portfolio Links

**GitHub:** [github.com/uriel0byte](https://github.com/uriel0byte)  
**LinkedIn:** []  
**TryHackMe Profile:** []  
**Email:** poseidon.smash@gmail.com  

**This Portfolio:**
- Main Documentation: [Link to repo]
- Case Studies: [Link to case studies folder]
- Skills Matrix: [Link to skills matrix]

---

## Conclusion

Completing TryHackMe's Advent of Cyber 2025 represents a significant milestone in my transition from ILS studies to a cybersecurity career. This achievement demonstrates:

✅ **Technical capability** through hands-on mastery of security tools and concepts  
✅ **Professional communication** through comprehensive documentation  
✅ **Commitment to excellence** through 100% completion during challenging period  
✅ **Strategic learning** aligned with Security+ certification and SOC career path  
✅ **Growth mindset** demonstrated by overcoming obstacles and continuous improvement

I am actively seeking SOC Analyst I positions where I can apply these skills, contribute to security operations, and continue growing as a cybersecurity professional.

---

*Last Updated: January 18, 2026*  
*Advent of Cyber 2025: December 1-31, 2025*  
*Documentation Created: January 2026*
