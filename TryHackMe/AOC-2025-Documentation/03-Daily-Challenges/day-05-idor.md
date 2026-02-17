# Day 5: IDOR - Santa's Little IDOR

## 📋 Quick Facts
- **Date Completed:** December 5, 2025
- **Time Spent:** 3 hours
- **Difficulty:** ★★★☆ (Hard)
- **Category:** Web Security / Access Control Vulnerabilities
- **Room URL:** https://tryhackme.com/room/idor-aoc2025-zl6MywQid9

---

## 🎯 Challenge Overview

This challenge investigated access control vulnerabilities on the TryPresentMe website after a suspiciously named account, "Sir Carrotbane," accumulated unauthorized vouchers. Parents were unable to activate legitimate vouchers and were receiving targeted phishing emails containing private information—signs of a serious data breach. I learned about IDOR (Insecure Direct Object Reference) vulnerabilities, explored different forms of object reference manipulation, and understood how missing authorization checks lead to data exposure.

**Learning Objectives:**
- Understand the concepts of authentication and authorization
- Learn how to spot potential IDOR opportunities
- Exploit IDOR to perform horizontal privilege escalation
- Learn how to turn IDOR into SDOR (Secure Direct Object Reference)

---

## 💡 What I Learned

### Authentication vs. Authorization (Critical Concept)

**Authentication:** Verifying *who* you are
- Supplying username + password → receive session token/cookie
- Happens on **every subsequent request** (not just login)
- Session expiry → redirect to login for reauthentication

**Authorization:** Verifying *what you're allowed to do*
- Cannot happen **before** authentication
- Checks: "Does this user own or have permission to view this item?"
- Must be enforced on **every request**, server-side

**Critical Rule:**
```
Authentication  → Who are you?
Authorization   → What can you do?
One cannot exist without the other first.
```

### What is IDOR?

**IDOR (Insecure Direct Object Reference)** is an access control vulnerability where a web application uses references (IDs) to retrieve data but **doesn't verify if the requesting user is authorized** to access it.

**Simple Example:**
```
URL: https://site.com/TrackPackage?packageID=1001
Change to: https://site.com/TrackPackage?packageID=1002
Result: You see someone else's package details!
```

**Why it happens — the vulnerable SQL pattern:**
```sql
SELECT person, address, status FROM Packages WHERE packageID = value;
-- No check: "Does this user OWN packageID 1002?"
```

**Note from room co-author:** Some prefer calling this "Authorization Bypass" — which is more accurate. IDOR is the industry-standard name, but the root cause is always **missing authorization checks**.

### Four IDOR Attack Types I Practiced

**1. Simple Numeric ID (Most Basic)**
- Found `user_id=10` in Browser Dev Tools → Local Storage
- Changed to `user_id=11` → Instantly viewed another user's account
- Sequential IDs = predictable = vulnerable

**2. Base64 Encoded IDs**
- Network request showed `Mg==` for "view child"
- Decoded: `Mg== = 2` (just the number 2)
- **Key lesson:** Encoding ≠ Security. It's just obfuscation.

**3. MD5 Hashed IDs**
- References appeared as MD5 hashes
- If you understand what was hashed (sequential IDs), replicate the function
- Hash identifier tools reveal the algorithm used

**4. UUID Version 1 Predictability**
- Voucher codes used UUID v1 format
- **Critical flaw:** UUID v1 contains timestamp information
- Knowing vouchers generated between 20:00-24:00 → generate all 14,400 possible UUIDs
- Brute force the valid voucher

### Types of Privilege Escalation

**Horizontal (most IDOR cases):**
- Use authorized feature → access someone **else's data** at the same level
- Example: View your account ✅ → View another user's account ❌

**Vertical:**
- Gain access to **higher-privilege features**
- Example: Normal user → performing admin actions

### Fixing IDOR → SDOR (Secure Direct Object Reference)

