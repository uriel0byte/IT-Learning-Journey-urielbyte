# Day 4: AI in Security - old sAInt nick

## 📋 Quick Facts
- **Date Completed:** December 4, 2025
- **Time Spent:** 1 hour
- **Difficulty:** ★☆☆☆ (Easy)
- **Category:** AI Security / Emerging Technologies
- **Room URL:** https://tryhackme.com/room/AIforcyber-aoc2025-y9wWQ1zRgB

---

## 🎯 Challenge Overview

This challenge introduced AI-powered cyber security assistants through TBFC's new tool, Van SolveIT. I explored how AI agents can assist across defensive security (Blue Team), offensive security (Red Team), and software development workflows. The hands-on exercise demonstrated AI's practical applications in generating exploits, analyzing web logs, and scanning code for vulnerabilities.

**Learning Objectives:**
- Understand how AI can assist in various cyber security roles and tasks
- Use an AI assistant to solve defensive, offensive, and software security challenges
- Learn important considerations when deploying AI in cyber security contexts

---

## 💡 What I Learned

### AI's Role in Cyber Security

AI assistants are transforming how cyber security professionals work by automating tedious, time-consuming tasks and allowing humans to focus on critical analysis and decision-making.

**Key AI Capabilities for Security:**

| AI Feature | Cyber Security Application |
|------------|---------------------------|
| **Processing large data volumes** | Analyzing vast amounts of system and network logs simultaneously |
| **Behavior analysis** | Tracking normal activity patterns and flagging anomalies |
| **Generative capabilities** | Summarizing events and providing context to security incidents |

### Defensive Security (Blue Team)

AI agents accelerate detection, investigation, and response workflows:
- **Automated alert triage** - Processing telemetry (logs, network flows, endpoint signals) and adding context to alerts
- **Vendor integration** - AI-assisted firewalls and intrusion detection systems (IDS)
- **Automated response** - Real-time actions like isolating infected devices, blocking suspicious emails, or flagging unusual login attempts

**Example Use Cases:**
- Analyzing patterns across multiple log sources
- Identifying anomalous behavior in user activity
- Correlating alerts from multiple security tools

### Offensive Security (Red Team)

AI assists penetration testers by automating labor-intensive reconnaissance tasks:
- **Information gathering** - Automating OSINT (Open Source Intelligence) collection
- **Scanner output analysis** - Processing noisy scan results from tools like Nmap
- **Attack surface mapping** - Identifying potential entry points across large infrastructures
- **Exploit generation** - Creating proof-of-concept exploit scripts

This allows pentesters to spend more time on tasks requiring human expertise and critical thinking.

### Software Security

AI serves as a virtual code review assistant:
- **Code vulnerability scanning** - Auditing code for potential security flaws
- **Static analysis** - Identifying common vulnerabilities (SQL injection, XSS, etc.)
- **Code review assistant** - Acting as a "colleague" to bounce ideas off during development

**Irony noted:** AI agents are effective at *identifying* vulnerabilities but not as reliable at *writing* secure code.

### Critical Considerations for AI in Cyber Security

**⚠️ Important Limitations:**

1. **Accuracy is not guaranteed** - AI output must be verified; never assume 100% correctness
2. **Data privacy concerns** - Sensitive data used to train AI models may be exposed
3. **Offensive security risks** - AI could cause unintended damage (race conditions, denial of service)
4. **Transparency challenges** - Understanding how AI reaches decisions can be difficult
5. **Model security** - AI models themselves can be attacked or manipulated

**Best Practices:**
- Always verify AI-generated exploits before execution
- Be cautious when using AI in live penetration testing environments
- Never feed sensitive client data into public AI models
- Treat AI as an assistant, not a replacement for human expertise

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Van SolveIT** - AI cyber security assistant (custom chatbot)
2. **AI Exploit Generator** - Red Team automated exploit creation
3. **AI Log Analyzer** - Blue Team web log analysis
4. **AI Code Scanner** - Software vulnerability detection

### Techniques
- **Red Team Showcase:** Generated and executed exploit script against vulnerable web application
- **Blue Team Showcase:** Analyzed web server logs to identify attack patterns
- **Software Showcase:** Scanned source code for security vulnerabilities
- Interacting with AI agents via conversational interface
- Understanding AI's role in automating security workflows

---

## 🤔 Challenges I Faced

Nothing in particular—this challenge was pretty straightforward. I just followed the instructions through UnixGuy's interactive showcase. It was an easy learning experience focused on understanding new concepts rather than technical problem-solving.

**What made it easy:**
- Clear step-by-step guidance from the AI assistant
- Well-structured showcase format (Red → Blue → Software)
- No complex technical prerequisites
- Focus on understanding AI applications rather than deep technical implementation

**What I appreciated:**
- Learning how AI fits into real-world security workflows
- Seeing practical examples across all three domains (Red, Blue, Software)
- Understanding the limitations and risks of AI in security contexts

---

## ✅ How This Helps My Career

AI in cyber security is rapidly growing—understanding how to leverage AI tools effectively is becoming essential for SOC analysts and security professionals.

**Why AI Security Skills Matter:**

**Growing Industry Adoption:**
- Security vendors are integrating AI into SIEMs, firewalls, EDR platforms
- SOC teams are using AI for alert triage and log analysis
- Penetration testers use AI to accelerate reconnaissance

**Practical SOC Applications:**
- **Alert fatigue reduction** - AI can pre-filter and prioritize alerts
- **Threat hunting** - AI assists in identifying patterns across massive datasets
- **Incident response** - AI provides context and suggests next steps during investigations

**Career Differentiation:**
- Many candidates avoid or fear AI; demonstrating experience is valuable
- Understanding AI's limitations shows critical thinking
- Being able to verify and validate AI output demonstrates expertise

**Interview Talking Point:** "I have hands-on experience using AI security assistants for both defensive operations (log analysis, alert triage) and offensive tasks (exploit generation, reconnaissance automation). I understand AI's role as a force multiplier for security teams while recognizing the critical importance of verifying AI-generated output and considering data privacy implications."

---

## 🔗 Security+ Connection

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Understanding emerging threats, including AI-based attacks and vulnerabilities introduced by AI systems.

**Domain 4.0 - Security Operations (28%):** Security automation, AI-assisted threat detection, and understanding how AI integrates into SOC workflows.

---

## 📸 Evidence

![Van SolveIT AI Assistant](../07-Screenshots/day-04/van-solveit-interface.png)
*Interacted with Van SolveIT AI assistant through Red, Blue, and Software security showcases*

![AI-Generated Exploit](../07-Screenshots/day-04/red-team-exploit.png)
*AI-generated exploit script executed against vulnerable web application*

![AI Log Analysis](../07-Screenshots/day-04/blue-team-log-analysis.png)
*AI assistant analyzing web server logs to identify attack patterns and anomalies*

---