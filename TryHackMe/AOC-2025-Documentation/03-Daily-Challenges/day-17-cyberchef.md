# Day 17: CyberChef - Hoperation Save McSkidy

## 📋 Quick Facts
- **Date Completed:** December 17, 2025
- **Time Spent:** 2 hours
- **Difficulty:** ★★★☆ (Medium-Hard)
- **Category:** Encoding/Decoding / Cryptography / Web Inspection / CyberChef
- **Room URL:** https://tryhackme.com/room/encoding-decoding-aoc2025-s1a4z7x0c3

---

## 🎯 Challenge Overview

This challenge focused on breaking five security locks to help McSkidy escape King Malhare's Quantum Warren. The locks progressively introduced encoding/decoding concepts using CyberChef (Cyber Swiss Army Knife). I had to inspect web application headers and login logic, decode Base64-encoded guard messages, chain multiple encoding operations, understand XOR encryption theory, crack MD5 hashes, and apply complex multi-step decoding recipes. The challenge tested both cryptographic knowledge and practical web inspection skills.

**Learning Objectives:**
- Understand encoding vs. encryption (purpose, process, security)
- Learn to use CyberChef for encoding/decoding operations
- Extract information from web page headers (Network tab)
- Analyze login logic through browser Debugger
- Chain multiple CyberChef operations
- Understand XOR (exclusive OR) and its reversible properties
- Use online hash cracking tools (CrackStation)
- Apply complex multi-step decoding recipes

---

## 💡 What I Learned

### Encoding vs. Encryption - Critical Distinction

**This is FUNDAMENTAL to understand:**

| Aspect | Encoding | Encryption |
|--------|----------|-----------|
| **Purpose** | Compatibility, Usability | Security, Confidentiality |
| **Process** | Standardized algorithm | Algorithm + Secret Key |
| **Security** | NO security | YES secure |
| **Speed** | Fast | Slow |
| **Reversible** | Yes (deterministic) | Yes (with key) |
| **Examples** | Base64, Hex, ROT13 | AES, RSA, XOR (with key) |

**Key Insight:** Encoding ≠ Encryption

- **Encoding:** Anyone can decode (no key needed)
- **Encryption:** Only those with key can decrypt
- Encoding is for **compatibility**, not **security**

**What This Means:**
If someone encodes a password in Base64, it's NOT secure. Anyone can decode it. But in this challenge, guards used encoding as a step in multi-layer security.

### CyberChef - The Cyber Swiss Army Knife

**What is CyberChef?**

Free, open-source web tool for encoding, decoding, encryption, decryption, and data analysis.

**Why CyberChef Matters:**
- ✅ Chain operations easily
- ✅ Visual recipe building (drag-and-drop)
- ✅ Instant output
- ✅ 300+ operations available
- ✅ No installation needed (web-based)
- ✅ Perfect for CTFs and cryptography challenges

**CyberChef Interface:**

| Area | Purpose |
|------|---------|
| **Operations** (left) | Repository of encoding/decoding operations |
| **Recipe** (center) | Drag operations here to create chain |
| **Input** (bottom-left) | Paste your encoded/encrypted data |
| **Output** (right) | Shows result of recipe |

**Simple Example Used in Challenge:**

1. Drag "To Base64" operation to Recipe
2. Type "IamRoot" in Input
3. See Base64 output: `SWFtUm9vdA==`
4. Drag "From Base64" operation after first
5. See original text again: `IamRoot`

**Key Capability:** Chain operations (input → operation 1 → operation 2 → operation 3 → output)

### Web Inspection - Finding Hidden Information

**This was NEW to me in practical application:**

Modern web applications hide information in multiple places:

**1. Page Headers (Network Tab)**

**How to Access:**
- Chrome: `More tools > Developer tools`
- Firefox: `Menu > More tools > Web Developer Tools`
- Edge: `Settings > More tools > Developer tools`

**What to Look For:**
- Custom headers (X-Magic, X-Password, etc.)
- Server information
- Hidden metadata
- Magic questions or clues

**Example from Challenge:**
Header contained: `X-Magic: Identify the guard's name`

This header was the "magic question" we had to answer!

