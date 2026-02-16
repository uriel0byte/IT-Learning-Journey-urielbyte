# Day 2: Phishing - Merry Clickmas

## 📋 Quick Facts
- **Date Completed:** December 2, 2025
- **Time Spent:** 2 hours
- **Difficulty:** ★★☆☆ (Medium)
- **Category:** Social Engineering / Red Team Operations
- **Room URL:** https://tryhackme.com/room/phishing-aoc2025-h2tkye9fzU

---

## 🎯 Challenge Overview

This challenge put me on the TBFC red team alongside Recon McRed, Exploit McRed, and Pivot McRed to conduct an authorized phishing penetration test. The goal was to test if TBFC employees would fall for a phishing email and enter their credentials on a fake login page, validating whether security awareness training was effective. I learned the complete phishing attack lifecycle: building a credential harvesting trap, crafting convincing social engineering pretexts, and using the Social-Engineer Toolkit (SET) to deliver phishing emails that appeared to come from a trusted shipping partner.

**Learning Objectives:**
- Understand what social engineering is and how it exploits human psychology
- Learn the types of phishing (email, smishing, vishing, quishing)
- Explore how red teams create fake login pages for credential harvesting
- Use the Social-Engineer Toolkit (SET) to send realistic phishing emails
- Apply anti-phishing detection mnemonics (S.T.O.P.)

---

## 💡 What I Learned

### Social Engineering Fundamentals

**Definition:** Social engineering refers to manipulating a user to make a mistake—such as sharing a password, opening a malicious file, or approving a fraudulent payment.

**Key Principle:** The target is **human beings, not computer systems**. This is why some call it "human hacking."

**Psychological Factors Attackers Exploit:**
- **Urgency** - "Act now or lose access!"
- **Curiosity** - "You've received a package!"
- **Authority** - "Your manager needs this immediately!"

**Why it works:** Humans are the weakest link in security. Even strong technical defenses fail when users are tricked into bypassing them.

### Phishing Types and Evolution

**Phishing:** A subset of social engineering where the communication medium is mostly messages.

**Evolution of Phishing:**
- **Traditional:** Email phishing (still most common)
- **Smishing:** SMS/text message phishing
- **Vishing:** Voice call phishing
- **Quishing:** QR code phishing (emerging threat)
- **Social Media:** Direct message phishing

**Why phishing is dangerous:** Attacks are becoming harder to spot. Even careful people can fall victim if they don't exercise proper awareness.

### The S.T.O.P. Anti-Phishing Mnemonics

**S.T.O.P. #1 (Pre-Click Questions)** - From All Things Secured

Before acting on any email, ask yourself:
- **S**uspicious? Does something feel off about this message?
- **T**elling me to click? Is there pressure to click links?
- **O**ffering amazing deals? Is this too good to be true?
- **P**ushing urgency? Am I being rushed to act now?

**S.T.O.P. #2 (Response Protocol)**

When you receive a suspicious message:
- **S**low down - Scammers run on your adrenaline (panic = mistakes)
- **T**ype addresses yourself - Don't use the message's link
- **O**pen nothing unexpected - Verify before opening attachments
- **P**rove the sender - Check the real "From" address/number, not just display name

**Critical lesson:** These mnemonics are taught in TBFC security awareness training, yet users still fell for the phishing test. **Training alone isn't enough—regular testing validates effectiveness.**

### Building the Phishing Trap (Technical Setup)

**Objective:** Acquire target user's login credentials through a fake TBFC portal.

**Step 1: Fake Login Page Creation**

**Script location:** `~/Rooms/AoC2025/Day02/server.py`

**How to deploy:**
```bash
cd ~/Rooms/AoC2025/Day02
./server.py
```

**Output:**
```
Starting server on http://0.0.0.0:8000
```

**What this means:**
- Server listening on **port 8000**
- Bound to **0.0.0.0** (all interfaces) - accessible from any IP
- Hosts a fake TBFC login page
- Captures any credentials entered

**Testing the phishing page:**
- Browse to `http://CONNECTION_IP:8000` (external access)
- Or `http://127.0.0.1:8000` (local testing)
- Confirms what the victim will see

**Key insight:** The script implements backend logic to capture credentials. A realistic-looking login page alone isn't enough—you need server-side capture functionality.

**Step 2: Crafting the Social Engineering Pretext**

**Attack Strategy:**

**Trusted Entity Impersonation:**
- **Legitimate sender:** Flying Deer (trusted shipping company)
- **Business context:** TBFC employees regularly communicate with Flying Deer
- **Credible reason:** Shipping schedule changes (plausible during busy season)

