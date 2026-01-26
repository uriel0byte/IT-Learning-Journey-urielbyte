# Day 12: Phishing Analysis - Phishmas Greetings

## 📋 Quick Facts
- **Date Completed:** December 12, 2025
- **Time Spent:** 2 hours
- **Difficulty:** ★★★☆ (Medium-Hard)
- **Category:** Security Awareness / Phishing Analysis / Email Security
- **Room URL:** https://tryhackme.com/room/spottingphishing-aoc2025-r2g4f6s8l0

---

## 🎯 Challenge Overview

This challenge focused on advanced phishing detection after TBFC's Email Protection Platform went offline. With email filters disabled, staff had to manually triage every suspicious message. I joined the Incident Response Task Force to identify legitimate emails versus phishing attempts from Malhare's Eggsploit Bunnies. I learned to analyze email headers, spot impersonation techniques, identify typosquatting and punycode, detect email spoofing, and recognize modern phishing trends using legitimate platforms.

**Learning Objectives:**
- Learn to spot phishing emails through detailed analysis
- Understand trending phishing techniques used by modern attackers
- Differentiate between spam and phishing (different intentions, different risks)
- Analyze email headers for authentication failures and spoofing indicators

---

## 💡 What I Learned

### Phishing vs. Spam - Critical Difference

**From Professor Messer's Security+:** Learned surface-level definition of phishing

**From This Room:** First time diving deep into phishing analysis, techniques, and practical detection

**Spam (Digital Noise - Mostly Harmless):**
- **Focus:** Quantity over precision
- **Goal:** Push exposure or engagement, not steal data
- **Delivery:** Bulk messages to flood inboxes
- **Risk Level:** Low (annoying but not dangerous)

**Common Spam Intentions:**
- Promotion (advertising products, services, events)
- Scams (fake offers, "get rich quick" schemes)
- Traffic generation (clickbait to boost metrics)
- Data harvesting (collecting active email addresses)

**Phishing (Precision Strike - High Risk):**
- **Focus:** Precision and persuasion
- **Goal:** Deceive specific users to steal credentials/data
- **Delivery:** Carefully crafted, targeted messages
- **Risk Level:** High (direct security threat)

**Common Phishing Intentions:**
- **Credential theft** - Tricking users into revealing passwords/login details
- **Malware delivery** - Disguising malicious attachments or links as safe content
- **Data exfiltration** - Gathering sensitive company or personal information
- **Financial fraud** - Persuading victims to transfer money or approve fake invoices

**Key Takeaway:** Not every unwanted email is a threat. Look for the **intention** behind it. Spam is noise; phishing is a targeted attack.

### Phishing Technique #1: Impersonation

**What it is:** Attacker pretends to be a person, department, or service to gain credibility.

**Example from Challenge:**
- Email subject: "URGENT: McSkidy access for incident response"
- `From:` field shows McSkidy's name
- BUT sender's email: `[email protected]` (Gmail free domain)

**How to Spot It:**
- Check if sender's email matches **internal company domain**
- Look for **free email domains** (gmail.com, yahoo.com, outlook.com)
- Verify against company's **standard email structure**

**Red Flag:** TBFC employee using Gmail instead of @tbfc.com domain = clear impersonation

### Phishing Technique #2: Social Engineering

**What it is:** Manipulating people's emotions rather than breaking technology.

**Common Emotional Triggers:**
- **Fear** - "Your account will be locked!"
- **Helpfulness** - "Please help urgently needed"
- **Curiosity** - "You won't believe this..."
- **Urgency** - "Immediate action required"

**Social Engineering Indicators in McSkidy Email:**

**1. Impersonation:**
- Pretending to be McSkidy (trusted authority figure)

**2. Sense of Urgency:**
- Words like "URGENT" and "immediately" to pressure recipient
- Creates panic to bypass critical thinking

**3. Side Channel:**
- Discourages using standard communication channels (phone, email)
- "Don't contact me through normal means, use this sketchy link instead"

**4. Malicious Intention:**
- Asking for VPN credentials (massive red flag!)
- Could also request: payment approval, opening attachments, sharing sensitive data

**Key Learning:** Legitimate urgent requests from IT/management will ALWAYS allow verification through official channels.

### Phishing Technique #3: Typosquatting and Punycode

**First Time Learning:** This was completely new to me - never covered in Security+ at this depth.

**Typosquatting:**
- Attacker registers common **misspelling** of organization's domain
- Example: `glthub.com` instead of `github.com` (L instead of i)
- Relies on user's lack of attention or typing mistakes