**2. Debugger Tab (Browser Developer Tools)**

**What to Look For:**
- JavaScript code (app.js, login.js)
- Login logic and validation
- Comments explaining encoding/decoding
- Hidden business logic

**Example from Challenge:**
```javascript
// Lock 1: Password is Base64 encoded
const decodedPassword = base64decode(guardPassword);

// Lock 3: Password is XORed then Base64 encoded
const xorResult = xor(password, key);
const decodedPassword = base64decode(xorResult);

// Lock 4: Password is MD5 hashed
const hash = md5(password);
```

Comments in code told us exactly what encoding to reverse!

### Five Locks - Progressively Complex

**Lock 1: Outer Gate - Base64 Introduction**

**Concept:** Simple Base64 encoding

**Steps:**
1. Identify guard name from page
2. Encode guard name to Base64 (username)
3. Find magic question in headers
4. Encode magic question to Base64
5. Send to guard in chat (Base64-encoded)
6. Guard replies with encoded password
7. Decode guard's reply with "From Base64"
8. Use Base64 username + plaintext password to login

**Encoding Chain:**
```
Guard name → [Base64 encode] → Username
Magic question → [Base64 encode] → Chat message
Guard reply → [Base64 decode] → Plaintext password
```

**What I Learned:** Base64 is fundamental for data compatibility

---

**Lock 2: Outer Wall - Double Encoding**

**Concept:** Base64 applied TWICE

**Steps:**
1. Encode guard name to Base64 (as before)
2. Get encoded password from guard
3. Decode Base64 → DECODE Base64 AGAIN (two operations!)
4. Result is plaintext password

**Decoding Chain:**
```
Guard reply → [From Base64] → Still looks encoded!
Result → [From Base64] → Plaintext password
```

**Key Insight:** When login logic applies Base64 twice, you must decode twice!

**CyberChef Recipe:**
1. Add "From Base64" operation
2. Add "From Base64" operation again (chained)
3. Paste encoded guard reply
4. Get plaintext password

---

**Lock 3: Guard House - XOR Encryption**

**Concept:** XOR (exclusive OR) with a key

**What is XOR?**

Bitwise operation that takes a data input and a key:
- `data XOR key = encrypted_result`
- `encrypted_result XOR key = original_data` (reversible!)

**Magic Property of XOR:**
When you XOR a result with the SAME key again, you get back original data!

```
plaintext → XOR with key → ciphertext
ciphertext → XOR with same key → plaintext
```

**Example:**
```
Message: "Hi"
Key: "secret"
Encrypted: [binary XOR result]
Decrypt: [binary XOR result] XOR "secret" = "Hi"
```

**Why This Matters:**
- XOR is reversible (unlike hashing)
- XOR is NOT encryption (no security!)
- XOR is often used in combination with other operations

**Lock 3 Process:**

**Steps:**
1. Get encoded guard name
2. Ask guard for password (short message like "Password please.")
3. Guard responds with encoded result
4. Look at login logic: `XOR_with_key(password) → Base64 encode`

**To Reverse:**
```
Guard reply → [From Base64] → XOR result
XOR result → [XOR with same key] → Plaintext password
```

**In CyberChef:**
1. Add "From Base64" operation
2. Add "XOR" operation with the extracted key
3. Paste guard reply
4. Get plaintext password

**What I Learned:** XOR reversibility is powerful for forensics; if attacker uses XOR, we can recover original data!

**Important Note:** Guards took longer to respond from Lock 3 onwards (~2-3 minutes). Keeping messages short helped.

---

**Lock 4: Inner Castle - MD5 Hash Cracking**

**Concept:** One-way hashing (no mathematical reversal possible)

**What is MD5?**

Cryptographic hash function that:
- Takes ANY input (password, file, etc.)
- Produces **fixed-size 128-bit hash** (32 hexadecimal characters)
- **ONE-WAY:** Cannot mathematically reverse hash to get original
- **Deterministic:** Same input always produces same hash
- **NOT SECURE:** Collisions found, widely cracked

