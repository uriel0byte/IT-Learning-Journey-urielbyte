# Day 7: Network Discovery - Scan-ta Clause

## 📋 Quick Facts
- **Date Completed:** December 7, 2025
- **Time Spent:** 1 hour
- **Difficulty:** ★★☆☆ (Easy-Medium)
- **Category:** Network Security / Reconnaissance
- **Room URL:** https://tryhackme.com/room/networkservices-aoc2025-jnsoqbxgky

---

## 🎯 Challenge Overview

This challenge focused on network service discovery after HopSec breached TBFC's QA environment and locked everyone out of the `tbfc-devqa01` server. Using Nmap and various network tools, I performed reconnaissance to identify open ports, discovered hidden services (FTP, custom TBFC app, DNS), collected three key fragments, and ultimately regained access to the server's admin panel and MySQL database.

**Learning Objectives:**
- Learn the basics of network service discovery with Nmap
- Understand core network protocols (TCP, UDP, FTP, DNS, SSH, HTTP, MySQL)
- Apply reconnaissance skills to regain access to a compromised server

---

## 💡 What I Learned

### Network Service Discovery Strategy

**Engagement Workflow:**
1. **Know your target** - Identify IP address (`MACHINE_IP`)
2. **Scan for open ports** - Check common ports (22 SSH, 80 HTTP)
3. **Explore services** - Investigate what's running behind open ports
4. **Exploit weaknesses** - Find entry points and regain access

### Nmap Port Scanning Techniques

**1. Basic TCP Scan (Top 1000 Ports)**

```bash
nmap MACHINE_IP
```

**Output:**
- Port 22/tcp - SSH (Secure Shell)
- Port 80/tcp - HTTP (Web server)

This scans only the top 1000 most commonly used ports out of 65,535 total TCP ports.

**2. Full TCP Port Scan with Banner Grabbing**

```bash
nmap -p- --script=banner MACHINE_IP
```

**New flags learned:**
- `-p-` - Scan ALL 65,535 TCP ports (not just top 1000)
- `--script=banner` - Retrieve service banners to identify software versions

**Discovered:**
- Port 22/tcp - SSH-2.0-OpenSSH_9.6p1 Ubuntu
- Port 80/tcp - HTTP
- Port 21212/tcp - FTP (vsFTPd 3.0.5) ← **Non-standard FTP port!**
- Port 25251/tcp - Custom TBFC maintenance daemon v0.2

**Key lesson:** Services don't always run on default ports. FTP typically uses port 21, but can be configured on any port (in this case 21212).

**3. UDP Port Scan**

```bash
nmap -sU MACHINE_IP
```

**New flag:**
- `-sU` - Scan UDP ports instead of TCP

**Discovered:**
- Port 53/udp - DNS (Domain Name System)

**Critical concept:** There are TWO separate sets of 65,535 ports:
- 65,535 TCP ports
- 65,535 UDP ports

You must scan both protocols to find all services.

### Service Enumeration and Exploitation

**FTP Anonymous Access (Port 21212)**

```bash
ftp MACHINE_IP 21212
Name: anonymous
ftp> ls
ftp> get tbfc_qa_key1 -
```

**What I learned:**
- FTP "anonymous" login allows access without authentication (misconfiguration)
- Retrieved first key fragment from FTP server
- FTP can run on non-standard ports

**Netcat Service Interaction (Port 25251)**

```bash
nc -v MACHINE_IP 25251
HELP
GET KEY
```

**What I learned:**
- Netcat (`nc`) is a universal tool for interacting with network services
- `-v` flag enables verbose output
- Custom applications may expose management interfaces
- Retrieved second key fragment from TBFC maintenance daemon

**DNS TXT Record Query (Port 53 UDP)**

```bash
dig @MACHINE_IP TXT key3.tbfc.local +short
```

**What I learned:**
- `dig` performs advanced DNS queries
- `@MACHINE_IP` specifies which DNS server to query
- `TXT` requests text records (often used for configuration/secrets)
- `+short` provides concise output
- Retrieved third key fragment from DNS TXT record

### On-Host Service Discovery

After gaining access to the admin panel, I could enumerate services from inside the server.

**Listing Listening Ports with `ss`**

```bash
ss -tunlp
```