**Punycode:**
- Special encoding system converting **Unicode characters** to ASCII
- Allows attackers to use visually identical characters from different alphabets
- Example: `tryhackme.com` vs. `тrуhackme.com` (Cyrillic т, г, у)

**Challenge Example:**
- Email subject: "TBFC-IT shared 'Christmas Laptop Upgrade Agreement' with you"
- Sender domain contains Latin `ƒ` instead of normal `f`
- **Looks legitimate to human eye but different to computers**

**How to Detect Punycode:**
Check email headers for `Return-Path` field:
- Legitimate domain: `example.com`
- Punycode domain: `xn--exmple-cua.com` (ACE prefix + encoded characters)

**Why It's Dangerous:** 
- Users won't notice the difference in email preview
- Domain looks identical or nearly identical
- Passes casual inspection

### Phishing Technique #4: Email Spoofing

**What it is:** Making an email **look** like it came from a legitimate domain, but headers reveal the truth.

**Challenge Example:**
- Email subject: "New Audio Message from McSkidy"
- `From:` field shows `[email protected]` (looks legitimate!)
- BUT email headers tell different story

**Email Header Analysis (First Time Learning This):**

**Key Headers to Check:**

**1. Authentication-Results:**
Shows if email passed security checks:
- **SPF (Sender Policy Framework)** - Which servers are allowed to send for this domain
- **DKIM (DomainKeys Identified Mail)** - Digital signature proving email wasn't changed
- **DMARC (Domain-based Message Authentication)** - Uses SPF + DKIM to decide what to do with suspicious emails

**In spoofed email:**
- SPF: FAIL
- DKIM: FAIL
- DMARC: FAIL

**If both SPF and DKIM fail = strong sign of spoofing**

**2. Return-Path:**
Shows the **real sender's email address**
- Display shows: `[email protected]`
- Return-Path shows: `[email protected]`

**Confirms spoofing!**

**Why Modern Email Clients Usually Block This:**
- Email authentication (SPF/DKIM/DMARC) is standard
- But with TBFC's email protection down, spoofed emails can pass!

### Phishing Technique #5: Malicious Attachments

**Classic Phishing Vector:** Attaching malicious files disguised as legitimate documents.

**Challenge Example:**
- Email claims to contain "voice message from McSkidy"
- Attachment appears to be an audio file
- **Actually:** `.html` file (dangerous!)

**Why HTML/HTA Files Are Dangerous:**
- Run **without browser sandboxing**
- Scripts have **full access to the endpoint**
- Can install malware, steal passwords, give attackers network access

**Common Malicious File Types:**
- `.html` / `.hta` - Run scripts with full system access
- `.exe` / `.bat` - Executable programs
- `.zip` / `.rar` - Compressed files hiding malware
- `.js` / `.vbs` - Script files
- Office docs with macros (.docm, .xlsm)

**Red Flag:** Unexpected attachments, especially with urgent/emotional messaging in email body

### Modern Phishing Trends (2025)

**Why Attackers Changed Tactics:**
- Email platforms got better at blocking malicious attachments
- Security tools detect suspicious files easily
- Attackers shifted to **social engineering + legitimate tools**

**New Strategy:**
1. **Don't send malware directly** - Too easily caught
2. **Trick users into leaving secure environment** - Company can't protect them on external sites
3. **Use legitimate platforms** - Links look trustworthy, pass email filters
4. **Make users download malware themselves** - User action = bypasses some defenses

**Modern Phishing Flow:**

```
Phishing Email
     ↓
Legitimate Platform Link (Dropbox, Google Drive, OneDrive)
     ↓
Fake Shared Document (attractive proposal)
     ↓
Fake Login Page OR Malicious Download
     ↓
Credential Theft OR Malware Installation
```

**Technique 1: Legitimate Applications Abuse**

**Attackers hide behind trusted services:**
- Dropbox
- Google Drive / Google Docs
- OneDrive
- SharePoint

**Attack Scenario:**
1. Email: "HR shared 'Salary Raise Document' with you"
2. Link goes to real OneDrive/Google Drive
3. Shared document contains fake content
4. Redirects to fake login page (steal credentials) OR malicious file download

**Example from Challenge:**
- Subject: "TBFC-IT shared 'Christmas Laptop Upgrade Agreement' with you"
- **Combines:**
  - Fake domain with punycode (trust manipulation)
  - Legitimate tool (OneDrive - passes filters)
  - Attractive proposal (laptop upgrade - social engineering)

**Technique 2: Fake Login Pages**

**Most Common Goal:** Steal credentials through fake authentication pages