**Example:**
```
Input: "Password123"
MD5 Hash: "482c811da5d5b4bc6d497ffa98491e38"

Input: "password123" (lowercase)
MD5 Hash: "482c811da5d5b4bc6d497ffa98491e38" 
(Different! MD5 is case-sensitive)
```

**How to Crack MD5 (Hash Reversal):**

Since MD5 cannot be reversed mathematically, attackers use **precomputed hash tables**:

1. Take common passwords (millions of them)
2. Compute MD5 hash for each
3. Store in database: `hash → plaintext`
4. When you have a hash, lookup in database
5. Get plaintext password!

**Real-World Tools:**
- **CrackStation** (free online) - https://crackstation.net/
- **HashCat** (offline)
- **John the Ripper**
- **Online hash database** - md5.gromweb.com

**Lock 4 Process:**

**Steps:**
1. Ask guard for password
2. Guard responds with encoded/hashed data
3. Login logic shows: `MD5(password)`
4. We have the MD5 hash, need the plaintext

**To Get Password:**
1. Copy the MD5 hash
2. Go to CrackStation.net
3. Paste hash in search box
4. Click "Crack Hashes"
5. Get plaintext password!

**What I Learned:** Even "one-way" hashes can be reversed using precomputed tables; this is why password hashing algorithms use salt!

---

**Lock 5: Prison Tower - Complex Multi-Step Recipe**

**Concept:** Different encoding combinations based on Recipe ID

**Challenge:** Sir BreachBlocker III implemented **variable defense mechanisms** that change occasionally

**Recipe ID Approach:**

Header contains Recipe ID (1, 2, 3, or 4), each with different decoding logic:

| Recipe ID | Reverse Logic |
|-----------|---------------|
| **1** | From Base64 → Reverse → ROT13 |
| **2** | From Base64 → From Hex → Reverse |
| **3** | ROT13 → From Base64 → XOR (extracted key) |
| **4** | ROT13 → From Base64 → ROT47 |

**What These Operations Do:**

**ROT13:**
- Rotates each letter 13 positions in alphabet
- Example: A→N, B→O, Z→M
- Reversible: ROT13 applied twice = original
- Very weak encryption (just for fun)

**ROT47:**
- Like ROT13 but for printable ASCII (47 characters)
- Includes letters, numbers, symbols
- Reversible like ROT13

**XOR (with extracted key):**
- Reverse the XOR encryption using stored key

**Lock 5 Example Flow:**

If Recipe ID = 1:
1. Get encoded guard name (for username)
2. Get encoded password from guard
3. In CyberChef, build recipe:
   - Operation 1: "From Base64"
   - Operation 2: "Reverse"
   - Operation 3: "ROT13"
4. Paste guard reply
5. Get plaintext password
6. Login with credentials

**What I Learned:** Real security sometimes uses "security through obfuscation" (combining multiple weak techniques to create stronger defense)

### Understanding the Complete Challenge Flow

**General Pattern Across All Locks:**

```
1. WEB INSPECTION
   ├─ Find guard name (page content or headers)
   ├─ Identify magic question (in headers, X-Magic)
   └─ Extract key (if needed)

2. COMMUNICATION WITH GUARD
   ├─ Encode guard name to Base64
   ├─ Encode magic question / simple message to Base64
   ├─ Send to guard in chat
   └─ Wait for reply (gets longer from Lock 3+)

3. ANALYZE LOGIN LOGIC
   ├─ Open Developer Tools → Debugger
   ├─ Find app.js or login logic
   └─ Read comments to understand encoding/decoding

4. BUILD CYBERCHEF RECIPE
   ├─ Reverse the encoding steps from login logic
   ├─ Chain operations in correct order
   └─ Apply to guard's reply

5. EXTRACT PASSWORD
   ├─ Get plaintext password from CyberChef
   └─ Use with Base64-encoded username to login
```

### Web Inspection Features I Practiced

**1. Network Tab:**
- Shows HTTP requests and responses
- Headers (metadata about request/response)
- Status codes (200, 401, 500, etc.)
- Refresh page AFTER opening Network tab
- Select first response to examine headers

**2. Debugger Tab:**
- Shows JavaScript source code
- View application logic
- Find login validation
- Read code comments
- Set breakpoints (advanced)

