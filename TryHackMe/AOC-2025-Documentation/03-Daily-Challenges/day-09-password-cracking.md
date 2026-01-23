# Day 9: Password Cracking - A Cracking Christmas

## 📋 Quick Facts
- **Date Completed:** December 9, 2025
- **Time Spent:** 1 hour
- **Difficulty:** ★☆☆☆ (Easy)
- **Category:** Password Security / Cryptography
- **Room URL:** https://tryhackme.com/room/attacks-on-ecrypted-files-aoc2025-asdfghj123

---

## 🎯 Challenge Overview

This challenge focused on password-based encryption vulnerabilities. Sir Carrotbane discovered encrypted PDF and ZIP files containing "North Pole Asset List" fragments of Santa's master gift registry. I learned how weak passwords make encrypted files vulnerable and used dictionary attacks with tools like `pdfcrack`, `fcrackzip`, and `john` (John the Ripper) to crack password-protected files. The room also introduced detection techniques for identifying password cracking activity on endpoints.

**Learning Objectives:**
- Understand how password-based encryption protects files (PDFs, ZIP archives)
- Learn why weak passwords make encrypted files vulnerable
- Use dictionary and brute-force attacks to recover passwords
- Practice cracking encrypted files to reveal contents
- Learn detection techniques for password cracking activity (new defensive perspective)

---

## 💡 What I Learned

### Password-Based Encryption Fundamentals

**Key Principle:** The strength of encryption protection depends almost entirely on the **password quality**.

- **Short or common passwords** → Can be guessed quickly
- **Long, random passwords** → Far harder to break

**Important Concepts:**

**1. Encryption protects confidentiality only**
- Encryption makes contents unreadable without the correct password
- Does NOT prevent offline password guessing attacks
- Attackers can try unlimited passwords if they have the encrypted file

**2. File formats use different encryption algorithms**
- **PDF encryption** vs. **ZIP encryption** differ in:
  - Key derivation methods
  - Salt usage
  - Number of hash iterations
- Legacy/weak modes (especially older ZIP encryption) are easier to crack

**3. Consumer tools often support weak encryption**
- Many tools still allow weak encryption modes for compatibility
- Makes some encrypted archives much easier to attack than modern implementations

### Attack Methods (Review)

**Dictionary Attacks (Fast and Effective)**

Use predefined wordlists containing:
- Leaked passwords from previous breaches
- Common substitutions (`password123`, `P@ssw0rd`)
- Predictable combinations (names + dates, patterns)

**Why effective:** Many users choose weak or common passwords

**Mask/Brute-Force Attacks (Thorough but Slower)**

**Brute-force:** Try EVERY possible character combination
- Guarantees success eventually
- Time grows exponentially with password length/complexity

**Mask attacks:** Limit guesses to specific formats
- Example: `?l?l?l?d?d` = three lowercase letters + two digits
- Reduces search space when password structure is known
- Balances speed and thoroughness

**Attacker Strategy (what I reviewed):**
1. Start with wordlist (fast wins) - `rockyou.txt`, `common-passwords.txt`
2. Try targeted wordlists (company names, project-specific terms)
3. Use mask attacks on short passwords
4. GPU-accelerate when possible (dramatically speeds up cracking)

### Password Cracking Tools (Hands-On Practice)

**Workflow:**

**1. Identify File Type**

```bash
file flag.pdf
file flag.zip
```

**2. Choose Tool Based on File Type**

| File Type | Tools |
|-----------|-------|
| **PDF** | `pdfcrack`, `john` (via `pdf2john`) |
| **ZIP** | `fcrackzip`, `john` (via `zip2john`) |
| **General** | `john` (flexible), `hashcat` (GPU-accelerated) |

**3. Dictionary Attack - PDF Example**

```bash
pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt
```

**Output shows:**
- PDF version, encryption details
- Average cracking speed (words/sec)
- Current password being tested
- `found user-password: 'XXXXXXXXXX'` when successful

**4. Dictionary Attack - ZIP with John the Ripper**

```bash
# Step 1: Convert ZIP to hash format John understands
zip2john flag.zip > ziphash.txt

# Step 2: Crack with wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt
```

