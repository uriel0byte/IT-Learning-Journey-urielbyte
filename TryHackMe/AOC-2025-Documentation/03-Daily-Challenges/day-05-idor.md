# Day 5: IDOR - Santa's Little IDOR

## 📋 Quick Facts
- **Date Completed:** December 5, 2025
- **Time Spent:** 3 hours
- **Difficulty:** ★★★☆ (Medium-Hard)
- **Category:** Web Security / Access Control Vulnerabilities
- **Room URL:** https://tryhackme.com/room/idor-aoc2025-zl6MywQid9

---

## 🎯 Challenge Overview

This challenge investigated access control vulnerabilities on the TryPresentMe website after suspicious activity involving a user named "Sir Carrotbane" who had accumulated unauthorized vouchers. I learned about IDOR (Insecure Direct Object Reference) vulnerabilities, explored different forms of object reference manipulation (numeric IDs, Base64, MD5 hashes, UUIDs), and understood the critical difference between authentication and authorization.

**Learning Objectives:**
- Understand the concepts of authentication and authorization
- Learn how to spot potential IDOR opportunities
- Exploit IDOR to perform horizontal privilege escalation
- Learn how to turn IDOR into SDOR (Secure Direct Object Reference)

---

## 💡 What I Learned

### Authentication vs. Authorization

This was a key concept that took time to understand:

**Authentication:** Verifying *who* you are (username + password → session token/cookie)
- Happens on every request via session information
- If session expires, you're redirected to login (reauthentication required)

**Authorization:** Verifying *what you're allowed to do*
- Cannot happen before authentication (system must know who you are first)
- Checks permissions: "Can this user view this data? Perform this action?"

**Critical Rule:** Authorization cannot happen before authentication. If the system doesn't know who you are, it can't verify your permissions.

### What is IDOR?

**IDOR (Insecure Direct Object Reference)** is an access control vulnerability where a web application uses references (IDs) to determine what data to return but *doesn't verify if the user is authorized* to access that data.

**Simple Example:**
- URL: `https://awesome.website.thm/TrackPackage?packageID=1001`
- What if you change `packageID=1002`?
- If the server doesn't check authorization → you see someone else's package details

**Why it happens:**
Web applications use simple SQL queries like:
```sql
SELECT person, address, status FROM Packages WHERE packageID = value;
```

If there's no check that the requester *owns* that package, anyone can access any package by guessing IDs.

### Types of Privilege Escalation

**Horizontal Privilege Escalation (most IDOR cases):**
- You use a feature you're authorized to use
- But gain access to *someone else's data*
- Example: Viewing your account is allowed → but you view someone else's account

**Vertical Privilege Escalation:**
- You gain access to *more features/higher privileges*
- Example: Normal user performing admin actions

### IDOR Attack Techniques

I exploited IDOR in multiple forms on the TryPresentMe application:

**1. Simple Numeric ID Manipulation**
- Used Browser Developer Tools (Network tab + Storage tab)
- Found `user_id=10` in Local Storage (`auth_user` data)
- Changed `user_id` to `11` → immediately viewed another user's account
- This is the most basic IDOR: sequential numeric IDs without authorization checks

**2. Base64 Encoded IDs**
- Clicked "view child" icon → Network request showed `Mg==`
- Decoded Base64: `Mg==` = `2`
- To exploit: Base64 encode different numbers and test requests
- *Lesson:* Encoding is NOT security; it's just obfuscation

**3. MD5 Hashed IDs**
- Some references appeared as MD5 hashes
- If you understand what value was hashed (e.g., sequential child IDs)
- You can replicate the hash function and brute force valid hashes
- Used hash identifiers to determine hashing algorithm

**4. UUID Version 1 Predictability**
- Voucher codes used UUID v1 format
- **Critical flaw:** UUID v1 includes timestamp information
- If you know when vouchers were generated (e.g., 20:00-21:00)
- You can generate all possible UUIDs for that timeframe (3600 UUIDs for 1 hour)
- Brute force attack to recover valid vouchers

### How to Fix IDOR (SDOR - Secure Direct Object Reference)

**✅ Server-side authorization checks (ESSENTIAL):**
- Always verify: *"Does this user own or have permission to view this item?"*
- Check on EVERY request, not just login

**❌ Don't rely on obfuscation:**
- Base64, hashing, or random-looking IDs don't fix IDOR
- If authorization checks are missing, it's still vulnerable

**✅ Use unpredictable references:**
- Random or hard-to-guess IDs for public links
- But remember: randomness alone ≠ security