**Flags explained:**
- `-t` - TCP sockets
- `-u` - UDP sockets
- `-n` - Numeric (don't resolve hostnames/services)
- `-l` - Listening sockets only
- `-p` - Show process information

**Key discovery:** Services listening on `127.0.0.1` (localhost) vs. `0.0.0.0` (all interfaces)

**Listening on 0.0.0.0 (externally accessible):**
- Port 22 SSH
- Port 80 HTTP
- Port 53 DNS
- Port 21212 FTP
- Port 25251 TBFC app

**Listening on 127.0.0.1 (localhost only - not visible externally):**
- Port 3306 MySQL database
- Port 8000 Unknown service
- Port 7681 Unknown service

**Critical concept:** Services bound to `127.0.0.1` can ONLY be accessed from the host itself, not from external scans. This is why Nmap didn't detect MySQL.

**MySQL Database Access (Port 3306)**

```bash
mysql -D tbfcqa01 -e "show tables;"
mysql -D tbfcqa01 -e "select * from flags;"
```

**Flags explained:**
- `-D tbfcqa01` - Connect to database named `tbfcqa01`
- `-e "query"` - Execute a single query and exit

**What I learned:**
- MySQL default port is 3306
- Localhost connections often don't require authentication (security misconfiguration)
- Retrieved final flag from database `flags` table

### Network Protocols Reviewed

| Protocol | Default Port | Purpose | Tool Used |
|----------|--------------|---------|-----------|
| **SSH** | 22/tcp | Secure remote shell access | N/A (locked out) |
| **HTTP** | 80/tcp | Web server | Browser |
| **FTP** | 21/tcp (21212 here) | File transfer | `ftp` |
| **DNS** | 53/udp | Domain name resolution | `dig` |
| **MySQL** | 3306/tcp | Database server | `mysql` |
| **Custom** | 25251/tcp | TBFC maintenance | `nc` (netcat) |

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Nmap** - Network mapper for port scanning and service discovery
2. **FTP client** - File Transfer Protocol client for anonymous access
3. **Netcat (nc)** - Universal network tool for service interaction
4. **dig** - DNS query tool for TXT record retrieval
5. **ss** - Socket statistics utility (modern replacement for netstat)
6. **mysql** - MySQL database client for SQL queries

### Techniques
- **TCP port scanning** (top 1000 ports and full range)
- **UDP port scanning** (protocol-specific reconnaissance)
- **Banner grabbing** (service version identification)
- **Anonymous FTP enumeration**
- **Custom protocol interaction** (netcat)
- **DNS TXT record queries** (information disclosure)
- **Listening port enumeration** (on-host reconnaissance)
- **Localhost service exploitation** (MySQL unauthenticated access)

---

## 🤔 Challenges I Faced

**Not Particularly Challenging:** I've used Nmap before in other CTFs, so the basic scanning concepts were familiar. This was more of a review and skill reinforcement rather than encountering entirely new territory.

**Learning New Syntax:**
- `--script=banner` flag was new to me
- `mysql` program syntax and one-liner queries (`-e` flag)

**Reviewing Familiar Tools:**
- `ss -tunlp` - Refreshed understanding of socket statistics flags
- `dig` - Reviewed DNS query syntax, especially TXT records
- `ftp` program - Practiced anonymous login workflow
- `netcat (nc)` - Reviewed basic network service interaction

**Overall Experience:** This felt like practical application of knowledge I already had, with some new flags and tools added to my toolkit. It was satisfying to see how different network tools work together in a real reconnaissance workflow.

---

## ✅ How This Helps My Career

Network reconnaissance is a **foundational skill for both offensive (pentesting) and defensive (SOC) security roles**:

**Why Network Discovery Matters:**
- **65% of SOC analyst job postings** mention network security fundamentals
- Network scanning is the #1 reconnaissance technique in penetration testing
- Understanding exposed services is critical for attack surface management

**SOC Analyst Applications (Defensive):**

**Attack Surface Monitoring:**
- Identify unauthorized services running on company infrastructure
- Detect non-standard ports (like FTP on 21212 instead of 21)
- Find services bound to `0.0.0.0` that should be localhost-only

**Incident Detection:**
- Recognize Nmap scan patterns in network logs/IDS alerts
- Understand attacker reconnaissance TTPs (Tactics, Techniques, Procedures)
- Identify suspicious DNS queries (TXT record enumeration)

**Vulnerability Assessment:**
- Locate anonymous FTP servers (common misconfiguration)
- Find localhost-only services with weak authentication (MySQL)
- Map internal vs. external service exposure

**Penetration Testing Applications (Offensive):**

**Reconnaissance Phase:**
- Systematically discover all exposed services (TCP + UDP)
- Identify service versions for vulnerability research
- Enumerate misconfigurations (anonymous access, default credentials)

**Exploitation:**
- Prioritize targets based on service exposure
- Understand protocol-specific attack vectors
- Chain information disclosures (3 keys → admin access → database)

**Career Skills Developed:**
- **Nmap mastery** - Industry-standard reconnaissance tool
- **Protocol understanding** - TCP vs. UDP, localhost vs. external
- **Multi-tool proficiency** - FTP, netcat, dig, ss, mysql
- **Methodical approach** - Systematic enumeration and exploitation chain

**Interview Talking Point:** "I have hands-on experience with network reconnaissance using Nmap for both TCP and UDP scanning, including full port range enumeration and banner grabbing. I can enumerate services using protocol-specific tools like FTP, DNS (dig), and netcat, differentiate between externally accessible and localhost-only services using ss/netstat, and chain information disclosures to escalate access. I understand both offensive reconnaissance techniques and how to detect them from a defensive SOC perspective."

---

## 🔗 Security+ Connection

**Domain 3.0 - Security Architecture (18%):** Network architecture, port security, service placement, segmentation, attack surface reduction.

**Domain 4.0 - Security Operations (28%):** Reconnaissance techniques, vulnerability scanning, network monitoring, threat hunting, incident detection.

---

## 📸 Evidence

![Nmap Full Port Scan](../07-Screenshots/day-07/nmap-all-ports-banner.png)
*Nmap full TCP scan with banner grabbing revealing FTP on port 21212 and custom TBFC app on 25251*

![FTP Anonymous Access](../07-Screenshots/day-07/ftp-anonymous-key.png)
*Successfully accessed FTP server anonymously and retrieved first key fragment*

![Socket Statistics - ss tunlp](../07-Screenshots/day-07/ss-listening-ports.png)
*Used ss -tunlp to identify localhost-only MySQL database on port 3306*

---