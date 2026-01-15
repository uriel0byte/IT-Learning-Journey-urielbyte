# Day 1: Shells and Bells - Linux Command Line

## 📋 Quick Facts
- **Date Completed:** December 1, 2025
- **Time Spent:**  2 hours
- **Difficulty:** ★☆☆☆ (Easy)
- **Category:** Foundational Skills / Linux
- **Room URL:** https://tryhackme.com/room/linuxcli-aoc2025-o1fpqkvxti

---

## 🎯 Challenge Overview

### The Story
McSkidy has been kidnapped! Without her, Wareville's defenses are faltering, and Christmas itself hangs by a thread. The TBFC (The Best Festival Company) team is investigating **tbfc-web01**, a server processing Christmas wishlists. Somewhere within its data may lie the truth: traces of McSkidy's final actions, or perhaps clues to King Malhare's twisted vision for EASTMAS.

### Official Learning Objectives
- Learn the basics of the command-line interface (CLI)
- Explore its use for personal objectives and IT administration
- Apply knowledge to unveil Christmas mysteries

---

## 🎯 What This Challenge Was About
This was an introduction to Linux command-line basics. The challenge put me in the role of an IT administrator who needed to navigate the file system, search for files, and manage permissions. It started easy with basic commands and gradually introduced more complex tasks like finding hidden files and understanding file permissions.

## 💡 What I Learned

### 1. Linux CLI Fundamentals
**What clicked:** The power of the command line for system investigation. No GUI needed!

**Key commands I mastered:**
- `echo "Hello World!"` - Basic output
- `ls` / `ls -la` - List files (including hidden)
- `cat filename` - Display file contents
- `cd directory` - Change directory
- `pwd` - Print working directory
- `grep "pattern" file` - Search within files
- `find /path -name pattern` - Search for files
- `sudo su` - Switch to root user
- `whoami` - Check current user
- `history` - View command history

### 2. Hidden Files in Linux
**The dot (.) prefix:** Files starting with `.` are hidden from normal `ls` view. Used by:
- System administrators (config files)
- Attackers (malware, backdoors)
- McSkidy (security guides!)

**Discovery:** `ls -la` reveals ALL files, including hidden ones.

### 3. Bash History Analysis
**Major takeaway:** Every command is saved in `.bash_history` - a goldmine for forensic investigations!

**What I found:**
- McSkidy's investigation trail in `/home/mcskidy/.bash_history`
- Root's suspicious commands in `/root/.bash_history`
- Sir Carrotbane's malicious `curl` commands uploading stolen data

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Bash Terminal** - Linux command-line interface
2. **grep** - Pattern matching in files and logs
3. **find** - File system search utility
4. **cat** - File content viewer
5. **sudo** - Privilege escalation

### Techniques
- File system navigation
- Hidden file discovery (`.` prefix)
- Log analysis (`/var/log/auth.log`)
- Bash history forensics
- Root user investigation
- Pattern matching with grep

---

## 🤔 Challenge I Faced
I didn't have any problems at all for all of the question provided but I struggled a while at trying to get access to (Side Quest 1 - The Great Disappearing Act) for about 1 hour and finally push through and finished it. So, I tried to do that Side Quest 1 but it was out of my league. I don't have enough knowledge to be able to finish it so I moved on.

## ✅ How This Helps My Career
Linux proficiency seems to appear in a lot of SOC analyst job postings because most security tools (SIEM, IDS/IPS, forensics tools) run on Linux servers. Being comfortable with the command line is non-negotiable. This challenge gave me hands-on practice with the exact commands I'll use daily to investigate log files, search for indicators of compromise, and analyze system configurations.

## 🔗 Security+ Connection
**Domain 3.3:** Security Architecture - Understanding operating system security including file permissions, access control, and system hardening concepts.

## 📸 Screenshot
![Key Finding](../07-Screenshots/day-XX/main-screenshot.png)
*Successfully using find and grep to locate specific files in the directory structure*

---