**Typical Targets:**
- Email platforms (Gmail, Outlook)
- Microsoft Office 365 login
- Google Workspace login
- VPN portals
- Internal company portals

**Example Fake Login Page:**
- Looks identical to Microsoft login
- Fake domain: `microsoftonline.login444123.com/signin`
- Real domain: `login.microsoftonline.com`

**How to Spot:**
- Check URL carefully (domain name before first `/`)
- Look for HTTPS (but don't rely on it alone - attackers use HTTPS too)
- Verify domain matches official company/service domain

**Technique 3: Side Channel Communications**

**What it is:** Moving conversation off email to platforms without company security controls

**Channels Attackers Use:**
- SMS / Text messages
- WhatsApp / Telegram
- Phone calls / Video calls
- Shared document platforms
- Personal email

**Why It's Effective:**
- Company email filters can't monitor these channels
- IT security can't detect suspicious messages
- Users are more trusting on personal platforms
- Harder to verify sender identity

**Red Flag:** "Don't email me back, text me at this number instead"

### Phishing Analysis Workflow (What I Practiced)

**Step 1: Check Sender Information**
- Does email domain match company domain?
- Is it a free email service (Gmail, Yahoo)?
- Does name match email address?

**Step 2: Analyze Email Headers**
- Check `Authentication-Results` (SPF, DKIM, DMARC)
- Verify `Return-Path` matches `From:` address
- Look for punycode (ACE prefix in Return-Path)

**Step 3: Examine Email Body**
- Look for urgency language ("immediate", "urgent", "now")
- Check for emotional manipulation (fear, curiosity)
- Verify any claims through official channels

**Step 4: Inspect Links and Attachments**
- Hover over links (don't click!) to see real destination
- Check file extensions on attachments
- Verify legitimacy of shared document platforms

**Step 5: Identify Three Clear Signals**
- For each phishing email, identify 3 indicators:
  - Example: Spoofing + Impersonation + Malicious Attachment
  - Example: Typosquatting + Social Engineering + Fake Login Page

**Mission Completed:** Triaged all emails, separated spam from phishing, identified signals for each phishing attempt, collected flags!

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Wareville Email Threat Inspector** - Email analysis platform
2. **Email Header Analyzer** - Examining SPF/DKIM/DMARC authentication
3. **Return-Path Inspector** - Identifying real sender addresses
4. **Visual Inspection** - Spotting typosquatting and punycode

### Techniques
- **Email header analysis** - First time examining authentication results
- **Domain verification** - Checking sender domains against company domains
- **Punycode detection** - Identifying Unicode-to-ASCII encoding tricks
- **Spoofing identification** - Comparing display names with Return-Path
- **Social engineering recognition** - Spotting emotional manipulation
- **Malicious attachment detection** - Identifying dangerous file types
- **Link analysis** - Examining URLs for fake login pages
- **Triage methodology** - Classifying emails as spam, phishing, or legitimate

---

## 🤔 Challenges I Faced

**No Major Problems:** The room was well-structured and guided me through each technique.

**What Took Time:**
- **Lots of reading** - 2 hours spent reading and trying to understand concepts
- **First time diving deep into phishing** - Security+ only covered surface-level definition
- **New concepts:** Typosquatting, punycode, email header analysis (SPF/DKIM/DMARC)
- **Email headers** - First time actually looking at email authentication results

**Medium Difficulty Because:**
- **Volume of information** - Many different phishing techniques to learn
- **Practical application** - Had to actually classify emails, not just read theory
- **Got stuck identifying types** - When doing tasks, sometimes uncertain which phishing technique was primary

**What Was New:**
- **Spam vs. Phishing distinction** - Understanding different intentions and risks
- **Email authentication** - SPF, DKIM, DMARC (never learned this before)
- **Punycode** - Completely new concept, visually identical characters from different alphabets
- **Return-Path header** - Didn't know about this field before
- **Modern phishing trends** - Legitimate platform abuse, fake login pages, side channels

**Overall Experience:** Medium difficulty with a lot to learn. The room did excellent job explaining each technique with real examples. Took time to absorb everything, but now have solid foundation in phishing analysis.

---

## ✅ How This Helps My Career

Phishing analysis is a **core daily responsibility** for SOC analysts and one of the most critical security awareness skills:

**Why Phishing Analysis Matters:**
- **85% of SOC analyst job postings** mention phishing detection/awareness
- **90% of successful breaches** start with phishing emails
- **#1 attack vector** for initial access to corporate networks
- Phishing is the gateway to ransomware, data breaches, and financial fraud

**SOC Analyst Applications (Defensive):**

**Alert Triage & Investigation:**
- Review phishing alerts from email security platforms
- Analyze reported suspicious emails from users
- Determine if email is spam, phishing, or legitimate
- Identify phishing technique used (spoofing, typosquatting, etc.)

**Incident Response:**
- Investigate phishing incidents after users click malicious links
- Check email headers for authentication failures (SPF/DKIM/DMARC)
- Track down all recipients of phishing campaign
- Contain damage (reset credentials, block malicious domains)

**Threat Intelligence:**
- Extract IOCs (indicators of compromise) from phishing emails:
  - Sender domains
  - Malicious URLs
  - Attachment hashes
  - Email subject patterns
- Share IOCs with security community
- Update email filters and detection rules

**Security Awareness Training:**
- Educate users on phishing indicators
- Create phishing simulation campaigns
- Demonstrate real phishing examples to staff
- Build culture of "verify before you click"

**Email Security Improvement:**
- Recommend SPF/DKIM/DMARC implementation
- Configure email authentication policies
- Fine-tune email filters to reduce false positives
- Implement URL rewriting and attachment sandboxing

**Security Operations Center Applications:**

**Daily Monitoring:**
- Monitor email security platform alerts
- Triage user-reported suspicious emails
- Track phishing trends and campaigns
- Correlate phishing attempts with other security events

**Proactive Threat Hunting:**
- Search for emails with failed authentication (SPF/DKIM fail)
- Hunt for punycode domains in email logs
- Identify patterns in phishing campaigns
- Find emails with malicious attachment types

**Career Skills Developed:**
- **Email header analysis** - Understanding authentication mechanisms
- **Phishing technique recognition** - Spoofing, typosquatting, social engineering
- **Triage skills** - Quickly classifying email threats
- **Attention to detail** - Spotting subtle domain differences
- **Critical thinking** - Identifying intention behind messages
- **Communication** - Explaining phishing risks to non-technical users

**Real-World Impact:**
- Preventing credential compromise
- Stopping ransomware before it deploys
- Protecting company finances from wire fraud
- Maintaining trust in company communications

**Interview Talking Point:** "I have hands-on experience with phishing analysis, including email header examination for SPF/DKIM/DMARC authentication failures, identifying spoofing and typosquatting techniques, and detecting social engineering tactics. I can analyze email headers to identify the real sender through Return-Path analysis, recognize punycode domain abuse, and differentiate between spam and targeted phishing attacks. I understand modern phishing trends including legitimate platform abuse, fake login pages, and side-channel communication tactics. I've practiced triaging phishing emails by identifying three clear technical indicators per suspicious message, which directly applies to SOC analyst responsibilities in monitoring email security platforms and responding to user-reported phishing attempts."

---

## 🔗 Security+ Connection

**Domain 1.0 - General Security Concepts (12%):** Security awareness training, phishing prevention, social engineering defense.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Phishing attacks, social engineering techniques, email-based threats, impersonation, typosquatting, spoofing, malicious attachments.

**Domain 4.0 - Security Operations (28%):** Email security monitoring, incident detection, threat intelligence, user awareness, security controls (SPF/DKIM/DMARC).

---

## 📸 Evidence

![Email Header Analysis - Spoofing Detection](../07-Screenshots/day-12/email-headers-spoofing.png)
*Analyzed email headers showing SPF/DKIM/DMARC failures and Return-Path mismatch, confirming email spoofing attempt from Eggsploit Bunnies*

![Punycode Detection in Email Domain](../07-Screenshots/day-12/punycode-typosquatting.png)
*Identified punycode abuse using visually similar Latin character ƒ in sender domain, verified through Return-Path ACE prefix encoding*

![Phishing Email Triage Dashboard](../07-Screenshots/day-12/email-triage-signals.png)
*Successfully triaged 6+ phishing emails by identifying three clear signals per message (impersonation, social engineering, malicious attachments)*

---

## 📚 Key Takeaways for Future Reference

**Phishing Detection Checklist:**
- ✅ Check sender domain vs. company domain
- ✅ Analyze email headers (SPF/DKIM/DMARC)
- ✅ Verify Return-Path matches From address
- ✅ Look for urgency/fear language
- ✅ Check for punycode (ACE prefix in headers)
- ✅ Hover links to verify destinations
- ✅ Examine attachment file extensions
- ✅ Question attractive proposals (salary raises, upgrades)
- ✅ Verify requests through official channels

**Email Authentication:**
- **SPF Fail + DKIM Fail** = High probability of spoofing
- **Return-Path ≠ From** = Definite spoofing
- **Free domain from internal user** = Impersonation
- **Punycode (xn-- prefix)** = Typosquatting attempt

---