**✅ What actually fixes it:**
- Server-side authorization check on **every request**: "Does this user own this item?"
- Random/unpredictable IDs for public links (but randomness alone ≠ security)
- Monitor and log failed access attempts (early IDOR detection)
- Test by trying to access another user's data while logged in

**❌ What does NOT fix it:**
- Base64 encoding IDs
- MD5 hashing IDs
- Making IDs "look random"
- Any client-side obfuscation

**Bottom line:** If the server doesn't verify authorization, the vulnerability exists regardless of how the ID looks.

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Browser Developer Tools** - Network tab (inspect requests), Storage tab (Local Storage)
2. **Base64 Decoder** - Decode obfuscated IDs
3. **Hash Identifier** - Determine hashing algorithm (MD5, SHA1, etc.)
4. **UUID Decoder** - Identify UUID version and timestamp extraction
5. **CyberChef** - Encode/decode various formats
6. **Burp Suite** - Intruder for automated brute force (bonus tasks)

### Techniques
- Local Storage manipulation (changing `user_id`)
- Base64 encoding/decoding bypass
- Hash algorithm identification and replication
- UUID v1 timestamp exploitation
- Horizontal privilege escalation
- Authorization bypass testing

---

## 🤔 Challenges I Faced

**Authentication vs. Authorization Confusion:** The conceptual difference was hard to grasp at first—especially that authentication happens on **every request** via session cookies, not just at login. It took a while to click.

**Web Security Mindset:** Honestly, **I don't really like web stuff**. This room burned me out a bit and took 3 hours. I'm still not confident with web security topics but I recognize building this foundation is necessary.

**UUID Exploitation:** Understanding that UUID v1 contains timestamp information and is therefore predictable was a completely new concept. The idea of generating 14,400 UUIDs for a 4-hour window made sense logically but was a lot to process.

**Overall:** Not my favorite domain, but committed to learning it anyway for a solid cybersecurity foundation.

---

## ✅ How This Helps My Career

**Why IDOR Matters:**
- **Broken Access Control = #1 in OWASP Top 10** (2021 and ongoing)
- **50% of SOC analyst job postings** mention web security skills
- Real-world impact: data breaches, privacy violations, financial fraud

**SOC Analyst Applications (Defensive - My Focus):**

**Alert Detection:**
- WAF (Web Application Firewall) alerts flag suspicious parameter manipulation
- Sequential ID access patterns in logs = IDOR exploitation in progress
- Example: User accessing `/account/10`, `/account/11`, `/account/12` rapidly

**Incident Investigation:**
- Understanding how attackers exploited authorization flaws
- Determining scope of data exposed (which accounts were accessed)
- Identifying if stolen vouchers/data are linked to phishing campaigns

**Risk Assessment:**
- Evaluating web applications for IDOR vulnerabilities
- Recommending server-side authorization controls
- Understanding OWASP Top 10 risk prioritization

**Authentication/Authorization Framework (Beyond Web):**
The same principles apply everywhere:
- **API security** - Same IDOR concepts apply to REST APIs
- **Cloud IAM** - Identity and Access Management
- **Database access control** - Row-level security

**Interview Talking Point:** "I have hands-on experience identifying IDOR vulnerabilities across multiple reference types—numeric IDs, Base64 encoding, MD5 hashes, and UUID v1 timestamp exploitation. I understand the critical distinction between authentication and authorization, and why server-side checks must be enforced on every request. From a defensive perspective, I can detect IDOR exploitation attempts through log analysis, recognize sequential access patterns in WAF alerts, and assess the scope of data exposure during incident investigations. I understand Broken Access Control as the #1 OWASP vulnerability and why it consistently leads to real-world data breaches."

---

## 🔗 Security+ Connection

**Domain 1.0 - General Security Concepts (12%):** Authentication vs. authorization, access control models, least privilege principle.

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** OWASP Top 10, web application vulnerabilities, access control weaknesses, privilege escalation.