**Email Components:**
- **From address:** `updates@flyingdeer.thm`
- **From name:** "Flying Deer" (display name users see)
- **Subject:** "Shipping Schedule Changes"
- **Body message:** Professional tone, legitimate business reason to click

**Why this works:** The email doesn't seem suspicious because:
1. Employees expect communication from Flying Deer
2. Subject line is relevant to business operations
3. Shipping schedules actually change (realistic scenario)
4. Creates urgency without being overtly suspicious

### Social-Engineer Toolkit (SET) Deep Dive

**What is SET:** An open-source tool designed by David Kennedy for social engineering attacks. Offers wide-ranging features for crafting and delivering phishing campaigns.

**Command to launch:**
```bash
setoolkit
```

**Complete Workflow (Step-by-Step):**

**Main Menu - Select Attack Type:**
```
Select from the menu:
   1) Social-Engineering Attacks
   
set> 1
```

**Social Engineering Menu - Choose Mass Mailer:**
```
Select from the menu:
   1) Spear-Phishing Attack Vectors
   2) Website Attack Vectors
   5) Mass Mailer Attack  ← Selected
   
set> 5
```

**Target Selection:**
```
What do you want to do:
   1. E-Mail Attack Single Email Address  ← Selected
   2. E-Mail Attack Mass Mailer
   
set:mailer> 1
```

**Email Configuration (Critical Details):**

**Target and Delivery:**
- **Send email to:** `factory@wareville.thm`
- **Delivery method:** Use your own server or open relay (option 2)
- **From address:** `updates@flyingdeer.thm`
- **From name:** Flying Deer
- **Username/Password:** Left blank (open relay)
- **SMTP server:** `MACHINE_IP` (TBFC mail server)
- **Port:** 25 (default SMTP)

**Email Options:**
- **High priority flag:** no (avoid suspicion)
- **Attach file:** n (credential harvesting, not malware)
- **Attach inline file:** n

**Email Content:**
- **Subject:** "Shipping Schedule Changes"
- **Format:** Plaintext (less suspicious than HTML)
- **Body:**
```
Dear elves,
Kindly note that there have been significant changes to the shipping 
schedules due to increased shipping orders.
Please confirm the new schedule by visiting http://CONNECTION_IP:8000
Best regards,
Flying Deer
```
- **End signal:** Type `END` (all capitals) on new line

**Final output:**
```
[*] SET has finished sending the emails
Press <return> to continue
```

**Important Notes:**
- **Ctrl+C** restarts if you make a mistake
- **Option 99** returns to main menu
- Wait 1-2 minutes for simulated user to interact
- Monitor `server.py` terminal for captured credentials

### Attack Success and Post-Exploitation

**Credential Harvest:**
- At least one set of working credentials captured
- Admin password successfully harvested

**Credential Reuse Testing:**
- Browse to `http://MACHINE_IP` (TBFC email portal)
- Log in with captured admin credentials
- **Success:** Password reused across systems (common vulnerability)
- Accessed admin's mailbox and discovered sensitive information

**Security Implications:**

**Why this is alarming:**
- ✅ Phishing bypassed security awareness training
- ✅ Users clicked malicious links
- ✅ Credentials entered on fake page
- ✅ Password reuse enabled lateral movement
- ✅ Admin access = potential system-wide compromise

**Real-world impact:**
If an actual adversary gained such access:
- Could compromise entire gift delivery system
- Access to sensitive customer data
- Potential for ransomware deployment
- Supply chain disruption

**Red Team Conclusion:** More security awareness training required. Current training is insufficient to protect against realistic phishing attacks.

### Understanding Email Delivery (SMTP)

**SMTP (Simple Mail Transfer Protocol):**
- Standard protocol for sending email
- Default port: 25
- Used by SET to deliver phishing emails

**How SET delivers email:**
1. Connects to target's SMTP server (`MACHINE_IP:25`)
2. Presents email as coming from `updates@flyingdeer.thm`
3. Server accepts and routes to `factory@wareville.thm`
4. User receives email in inbox

**Why spoofing works:**
- SMTP doesn't inherently verify sender identity
- Without SPF/DKIM/DMARC, spoofing is easy
- Display name ("Flying Deer") shown prominently
- Users rarely check actual email headers

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Social-Engineer Toolkit (SET)** - Phishing campaign automation
2. **server.py** - Custom credential harvesting server
3. **SMTP** - Email delivery protocol (port 25)
4. **Firefox** - Testing phishing page appearance
5. **Python** - Backend scripting for credential capture

