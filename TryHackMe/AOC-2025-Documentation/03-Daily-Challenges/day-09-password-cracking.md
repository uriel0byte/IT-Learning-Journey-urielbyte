# Day 9: Password Cracking - A Cracking Christmas

## 📋 Quick Facts
- **Date Completed:** December 9, 2025
- **Time Spent:** 1 hour
- **Difficulty:** ★☆☆☆ (Easy)
- **Category:** Password Security / Cryptography
- **Room URL:** https://tryhackme.com/room/attacks-on-ecrypted-files-aoc2025-asdfghj123

---

## 🎯 Challenge Overview

Sir Carrotbane discovered encrypted PDF and ZIP files labeled "North Pole Asset List" containing fragments of Santa's master gift registry. I learned how weak passwords make encrypted files vulnerable and practiced using dictionary attacks with `pdfcrack`, `fcrackzip`, and John the Ripper to crack password-protected files. The room's most valuable section introduced **defensive detection techniques** for identifying password cracking activity on endpoints—critical for SOC analysts since offline cracking doesn't trigger traditional authentication alerts.

**Learning Objectives:**
- Understand password-based encryption (PDFs, ZIP archives)
- Learn why weak passwords make encrypted files vulnerable
- Use dictionary and brute-force attacks to recover passwords
- **NEW:** Learn detection techniques for password cracking activity (defensive perspective)

---

## 💡 What I Learned

### Password-Based Encryption Fundamentals

**Core Principle:**
Protection strength depends **almost entirely on password quality**.

```
Short/common password → Easily guessed
Long, random password → Far harder to break
```