**3. Inspector Tab (Bonus):**
- View HTML structure
- Find element attributes
- CSS styling
- Hidden input fields

**What I Learned:** Modern browsers give us powerful tools to analyze web applications; security-conscious developers should minimize information leakage in these areas!

---

## 🛠️ Tools & Techniques Used

### Tools
1. **CyberChef** - Encoding/decoding operations (drag-and-drop)
2. **Browser Developer Tools** - Network tab, Debugger tab
3. **CrackStation** - MD5 hash cracking (online)
4. **Firefox/Chrome** - Web inspection and analysis
5. **Text Editor** - Note-taking during investigation

### Techniques
- **Base64 encoding/decoding** - Data compatibility
- **Double encoding** - Chaining Base64 operations
- **XOR encryption/decryption** - Reversible operations with keys
- **MD5 hash cracking** - Precomputed hash lookup
- **ROT13/ROT47** - Letter rotation ciphers
- **Multi-step decoding** - Chaining operations in correct order
- **Web header inspection** - Finding hidden metadata
- **JavaScript analysis** - Understanding login logic
- **CyberChef recipe building** - Visual operation chaining

---

## 🤔 Challenges I Faced

**Fun Topic, Prior Knowledge, Some Challenges**

**Personal Background:**
- "I've learnt and tried familiar with cryptography with picoCTF, HackTheBox, TryHackMe CTF"
- **Already have cryptography foundation!**
- CTF experience helps significantly

**What Was Challenging:**

**1. Web Inspector Features (NEW):**
- Network tab - Finding the right response header
- Debugger tab - Reading JavaScript code
- X-Magic header - Understanding what it meant
- app.js structure - Following the login logic
- **These are practical skills beyond CTF knowledge**

**2. XOR Concept:**
- Understanding XOR is reversible (vs. one-way hash)
- Applying XOR in CyberChef correctly
- Knowing when to use XOR vs. Base64
- **Cryptographic theory + practical application**

**3. MD5 Hash Cracking:**
- Never manually cracked MD5 before (CTFs often provide tools)
- Finding CrackStation and using it
- Understanding precomputed hash tables
- **Practical hacking skill beyond theory**

**4. Lock 5 - Prison Tower (Complex!):**
- Multiple possible Recipe IDs
- Matching correct Recipe ID to decoding logic
- Chaining 3-4 operations in correct order
- Different combinations for different scenarios
- **Most technically challenging lock**

**5. Application Understanding:**
- Understanding chat is Base64 encoded
- Guards take longer to respond (patience!)
- Keeping messages short helps
- Reading code comments (trial and error)
- **Application-specific knowledge**

### What Clicked:

**CyberChef Workflow:**
- Drag-and-drop was intuitive
- Seeing results instantly helped
- Chaining operations made sense after trying
- **Visual approach > command-line tools**

**Web Inspection:**
- Developer tools are powerful
- Headers contain clues
- Debugger shows actual logic
- **Browser is a security testing tool!**

**Encoding Progression:**
- Lock 1: Simple Base64 ✅
- Lock 2: Double Base64 ✅
- Lock 3: Base64 + XOR ✅
- Lock 4: MD5 hash cracking ✅
- Lock 5: Multi-step recipes ✅
- **Each lock built on previous knowledge**

### What's Still Not Fully Understood:

**Quote:** "Most of the topics, I've seen and learnt but I still not complete understand and remember"

- **Memorizing all CyberChef operations** - 300+ options, which to use when?
- **Recognizing encoding types** - How to identify what's being used by looking at data?
- **Advanced CyberChef recipes** - What other operations chain together?
- **Real-world application** - When would organizations use these techniques?

**Overall Assessment:**
- "Fun, reviewing stuff, try new things, some challenging mission"
- Bridged gap between CTF theory and practical web application testing
- CyberChef is now a regular tool in security toolkit
- Web inspection skills valuable for penetration testing

---

## ✅ How This Helps My Career

Encoding/decoding and CyberChef are **critical for multiple security roles**:

**Why This Matters:**
- **Malware analysis** - Decoders obfuscated code
- **Web application security** - Test input validation
- **Network forensics** - Analyze network traffic encoding
- **Incident response** - Decode suspicious artifacts
- **Penetration testing** - Bypass basic security measures
- **CTF competitions** - Fundamental skill

**SOC Analyst / Incident Response Applications:**

**Malware Investigation:**
- Decode Base64 strings in malware samples
- Analyze encoded command-and-control messages
- Identify obfuscation techniques used
- Reverse engineer attacker payloads

**Web Application Testing:**
- Analyze network requests/responses in headers
- Test authentication mechanisms
- Find hardcoded secrets in JavaScript
- Identify weak encoding implementations

**Log Analysis:**
- Decode Base64 in application logs
- Find encoded commands in web server logs
- Identify suspicious patterns
- Extract evidence from encoded data

**Practical Example - Web Penetration Test:**
1. Capture login request in Burp Suite
2. See Base64-encoded credentials: `YWRtaW46cGFzc3dvcmQ=`
3. Decode in CyberChef: `admin:password`
4. Identify credentials transmitted insecurely
5. Report as critical vulnerability

**Practical Example - Incident Response:**
1. Found suspicious Registry entry: `powershell -enc VABoAGkAcwA...`
2. Decode Base64 in CyberChef
3. Reveals: `This is malware.exe`
4. Confirms malware presence
5. Use for remediation

**Career Skills Developed:**

✅ **Technical Skills:**
- CyberChef mastery (drag-and-drop operation chaining)
- Web inspector tools (Network, Debugger tabs)
- Encoding/decoding techniques
- Hash cracking methodology
- Data analysis and transformation

✅ **Security Skills:**
- Identifying weak security implementations
- Recognizing obfuscation techniques
- Understanding cryptographic concepts
- Web application analysis
- Malware analysis foundation

✅ **Investigative Skills:**
- Information extraction from web applications
- Pattern recognition in encoded data
- Logical deduction (matching logic to implementation)
- Evidence-based conclusions
- Systematic troubleshooting

**Career Progression:**

**Tier 1 - SOC Analyst:**
- Use CyberChef to decode suspicious data
- Follow incident playbooks
- Identify obvious encoding

**Tier 2 - Security Analyst / Incident Response:**
- Build custom CyberChef recipes
- Analyze web application security
- Identify complex obfuscation
- Write detection rules

**Tier 3 - Threat Analyst / Malware Analyst:**
- Reverse engineer obfuscated malware
- Develop deobfuscation tools
- Analyze command-and-control communications
- Publish research on encoding techniques

**Salary Implications:**
- Entry: CyberChef + basic decoding = $60K-$75K
- Mid: Advanced CyberChef + web testing = $80K-$110K
- Senior: Custom tools + research = $120K-$180K+

**Interview Talking Point:** "I have hands-on experience with CyberChef for encoding and decoding operations, including chaining multiple operations to decode complex obfuscated data. I understand the distinction between encoding and encryption, and can apply this knowledge to identify weak security implementations in web applications. I'm proficient with browser developer tools for inspecting HTTP headers, analyzing JavaScript login logic, and finding hidden metadata in web applications. I've practiced decoding Base64, XOR encryption, and cracking MD5 hashes using precomputed tables. While I'm still building comprehensive knowledge of all 300+ CyberChef operations, I have solid fundamentals and can quickly learn new encoding techniques as needed for investigations or penetration tests. This practical experience directly applies to malware analysis, incident response, and web application security testing."

---

## 🔗 Security+ Connection

**Domain 2.0 - Threats, Vulnerabilities & Mitigations (22%):** Encoding vs. encryption, cryptographic applications, obfuscation.

**Domain 3.0 - Cryptography & PKI (12%):** Encoding, hash functions, symmetric encryption, cryptographic concepts.

**Domain 4.0 - Security Operations (28%):** Tools and techniques for security operations, incident response, data analysis.

---

## 📸 Evidence

![CyberChef Multi-Step Recipe Chain](../07-Screenshots/day-17/cyberchef-recipe-chain.png)
*Built complex CyberChef recipe with chained operations: From Base64 → XOR with key → ROT13, demonstrating multi-step decoding for Lock 5*