### Techniques
- **Credential harvesting** - Fake login page captures usernames/passwords
- **Email spoofing** - Impersonating trusted sender (Flying Deer)
- **Sender impersonation** - Display name manipulation
- **Business context exploitation** - Leveraging existing trust relationships
- **SMTP relay configuration** - Direct mail server delivery
- **Pretext crafting** - Creating believable scenarios
- **Post-exploitation** - Testing credential reuse across systems
- **Authorized penetration testing** - Red team validation of security posture

---

## 🤔 Challenges I Faced

**Understanding SET Workflow:** SET has multiple nested menus and configuration steps. I had to be patient and follow each prompt carefully. One mistake means pressing `Ctrl+C` and starting over from the beginning.

**What made it challenging:**
- Multiple menu levels (main → social engineering → mass mailer → configuration)
- Lots of questions to answer sequentially
- No way to go back if you make a mistake midway
- Have to remember: Option 99 = main menu, Ctrl+C = restart

**Crafting Convincing Emails:** Writing a phishing email that's believable without being too suspicious required thinking about business context:
- Why would Flying Deer email about shipping schedules? ✅ Legitimate business relationship
- What would employees expect? ✅ Regular communication about shipping
- How to create urgency without raising red flags? ✅ "Confirm new schedule"

**Social Engineering Mindset:**
This challenged me to think like an attacker:
- What psychological triggers work? (urgency, authority, business necessity)
- How to build trust? (known sender, professional tone)
- How to avoid detection? (no attachments, plaintext, reasonable request)

**Waiting for Results:** After sending the email, I had to wait 1-2 minutes for the simulated user to interact with it. This taught me patience in red team operations—attacks don't always happen instantly.

**Ethical Considerations:** Even though this was authorized testing, creating phishing campaigns felt ethically complex. It reinforced why:
- ✅ Authorization is critical (never test without permission)
- ✅ Scope matters (only test authorized targets)
- ✅ Purpose is defensive (improve security posture)

---

## ✅ How This Helps My Career

Phishing is involved in **90% of successful breaches**, making it the **#1 initial access vector** for attackers. Understanding phishing is critical for both offensive (Red Team) and defensive (SOC Analyst) roles.

**Why Phishing Skills Matter:**

**Industry Statistics:**
- **90% of data breaches** start with phishing emails
- **85% of SOC analyst job postings** mention security awareness or phishing detection
- **Credential compromise** is the most common attack vector
- **Spear-phishing** bypasses most technical defenses

**SOC Analyst Applications (Defensive - My Career Focus):**

**Email Security Monitoring:**
- Analyze suspicious emails reported by users
- Identify phishing indicators (spoofed domains, suspicious links)
- Investigate email header information (SPF, DKIM, DMARC)
- Validate sender authenticity

**Incident Response:**
- Respond to credential compromise incidents
- Investigate which systems accessed with stolen credentials
- Assess scope of breach (password reuse, lateral movement)
- Coordinate password resets and account lockouts

**Security Awareness Programs:**
- Design phishing simulation campaigns (authorized testing)
- Educate users on S.T.O.P. mnemonics and detection techniques
- Measure training effectiveness through click rates
- Provide targeted training to vulnerable users

**Threat Detection:**
- Monitor for suspicious login attempts (compromised credentials)
- Detect credential stuffing attacks
- Identify unusual email patterns (mass phishing campaigns)
- Track phishing domains and infrastructure

**User Behavior Analytics:**
- Identify users who consistently fail phishing tests
- Monitor for credential reuse across systems
- Detect account compromise through behavioral anomalies

**Red Team Perspective (Offensive - Understanding the Adversary):**

**Penetration Testing:**
- Conduct authorized phishing assessments
- Test organization's security posture
- Validate effectiveness of email security controls
- Demonstrate real-world attack scenarios

**Social Engineering Assessments:**
- Craft convincing pretexts for authorized tests
- Understand psychological manipulation techniques
- Test human element of security defenses

**Career Skills Developed:**
- ✅ **Tool proficiency:** Social-Engineer Toolkit (SET)
- ✅ **Technical skills:** SMTP configuration, credential harvesting
- ✅ **Social engineering:** Psychological manipulation understanding
- ✅ **Defensive mindset:** Knowing attacks helps build defenses
- ✅ **Security awareness:** Educating users on phishing detection
- ✅ **Incident response:** Credential compromise investigation

**Real-World Scenarios:**

