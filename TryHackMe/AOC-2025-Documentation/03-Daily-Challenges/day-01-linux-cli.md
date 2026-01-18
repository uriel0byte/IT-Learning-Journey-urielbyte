# Day 1: Shells and Bells - Linux Command Line

## 📋 Quick Facts
- **Date Completed:** December 1, 2025
- **Time Spent:**  2 hours
- **Difficulty:** ★☆☆☆ (Easy)
- **Category:** Foundational Skills / Linux
- **Room URL:** https://tryhackme.com/room/linuxcli-aoc2025-o1fpqkvxti

---

## 🎯 Challenge Overview

This challenge introduced Linux command-line basics through a narrative where McSkidy has been kidnapped. As part of the investigation team, I needed to analyze the **tbfc-web01** server to uncover clues by navigating the file system, searching for files, and examining command histories.

**Learning Objectives:**
- Master basic Linux CLI commands
- Understand file system navigation and permissions
- Apply CLI skills for security investigation

---

## 💡 What I Learned

### Linux CLI Fundamentals
Gained hands-on experience with essential commands for system investigation:
- **Navigation:** `ls`, `cd`, `pwd` for file system exploration
- **File Operations:** `cat`, `grep`, `find` for searching and viewing files
- **Hidden Files:** Using `ls -la` to reveal files starting with `.` (often used by attackers or system configs)
- **Privilege Escalation:** `sudo su` to access root-level directories
- **History Analysis:** Examining `.bash_history` for forensic investigation

### Bash History Forensics
**Critical discovery:** The `.bash_history` file stores every command a user has executed, making it invaluable for incident investigation. I traced McSkidy's investigation trail and discovered suspicious commands from Sir Carrotbane showing data exfiltration via `curl` commands.

**Security Insight:** Attackers often try to clear bash history, but finding it intact can reveal the entire attack chain.

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Bash Terminal** - Linux command-line interface (Linux CLI)
2. **grep** - Pattern matching in files and logs (pattern matching)
3. **find** - File system search utility (file system search)
4. **cat** - File content viewer 
5. **sudo** - Privilege escalation

### Techniques
- File system navigation
- Hidden file discovery (`.` prefix)
- Log analysis (`/var/log/auth.log`)
- Bash Command history forensics
- Root user investigation
- Pattern matching with grep

---

## 🤔 Challenges I Faced
I didn't have any problems at all for all of the question provided but I struggled a while at trying to get access to (Side Quest 1 - The Great Disappearing Act) for about 1 hour and finally push through and finished it. So, I tried to do that Side Quest 1 but it was out of my league. I don't have enough knowledge to be able to finish it so I moved on.

---

## ✅ How This Helps My Career
Linux proficiency seems to appear in a lot of SOC analyst job postings because most security tools (SIEM, IDS/IPS, forensics tools) run on Linux servers. Being comfortable with the command line is non-negotiable. This challenge gave me hands-on practice with the exact commands I'll use daily to investigate:
- Investigating log files
- Searching for indicators of compromise (IOCs)
- Analyzing system configurations
- Conducting forensic investigations

**Interview Talking Point:** "I can confidently navigate Linux systems via CLI, search for suspicious files using find/grep, and analyze bash history for forensic investigation—skills I demonstrated while solving TryHackMe's Advent of Cyber challenges."

---

# 🔗 Security+ Connection

**Domain 3.0 - Security Architecture (18%):** Operating system security, file permissions, access control models, and system hardening concepts.

**Domain 4.0 - Security Operations (28%):** Log analysis, incident investigation, and forensic techniques.

---

## 📸 Evidence

![Linux CLI Investigation]()
*Successfully analyzed bash history to uncover suspicious command execution patterns*

---