**John reports:**
- Hash type detected (e.g., `ZIP, WinZip [PBKDF2-SHA1]`)
- Cracking speed and progress
- Recovered password when found

### Detection of Password Cracking Activity (NEW TOPIC)

**Challenge:** Offline cracking doesn't hit login services, so:
- No lockout alerts
- No failed login dashboards
- Must detect on endpoints where cracking occurs

**Detection Strategy: Look for process, GPU, network, and file artifacts**

**1. Process Creation Monitoring**

**Tools/Binaries to detect:**
- `john`, `hashcat`, `fcrackzip`, `pdfcrack`
- `zip2john`, `pdf2john.pl`, `7z`, `qpdf`

**Command-line indicators:**
- Flags: `--wordlist`, `-w`, `--rules`, `--mask`, `-a 3`, `-m`
- References to: `rockyou.txt`, `SecLists`, `zip2john`, `pdf2john`

**Potfiles (cracked password storage):**
- `~/.john/john.pot`
- `.hashcat/hashcat.potfile`
- `john.rec` (session recovery file)

**Platform-specific monitoring:**
- **Windows:** Sysmon Event ID 1 (process creation with full command line)
- **Linux:** `auditd`, `execve`, or EDR sensors (binaries + arguments)

**2. GPU and Resource Artifacts**

**GPU cracking is loud:**
- Sudden high GPU utilization on hosts
- `nvidia-smi` shows long-running `hashcat` or `john` processes
- High, steady GPU utilization and power draw
- Fan curve spikes

**Libraries loaded:**
- Windows: `nvcuda.dll`, `OpenCL.dll`, `amdocl64.dll`
- Linux: `libcuda.so`

**3. Network Hints (Light but Useful)**

Offline cracking doesn't need network once wordlists are present, but:
- Downloads of large text files (`rockyou.txt`)
- Git clones of wordlist repositories
- Package installs: `apt install john hashcat` (EDR package telemetry)
- GPU driver updates/downloads

**4. Unusual File Reads**

Repeated reads of:
- Wordlist files (`/usr/share/wordlists/rockyou.txt`)
- Encrypted files being cracked

### Detection Rules Examples (What I Didn't Fully Understand)

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

**Sigma rule (cross-platform detection format):**
- Detects execution of cracking tools
- Looks for specific command-line patterns
- Medium severity level

**What I understand:** These are detection rules for SIEM/EDR systems to alert when password cracking tools run.

**What's still unclear:** The specific syntax of each detection language (Sysmon filters, auditctl flags, Sigma format).

### Incident Response Playbook (NEW CONCEPT)

**Immediate Actions When Cracking Detected:**
1. **Isolate** the host (if malicious) or tag and suppress (if lab)
2. **Capture triage artifacts** - process list, memory dump, GPU output, open files
3. **Preserve evidence** - working directory, wordlists, hash files, shell history
4. **Review impact** - Which files were decrypted? Look for lateral movement/exfiltration
5. **Identify intent** - Authorized testing or malicious activity?
6. **Remediate** - Rotate affected passwords, enforce MFA
7. **Close with education** - Train users, move tools to approved sandboxes

---

## 🛠️ Tools & Techniques Used

### Tools
1. **pdfcrack** - PDF password cracking tool
2. **fcrackzip** - ZIP password cracking tool
3. **John the Ripper (john)** - General-purpose password cracker
4. **zip2john / pdf2john** - Convert encrypted files to John-compatible hash format
5. **rockyou.txt** - Popular wordlist (14+ million passwords)
6. **file** command - Identify file types

### Techniques
- **Dictionary attacks** - Wordlist-based password guessing
- **File type identification** - Determine encryption type
- **Hash extraction** - Convert encrypted files to crackable format
- **Offline password cracking** - Attack without network/authentication limits
- **Detection rule analysis** - Understanding defensive monitoring (new)

---

## 🤔 Challenges I Faced

**No Major Problems:** This was mostly a review topic. I've learned password cracking before, so the core concepts and tools were familiar.