**Example 1 - SOC Analyst Daily Work:**
User reports suspicious email → Analyze headers → Identify spoofed sender → Check if credentials entered → Lock account → Force password reset → Alert security team

**Example 2 - Post-Breach Investigation:**
Admin account compromised → Review login history → Identify credential reuse → Check lateral movement → Assess data exfiltration → Implement MFA

**Example 3 - Security Awareness:**
Conduct quarterly phishing tests → Track click rates → Identify vulnerable departments → Provide targeted training → Measure improvement over time

**Interview Talking Point:** "I have hands-on experience conducting authorized phishing penetration tests using the Social-Engineer Toolkit (SET). I understand both the offensive techniques attackers use—including email spoofing, credential harvesting, and social engineering pretexts—and the defensive countermeasures SOC analysts deploy to detect and respond to phishing incidents. I can craft realistic phishing campaigns to test security posture, analyze email headers for spoofing indicators, investigate credential compromise incidents, and educate users on phishing detection using the S.T.O.P. mnemonics. I understand that phishing is the #1 initial access vector in 90% of breaches, making this knowledge critical for protecting organizations."

---

## 🔗 Security+ Connection

**Domain 1.0 - General Security Concepts (12%):** Social engineering tactics, security awareness training programs, user education, authentication security.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Threat actors, phishing attack techniques, credential harvesting, email-based attacks, spear-phishing.

**Domain 4.0 - Security Operations (28%):** Security awareness best practices, incident detection and response, email security, user behavior monitoring, credential compromise investigation.

---

## 📸 Evidence

**Note:** Screenshots were not captured during initial completion. Documentation based on hands-on completion and room content review.

### Key Findings:
- Successfully deployed credential harvesting server on port 8000
- Configured SET to send phishing email impersonating Flying Deer shipping company
- Crafted convincing pretext: "Shipping Schedule Changes" with legitimate business context
- Harvested admin credentials from fake TBFC login portal
- Validated password reuse vulnerability by accessing email portal with captured credentials
- Demonstrated effectiveness of phishing attacks despite security awareness training

---

## 📚 Key Takeaways for Future Reference

### Social Engineering Attack Fundamentals

**Core Principle:**
Social engineering targets **humans, not systems**. Technical defenses fail when users are manipulated into bypassing them.

**Psychological Triggers:**
- **Urgency:** "Act now or lose access!"
- **Curiosity:** "You've won a prize!"
- **Authority:** "Your boss needs this immediately!"
- **Fear:** "Your account will be locked!"
- **Trust:** Impersonating known entities

### S.T.O.P. Anti-Phishing Mnemonics (Critical for Defense)