**✅ Monitor and log:**
- Record failed access attempts
- Early signs of IDOR exploitation attempts

**✅ Test your application:**
- Try accessing another user's data while logged in as different user
- Ensure it's blocked by authorization logic

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Browser Developer Tools** - Network tab (inspect requests), Storage tab (Local Storage manipulation)
2. **Base64 Decoder** - Decode obfuscated IDs
3. **Hash Identifier** - Determine hashing algorithms (MD5, SHA1, etc.)
4. **CyberChef** - Decode/encode various formats
5. **Burp Suite (optional bonus)** - Intruder for automated IDOR testing

### Techniques
- Parameter manipulation (changing `user_id` values)
- Local Storage tampering (modifying session data)
- Base64 encoding/decoding for ID obfuscation bypass
- Hash replication (understanding hash inputs to reproduce valid hashes)
- UUID timestamp exploitation (generating UUIDs based on known timeframes)
- Horizontal privilege escalation exploitation
- Authorization bypass testing

---

## 🤔 Challenges I Faced

**Understanding Authentication vs. Authorization:** This conceptual difference was confusing at first. It took time to grasp that authentication happens on *every request* (via session cookies), not just at login, and that authorization *depends on* authentication.

**Playing with ID Values:** I had to manually test different ID values in URLs and request bodies to see how the IDOR worked. Trial and error was necessary to understand the behavior.

**Web Security Mindset:** Overall, this challenge took a lot of time to understand these new concepts. To be honest, it was kind of confusing for me—**I don't really like web stuff**, but I recognize I need to learn it to have a strong foundation in cybersecurity.

**Burnout and Confidence:** This room took a lot of time and kind of burned me out a little bit. I'm still not confident about web security topics, but I'm committed to building that foundation even though it's not my favorite area.

**Why it was hard:**
- First exposure to web access control concepts
- Understanding how references (numeric, Base64, hashed, UUIDs) work
- Connecting theory (authentication/authorization) to practical exploitation
- Web application testing requires a different mindset than other security domains

---

## ✅ How This Helps My Career

Despite not enjoying web security as much, **IDOR and access control vulnerabilities are critical for SOC analysts and penetration testers**:

**Why IDOR Matters:**
- **50% of SOC analyst job postings** mention web security skills
- Access control flaws are consistently in **OWASP Top 10** (Broken Access Control is #1 in 2021)
- Real-world impact: Data breaches, privacy violations, financial fraud

**SOC Analyst Perspective (Defensive):**
- **Web application firewall (WAF) alerts** often flag suspicious parameter manipulation
- **Log analysis** can reveal IDOR exploitation attempts (unusual ID access patterns)
- **Incident investigation** requires understanding how attackers exploit authorization flaws

**Penetration Testing Perspective (Offensive):**
- IDOR testing is a standard part of web application penetration tests
- Understanding different reference types (Base64, hashes, UUIDs) is essential
- Helps identify common developer mistakes during security assessments

**Authentication/Authorization Framework:**
This challenge taught me the foundation of access control, which applies beyond web:
- API security (same IDOR principles apply)
- Database access control
- Cloud IAM (Identity and Access Management) concepts

**Interview Talking Point:** "I've identified and exploited IDOR vulnerabilities in web applications, including bypassing Base64 obfuscation, hash-based references, and UUID v1 timestamp exploitation. I understand the critical difference between authentication and authorization, and how missing authorization checks lead to horizontal privilege escalation. While web security isn't my strongest area, I recognize its importance and have hands-on experience testing access control mechanisms."

---

## 🔗 Security+ Connection

**Domain 1.0 - General Security Concepts (12%):** Authentication vs. authorization, access control models, least privilege principle.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** OWASP Top 10, web application vulnerabilities, access control weaknesses, privilege escalation.

**Domain 3.0 - Security Architecture (18%):** Web application security architecture, session management, authorization enforcement.

---

## 📸 Evidence

![IDOR User ID Manipulation](../07-Screenshots/day-05/user-id-local-storage.png)
*Modified user_id in Local Storage from 10 to 11, gaining access to another user's account without authorization checks*

![Base64 Encoded IDOR](../07-Screenshots/day-05/base64-child-id.png)
*Discovered Base64-encoded child IDs (Mg== = 2) demonstrating that encoding is not security*

![Developer Tools IDOR Testing](../07-Screenshots/day-05/network-tab-idor.png)
*Used Browser Developer Tools Network tab to inspect requests and identify IDOR vulnerability in view_accountinfo endpoint*

---