**What I Reviewed Successfully:**
- Dictionary vs. brute-force/mask attacks
- Using `pdfcrack`, `fcrackzip`, and `john`
- `rockyou.txt` wordlist usage
- Offline cracking methodology

**New Topic - Detection (Partial Understanding):**
**"Detection of Indicators and Telemetry"** was new to me. I don't remember all the details, but I understand the core concept: **how to detect password cracking attacks from a defensive perspective**.

**What I Get:**
- Monitor for cracking tool processes (`john`, `hashcat`)
- Watch for GPU usage spikes
- Look for wordlist downloads/reads
- Detection is about finding artifacts on endpoints

**What I Don't Fully Get:**
The section **"Detections - Below are some examples of detection rules and hunting queries"** with Sysmon, Linux audit rules, and Sigma format. I can see they're detection rules for different platforms, but:
- **Sysmon syntax** - Don't fully understand the filter logic
- **auditctl flags** - What `-w`, `-p r`, `-k`, `-a always,exit`, `-F` mean exactly
- **Sigma rules** - The structure and how they translate to real SIEM queries

**Overall Assessment:** Pretty easy room. The cracking part was straightforward review; the detection part introduced new defensive concepts I'm still learning.

---

## ✅ How This Helps My Career

Password cracking knowledge is valuable for **both offensive (red team) and defensive (SOC) roles**:

**Why Password Security Matters:**
- **45% of SOC analyst job postings** mention password security/credential protection
- Weak passwords remain a top attack vector
- Understanding attacks helps defend against them

**Offensive Security Applications (Red Team / Penetration Testing):**

**Password Auditing:**
- Test organizational password policies
- Identify weak passwords in corporate environments
- Demonstrate risk of password reuse

**Post-Exploitation:**
- Crack encrypted files found during penetration tests
- Extract credentials from password-protected archives
- Access sensitive documents during red team engagements

**Defensive Security Applications (SOC Analyst):**

**Threat Detection (NEW from this room):**
- Recognize password cracking tool signatures
- Monitor for GPU usage anomalies
- Detect wordlist downloads and suspicious file reads
- Alert on cracking tool execution

**Incident Response:**
- Investigate credential compromise incidents
- Assess which accounts/files were accessed
- Follow IR playbook for password cracking incidents
- Recommend password rotation and MFA enforcement

**Security Awareness:**
- Educate users on password strength importance
- Demonstrate impact of weak passwords to stakeholders
- Advocate for password managers and strong password policies

**Career Skills Developed:**
- **Tool proficiency:** John the Ripper, hashcat, pdfcrack, fcrackzip
- **Offensive techniques:** Dictionary and mask attacks
- **Defensive mindset:** Detection rules and monitoring (new)
- **Incident response:** Triage, evidence preservation, remediation

**Interview Talking Point:** "I have hands-on experience with password cracking tools like John the Ripper, hashcat, and pdfcrack for both offensive security testing and defensive security awareness. I understand dictionary and brute-force attack methodologies using wordlists like rockyou.txt. From a defensive perspective, I'm learning to detect password cracking activity through process monitoring, GPU usage analysis, and detection rules in Sysmon and auditd. I can contribute to both red team password auditing and SOC alert triage for credential-based attacks."

---

## 🔗 Security+ Connection

**Domain 1.0 - General Security Concepts (12%):** Password policies, authentication security, cryptography concepts, password hashing.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Password attacks, brute-force attacks, credential compromise, attack techniques.

**Domain 4.0 - Security Operations (28%):** Incident detection, monitoring and logging, threat hunting, incident response procedures.

---

## 📸 Evidence

![pdfcrack Dictionary Attack](../07-Screenshots/day-09/pdfcrack-success.png)
*Successfully cracked password-protected PDF using pdfcrack with rockyou.txt wordlist, revealing average speed of ~30k words/sec*

![John the Ripper ZIP Cracking](../07-Screenshots/day-09/john-zip-crack.png)
*Used zip2john to extract hash and john with rockyou.txt to crack ZIP password in ~2 minutes*

![Detection Rules Overview](../07-Screenshots/day-09/detection-rules.png)
*Reviewed Sysmon, Linux auditctl, and Sigma detection rules for identifying password cracking tool execution*

---