**Before Clicking (S.T.O.P. #1):**
```
S - Suspicious? Does something feel off?
T - Telling me to click? Pressure to click links?
O - Offering amazing deals? Too good to be true?
P - Pushing urgency? Must act now?
```

**Response Protocol (S.T.O.P. #2):**
```
S - Slow down (scammers rely on adrenaline)
T - Type addresses yourself (never use message links)
O - Open nothing unexpected (verify first)
P - Prove the sender (check real address, not display name)
```

### Phishing Campaign Technical Setup

**Credential Harvesting Server:**
```bash
# Deploy fake login page
cd ~/Rooms/AoC2025/Day02
./server.py
# Output: Starting server on http://0.0.0.0:8000

# Test locally
firefox http://127.0.0.1:8000

# Monitor for captured credentials
# Watch terminal output
```

**Social-Engineer Toolkit (SET) Workflow:**

**Launch SET:**
```bash
setoolkit
```

**Menu Navigation:**
```
1 → Social-Engineering Attacks
5 → Mass Mailer Attack
1 → E-Mail Attack Single Email Address
```

**Configuration Template:**
```
Send email to: [target@example.com]
Delivery: Use your own server or open relay (option 2)
From address: [spoofed@trusted.com]
From name: [Trusted Company Name]
SMTP server: [target mail server IP]
Port: 25 (default SMTP)
High priority: no
Attach file: n
Subject: [Convincing business-related subject]
Body: [Professional message with malicious link]
END (to finish)
```

**Crafting Convincing Pretexts:**

**Elements of Believable Phishing:**
1. ✅ **Known sender:** Impersonate entity target trusts
2. ✅ **Business context:** Legitimate reason for communication
3. ✅ **Professional tone:** No spelling errors, proper grammar
4. ✅ **Subtle urgency:** "Please confirm" vs. "URGENT ACTION REQUIRED"
5. ✅ **Realistic request:** Something target would expect

**Example Template:**
```
From: updates@[trusted-partner].com
Subject: [Business-Related Change]

Dear [target],
Kindly note that [plausible business reason].
Please [reasonable action] by visiting [malicious link].
Best regards,
[Trusted Company Name]
```

### Phishing Detection Indicators (SOC Analyst Perspective)

**Email Header Red Flags:**
- Display name doesn't match actual email address
- Sender domain misspelled (microsft.com vs microsoft.com)
- Reply-to address differs from sender address
- Missing or failing SPF/DKIM/DMARC checks

**Message Content Red Flags:**
- Generic greetings ("Dear Customer" vs. your actual name)
- Spelling/grammar errors
- Suspicious links (hover to preview destination)
- Urgent threats ("Account will be locked!")
- Too-good-to-be-true offers
- Unexpected attachments

**Link Analysis:**
```bash
# Always hover before clicking to see real destination
# Check for:
- HTTP vs HTTPS (many phishing sites use HTTP)
- Misspelled domains (g00gle.com)
- Suspicious TLDs (.tk, .ml, .ga - often used in phishing)
- URL shorteners (bit.ly, tinyurl) hiding real destination
```

### Credential Compromise Incident Response

**Immediate Actions:**
1. ✅ Lock compromised account immediately
2. ✅ Force password reset
3. ✅ Review login history (identify unauthorized access)
4. ✅ Check for lateral movement (same credentials on other systems)
5. ✅ Assess data access (what did attacker see?)
6. ✅ Implement MFA if not already enabled
7. ✅ Alert security team and management

**Investigation Checklist:**
- When was credential entered on phishing page?
- Which systems were accessed with stolen credentials?
- Was data exfiltrated?
- Were additional accounts compromised?
- Is password reused across systems?

### SMTP and Email Delivery Basics

**SMTP (Simple Mail Transfer Protocol):**
- Default port: **25** (unencrypted)
- Secure alternatives: **587** (STARTTLS), **465** (SSL/TLS)
- Used for sending email between mail servers

**Why Email Spoofing Works:**
- SMTP doesn't verify sender identity by default
- Display name shown to users, not actual email address
- Without SPF/DKIM/DMARC, anyone can claim to be anyone

**Email Security Controls:**
- **SPF:** Specifies which servers can send email for domain
- **DKIM:** Cryptographic signature verifies email authenticity
- **DMARC:** Policy for handling failed SPF/DKIM checks

### Real-World Phishing Statistics

**Industry Data:**
- **90%** of data breaches start with phishing
- **85%** of organizations experienced phishing attacks
- **30%** of phishing emails are opened by targets
- **12%** of targets click malicious links
- **Average cost** of phishing attack: $4.65 million

**Most Targeted Industries:**
- Financial services
- Healthcare
- Technology
- Retail
- Government

### Red Team vs. Blue Team Perspectives

**Red Team (Offensive) - What I Did:**
- Created fake login page for credential harvesting
- Crafted convincing social engineering pretext
- Spoofed trusted sender (Flying Deer)
- Delivered phishing email via SMTP
- Captured and tested credentials

**Blue Team (Defensive) - What I'll Do as SOC Analyst:**
- Monitor for suspicious emails reported by users
- Analyze email headers for spoofing indicators
- Investigate credential compromise incidents
- Educate users on phishing detection
- Design security awareness training programs
- Test effectiveness through authorized phishing campaigns

### Security Awareness Best Practices

**Training Program Elements:**
1. ✅ Regular phishing simulations (monthly/quarterly)
2. ✅ Immediate feedback when users click (teachable moment)
3. ✅ Targeted training for repeat clickers
4. ✅ Positive reinforcement for reporting suspicious emails
5. ✅ Metrics tracking (click rate, report rate, time to report)

**User Education Focus:**
- Teach S.T.O.P. mnemonics
- Show real phishing examples
- Demonstrate how to verify sender authenticity
- Explain business impact of phishing
- Make reporting easy (one-click button)

### Authorized Penetration Testing Ethics

**Critical Requirements:**
- ✅ Written authorization from organization
- ✅ Defined scope (who can be targeted)
- ✅ Clear objectives (test awareness, not cause harm)
- ✅ Documented rules of engagement
- ✅ Incident response plan if user reports test

**Never do:**
- ❌ Phishing tests without authorization
- ❌ Targeting personal email addresses
- ❌ Using malware or destructive payloads
- ❌ Publicly shaming users who click

**Purpose:**
- Validate security awareness training effectiveness
- Identify vulnerable users/departments
- Improve organizational security posture
- Provide metrics for security leadership

---
