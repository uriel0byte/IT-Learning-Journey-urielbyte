# Day 2: Phishing - Merry Clickmas

## 📋 Quick Facts
- **Date Completed:** December 2, 2025
- **Time Spent:** 2 hours
- **Difficulty:** ★★☆☆ (Medium)
- **Category:** Social Engineering / Red Team Operations
- **Room URL:** https://tryhackme.com/room/phishing-aoc2025-h2tkye9fzU

---

## 🎯 Challenge Overview

This challenge put me on the TBFC red team alongside Recon McRed, Exploit McRed, and Pivot McRed to conduct a phishing penetration test. The goal was to test if TBFC employees would fall for a phishing email and enter their credentials on a fake login page, validating whether security awareness training was effective.

**Learning Objectives:**
- Understand phishing and social engineering tactics
- Learn anti-phishing detection mnemonics (S.T.O.P.)
- Create fake login pages for credential harvesting
- Use Social-Engineer Toolkit (SET) to send phishing emails

---

## 💡 What I Learned

### Social Engineering & Phishing Fundamentals
**Social Engineering** exploits human psychology (urgency, curiosity, authority) rather than technical vulnerabilities. **Phishing** is message-based social engineering via email, SMS (smishing), calls (vishing), QR codes (quishing), or social media.

### The S.T.O.P. Anti-Phishing Mnemonics
**S.T.O.P. #1 (Pre-Click Questions):**
- **S**uspicious? Does something feel off?
- **T**elling me to click? Pressure to click links?
- **O**ffering amazing deals? Too good to be true?
- **P**ushing urgency? Must act now?

**S.T.O.P. #2 (Response Protocol):**
- **S**low down - Don't let adrenaline rush decisions
- **T**ype addresses yourself - Never use message links
- **O**pen nothing unexpected - Verify first
- **P**rove the sender - Check real address, not display name

### Building the Phishing Trap
I learned how to set up a complete phishing attack:
1. **Fake Login Page:** Used `server.py` to host a fake TBFC portal on port 8000 that captures credentials
2. **Email Delivery:** Used Social-Engineer Toolkit (SET) to craft and send convincing phishing emails
3. **Social Engineering:** Spoofed emails from "Flying Deer" (trusted shipping company) with subject "Shipping Schedule Changes"

**Result:** Successfully harvested credentials, proving employees were vulnerable despite security training.

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Social-Engineer Toolkit (SET)** - Phishing campaign automation (`setoolkit`)
2. **server.py** - Fake login page hosting and credential capture
3. **SMTP** - Email delivery protocol (port 25)
4. **Firefox** - Testing phishing page appearance

### Techniques
- Credential harvesting via fake login pages
- Email spoofing and sender impersonation
- Crafting convincing pretexts (business context exploitation)
- SMTP relay configuration
- Post-exploitation investigation (credential reuse testing)

---

## 🤔 Challenges I Faced

**Understanding SET Workflow:** SET has multiple nested menus and configuration steps. I had to be patient and follow each prompt carefully. One mistake means pressing `Ctrl+C` and starting over.

**Crafting Convincing Emails:** Writing a phishing email that's believable without being too suspicious required thinking about business context—why would Flying Deer email about shipping schedules? What would employees expect?

**Waiting for Results:** After sending the email, I had to wait 1-2 minutes for the simulated user to interact with it. This taught me patience in red team operations.

---

## ✅ How This Helps My Career

Phishing is involved in **90% of successful breaches**, making it the #1 initial access vector. As a future SOC Analyst, I need to understand both sides:

**Red Team Perspective (Offensive):**
- How attackers craft campaigns
- Psychological manipulation techniques
- Technical setup (fake pages, email spoofing)

**Blue Team Perspective (Defensive):**
- Detecting phishing indicators in emails
- Email header analysis (SPF/DKIM/DMARC)
- User behavior monitoring for credential compromise
- Incident response for phishing incidents

**Interview Talking Point:** "I've conducted hands-on phishing simulations using SET, understand both offensive and defensive perspectives, and can train users on the S.T.O.P. mnemonics for phishing detection."

---

## 🔗 Security+ Connection

**Domain 1.0 - General Security Concepts (12%):** Social engineering tactics, security awareness training programs.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Threat actors, phishing attack techniques, credential harvesting.

**Domain 4.0 - Security Operations (28%):** Security awareness best practices, incident detection and response.

---

## 📸 Evidence

![SET Phishing Campaign]()
*Configured Social-Engineer Toolkit to send spoofed phishing email from Flying Deer*

![Credential Capture]()
*Successfully captured admin credentials via fake TBFC login portal*

---