![Web Inspector Headers and Magic Question](../07-Screenshots/day-17/web-inspector-headers.png)
*Used Network tab in browser developer tools to inspect HTTP headers, found X-Magic header containing magic question clue for guard*

![MD5 Hash Cracking with CrackStation](../07-Screenshots/day-17/crackstation-md5-lookup.png)
*Extracted MD5 hash from login logic, used CrackStation online tool to crack hash and retrieve plaintext password for Lock 4*

---

## 📚 Key Takeaways for Future Reference

**Encoding vs. Encryption Quick Reference:**

| Aspect | Encoding | Encryption |
|--------|----------|-----------|
| Purpose | Compatibility | Security |
| Reversibility | Yes (no key) | Yes (needs key) |
| Security | NO | YES |
| Examples | Base64, Hex, ROT13 | AES, RSA, XOR(key) |
| Speed | Very fast | Slower |
| Use Case | Data compatibility | Protecting secrets |

**Common Encodings to Know:**

| Encoding | Example | Use |
|----------|---------|-----|
| Base64 | `SWFtUm9vdA==` | Data transmission, obfuscation |
| Hex | `49616d526f6f74` | Binary data, data representation |
| ROT13 | `JnzSbbg` | Caesar cipher (weak) |
| ROT47 | Similar to ROT13 | Extended ASCII rotation |
| URL Encoding | `I%20am%20Root` | Web parameters |

**CyberChef Operations Cheat Sheet:**

**Common Decoding Operations:**
- `From Base64` - Decode Base64 strings
- `From Hex` - Convert hex to ASCII
- `XOR` - XOR operation (reversible with key)
- `ROT13` - Rotate letters 13 positions
- `ROT47` - Rotate ASCII 47 characters
- `Reverse` - Reverse string order
- `Unzip` - Decompress ZIP data

**Common Chaining Examples:**

**Double Base64:**
```
From Base64 → From Base64 → Result
```

**Base64 + XOR:**
```
From Base64 → XOR with key → Result
```

**Complex Multi-Step:**
```
From Base64 → From Hex → Reverse → ROT13 → Result
```

**Browser Developer Tools Quick Reference:**

**Network Tab:**
- Shows all HTTP requests/responses
- Inspect headers for metadata
- Check response body
- Identify API endpoints
- **Refresh page first!**

**Debugger Tab:**
- View JavaScript source code
- Find login/validation logic
- Read code comments
- Understand application flow
- Search for function names

**Inspector Tab:**
- View HTML structure
- Find hidden inputs
- Check CSS styling
- Identify element IDs/classes

**Hash Cracking Tools:**

| Tool | Type | Use |
|------|------|-----|
| CrackStation | Online | Common passwords, MD5 |
| HashCat | Offline | Large-scale cracking |
| John the Ripper | Offline | Complex hashes |
| Online databases | Lookup | Quick checks |

**Security Implications:**

❌ **Weak:** Base64 encoding passwords (anyone can decode)
❌ **Weak:** Sending encoded data in headers (still recoverable)
❌ **Weak:** MD5 hashing (precomputed tables crack instantly)
❌ **Weak:** XOR alone (reversible without key, easy to crack)

✅ **Better:** Encryption with keys (AES)
✅ **Better:** Password hashing with salt (bcrypt, Argon2)
✅ **Better:** HTTPS for transmission (TLS encryption)
✅ **Better:** Combining multiple techniques (defense in depth)

**Investigation Checklist:**

✅ **Data Classification:**
- Is this encoded or encrypted?
- What type of encoding? (Base64, Hex, ROT13, etc.)

✅ **Web Application Analysis:**
- Check headers (Network tab)
- Analyze login logic (Debugger tab)
- Find hidden fields or metadata
- Test input validation

✅ **Decoding Approach:**
- Build CyberChef recipe
- Chain operations logically
- Test with sample data
- Verify results

✅ **Hash Cracking:**
- Identify hash type (MD5, SHA1, etc.)
- Use appropriate tool (CrackStation first)
- Check online databases
- Fall back to offline tools if needed

---