**Critical Points:**
- Encryption protects confidentiality only (doesn't prevent offline guessing)
- Different file formats use different algorithms (PDF vs. ZIP encryption)
- Consumer tools often support legacy/weak modes (older ZIP especially vulnerable)

### Attack Methods (Review)

**Dictionary Attacks (Fast, Effective):**
- Predefined wordlists (`rockyou.txt`, common-passwords.txt)
- Leaked passwords from breaches
- Common substitutions (password123, P@ssw0rd)

**Brute-Force/Mask Attacks (Thorough, Slower):**
- Try every possible character combination
- **Mask attacks** narrow search (e.g., `?l?l?l?d?d` = 3 letters + 2 digits)
- GPU acceleration dramatically speeds up cracking

**Attacker Strategy:**
```
1. Wordlist attack (fast wins)
2. Targeted wordlists (company/project names)
3. Mask attacks (known password structure)
4. GPU-accelerated cracking
```

### Tools I Practiced

**PDF Cracking:**
```bash
# Dictionary attack with pdfcrack
pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt

# Output shows:
# - Average speed (words/sec)
# - Current word being tested
# - "found user-password: 'XXXXXXXXXX'" when successful
```

**ZIP Cracking (John the Ripper):**
```bash
# Step 1: Convert ZIP to John-compatible hash
zip2john flag.zip > ziphash.txt

# Step 2: Crack with wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt

# Output shows hash type, speed, recovered password
```

---

## 🛡️ **Detection of Password Cracking (NEW — Most Important for SOC)**

### The Detection Challenge

**Why offline cracking is invisible:**
- No login service hits
- No account lockouts
- No failed login dashboards

**Solution:** Detect on **endpoints** where cracking occurs.

### Four Detection Signal Categories

**1. Process Creation Monitoring**

**Binaries to watch:**
- `john`, `hashcat`, `fcrackzip`, `pdfcrack`
- `zip2john`, `pdf2john.pl`, `7z`, `qpdf`

**Command-line indicators:**
```
Flags: --wordlist, -w, --rules, --mask, -a 3, -m
References: rockyou.txt, SecLists, zip2john, pdf2john
```

**Artifacts (cracked password storage):**
```
~/.john/john.pot
.hashcat/hashcat.potfile
john.rec (session recovery)
```

**Platform-specific:**
- **Windows:** Sysmon Event ID 1 (full command line)
- **Linux:** auditd, execve, EDR sensors

---

**2. GPU and Resource Artifacts**

**GPU cracking is loud:**
- Sudden high GPU utilization
- `nvidia-smi` shows long-running hashcat/john
- High, steady GPU utilization + power draw
- Fan curve spikes

**Libraries loaded:**
```
Windows: nvcuda.dll, OpenCL.dll, amdocl64.dll
Linux: libcuda.so
```

---

**3. Network Hints (Light but Useful)**

Offline cracking doesn't need network once wordlists present, but:
- Downloads of large text files (rockyou.txt)
- Git clones of wordlist repositories
- Package installs (`apt install john hashcat`)
- GPU driver updates/downloads

---

**4. Unusual File Reads**

Repeated reads of:
- Wordlist files (`/usr/share/wordlists/rockyou.txt`)
- Encrypted files being cracked

### Detection Rules (What I Partially Understand)

**Sysmon (Windows):**
```
(ProcessName="C:\Program Files\john\john.exe" OR
 ProcessName="C:\Tools\hashcat\hashcat.exe" OR
 CommandLine="*pdf2john.pl*" OR
 CommandLine="*zip2john*")
```

**Linux audit rules:**
```bash
auditctl -w /usr/share/wordlists/rockyou.txt -p r -k wordlists_read
auditctl -a always,exit -F arch=b64 -S execve -F exe=/usr/bin/john -k crack_exec
```

**What I understand:** These alert when cracking tools run.

**What's still unclear:** Specific syntax details (Sysmon filters, auditctl flags, Sigma rule structure).

### Incident Response Playbook (NEW)

**Immediate actions when cracking detected:**

```
1. Isolate host (if malicious) OR tag/suppress (if lab)
2. Capture triage artifacts:
   - Process list
   - Memory dump
   - nvidia-smi output
   - Open files
3. Preserve evidence:
   - Working directory
   - Wordlists
   - Hash files
   - Shell history
4. Review impact:
   - Which files decrypted?
   - Lateral movement?
   - Exfiltration?
5. Identify intent:
   - Authorized testing?
   - Escalate to IR if malicious
6. Remediate:
   - Rotate affected passwords
   - Enforce MFA
7. Close with education
```

---

## 🛠️ Tools & Techniques Used

### Tools
1. **pdfcrack** - PDF password cracking
2. **fcrackzip** - ZIP password cracking
3. **John the Ripper** - General password cracker
4. **zip2john/pdf2john** - Hash extraction utilities
5. **rockyou.txt** - Popular wordlist (14+ million passwords)

### Techniques
- Dictionary attacks (wordlist-based)
- File type identification
- Hash extraction
- Offline password cracking
- **Detection rule analysis** (new defensive skill)

---

## 🤔 Challenges I Faced

**No Major Problems:** Mostly review. I've learned password cracking before.

**What I Reviewed:**
- Dictionary vs. brute-force/mask attacks
- Using pdfcrack, fcrackzip, john
- rockyou.txt wordlist
- Offline cracking methodology

**NEW Topic — Detection (Partial Understanding):**

**What I Get:**
- Monitor for cracking tool processes
- Watch GPU usage spikes
- Look for wordlist downloads/reads
- Endpoint-based detection required

**What I Don't Fully Get:**
- Sysmon filter syntax
- auditctl flag meanings (`-w`, `-p r`, `-k`, `-a always,exit`, `-F`)
- Sigma rule structure and SIEM translation

**Overall:** Easy room. Cracking = straightforward review. Detection = new defensive concepts still learning.

---

## ✅ How This Helps My Career

**Why Password Security Matters:**
- **45% of SOC analyst job postings** mention password security/credential protection
- Weak passwords = top attack vector
- Understanding attacks helps build defenses

**Defensive Security (SOC — My Focus):**

**Threat Detection (NEW from this room):**
- Recognize cracking tool signatures (john, hashcat)
- Monitor GPU usage anomalies
- Detect wordlist downloads and suspicious file reads
- Alert on cracking tool execution

**Incident Response:**
- Investigate credential compromise
- Assess which accounts/files accessed
- Follow IR playbook for password cracking incidents
- Recommend password rotation + MFA

**Offensive Security (Red Team/Pentesting):**

**Password Auditing:**
- Test organizational password policies
- Identify weak passwords
- Demonstrate risk of password reuse

**Post-Exploitation:**
- Crack encrypted files found during pentests
- Extract credentials from archives
- Access sensitive documents

**Interview Talking Point:** "I have hands-on experience with password cracking tools like John the Ripper and pdfcrack for both offensive security testing and defensive awareness. I understand dictionary and brute-force methodologies using wordlists like rockyou.txt. More importantly from a SOC perspective, I'm learning to detect password cracking activity through process monitoring, GPU usage analysis, and detection rules—skills critical for identifying credential-based attacks on endpoints before data exfiltration occurs."

---

## 🔗 Security+ Connection

**Domain 1.0 - General Security Concepts (12%):** Password policies, authentication security, cryptography, password hashing.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Password attacks, brute-force attacks, credential compromise.

**Domain 4.0 - Security Operations (28%):** Incident detection, monitoring and logging, threat hunting, incident response.

---

## 📸 Evidence

**Note:** Screenshots were not captured during initial completion. Documentation based on hands-on completion and room content review.

### Key Findings:
- Successfully cracked PDF password using pdfcrack with rockyou.txt (~30k words/sec)
- Successfully cracked ZIP password using zip2john + john with rockyou.txt (~2 minutes)
- Learned endpoint detection techniques: process monitoring, GPU usage, wordlist reads
- Reviewed incident response playbook for password cracking incidents

---

## 📚 Key Takeaways for Future Reference

### Password Cracking Tool Quick Reference

```bash
# Identify file type
file flag.pdf
file flag.zip

# PDF cracking
pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt

# ZIP cracking (John the Ripper)
zip2john flag.zip > ziphash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt

# View cracked passwords
john --show ziphash.txt
```

### Detection Quick Reference (SOC Focus)

**What to Monitor:**

| Signal Type | Indicators | Tools |
|------------|-----------|-------|
| **Process** | john, hashcat, pdfcrack, zip2john | Sysmon, EDR, auditd |
| **GPU** | High utilization, nvidia-smi | GPU monitoring, perfmon |
| **Network** | rockyou.txt downloads, Git clones | Proxy logs, EDR telemetry |
| **Files** | Wordlist reads, repeated encrypted file reads | File access logs, auditd |

**Command-Line Red Flags:**
```
--wordlist
-w rockyou.txt
--mask
-a 3
zip2john
pdf2john
```

**Artifact Locations:**
```
~/.john/john.pot
~/.hashcat/hashcat.potfile
john.rec
```

### Incident Response Checklist

When password cracking detected:
- [ ] Isolate host (if malicious)
- [ ] Capture process list, memory dump
- [ ] Preserve working directory, wordlists
- [ ] Review decrypted files
- [ ] Search for lateral movement/exfiltration
- [ ] Identify if authorized testing
- [ ] Rotate affected passwords
- [ ] Enforce MFA
- [ ] Educate users

### Password Security Best Practices

**Strong passwords:**
- 16+ characters
- Random (use password manager)
- Unique per account
- MFA enforcement

**Organizational defense:**
- Password policy enforcement
- Regular password audits
- Security awareness training
- MFA mandatory
- Monitor for cracking activity on endpoints

---