**Domain 3.0 - Security Architecture (18%):** Web application security architecture, session management, authorization enforcement.

---

## 📸 Evidence

**Note:** Screenshots were not captured during initial completion. Documentation based on hands-on completion and room content review.

### Key Findings:
- Changed `user_id` from 10 → 11 in Local Storage to access another user's account
- Decoded Base64 `Mg==` = 2, demonstrating encoding is not security
- Identified MD5-hashed child IDs exploitable via hash replication
- Discovered UUID v1 voucher codes are timestamp-predictable (brute-forceable)
- Confirmed root cause: missing server-side authorization checks on every request

---

## 📚 Key Takeaways for Future Reference

### Core IDOR Concept

```
IDOR = Application uses IDs to retrieve data
     + No server-side check "Does this user OWN this ID?"
     = Anyone can access anyone's data
```

### Authentication vs. Authorization Quick Reference

| Concept | Question | When |
|--------|----------|------|
| **Authentication** | Who are you? | Every request (via session token) |
| **Authorization** | What can you do? | After authentication, every request |

**Session lifecycle:**
```
Login → Session token issued → Token sent with every request
Token expired → Redirect to login → Reauthenticate
```

### IDOR Types at a Glance

| Type | Example | How to Exploit |
|------|---------|---------------|
| **Numeric** | `user_id=10` | Increment/decrement numbers |
| **Base64** | `Mg==` | Decode → change → re-encode |
| **MD5 Hash** | `cfcd208...` | Identify algorithm → hash new values |
| **UUID v1** | `abc-def-...` | Extract timestamp → generate all UUIDs in window |

### Detecting IDOR Exploitation in Logs (SOC Focus)

**Red Flags to Watch For:**
```
# Sequential ID access in short timeframe
GET /account/10  [200 OK]
GET /account/11  [200 OK]
GET /account/12  [200 OK]
GET /account/13  [200 OK]
← This pattern = IDOR enumeration

# Rapid Base64 variant requests
GET /child/MQ==   [200 OK]   (= 1)
GET /child/Mg==   [200 OK]   (= 2)
GET /child/Mw==   [200 OK]   (= 3)
← Base64 IDOR enumeration

# Mass voucher claim attempts (UUID brute force)
POST /vouchers/claim  [400 Bad Request] × 14,399
POST /vouchers/claim  [200 OK] × 1
← UUID v1 timestamp brute force
```

**WAF Rules to Create:**
- Alert on sequential parameter access (>5 sequential IDs from same IP)
- Flag rapid requests to same endpoint with different ID values
- Monitor 400 errors followed by 200 success on voucher/account endpoints

### SDOR Checklist (Secure Direct Object Reference)

**For Developers (Reporting Findings):**
- [ ] Server-side check: "Does user X own resource Y?"
- [ ] Check applied on **every request**, not just login
- [ ] Use unpredictable IDs (UUIDs v4, not v1)
- [ ] Never rely on Base64/hashing for security
- [ ] Log and alert on failed authorization attempts
- [ ] Test by accessing other users' resources while authenticated

### OWASP Top 10 Context

**Broken Access Control = #1 (2021)**

Includes:
- IDOR
- Missing function-level access control
- Privilege escalation
- CORS misconfiguration
- JWT token manipulation

**Why #1?**
- Easy to exploit (just change a number)
- Hard to detect without proper logging
- Massive real-world impact (data breaches)

### Quick IDOR Testing Methodology

```
1. Authenticate to application
2. Use Developer Tools → Network tab
3. Identify requests with ID parameters:
   - Numeric: user_id=10
   - Encoded: Mg==
   - Hashed: cfcd208...
   - UUID: abc-def-ghi
4. Try changing the ID to another valid value
5. If you see different user's data → IDOR confirmed
6. Document: endpoint, parameter, data exposed
```

---
