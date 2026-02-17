# Day 7: Network Discovery - Scan-ta Clause

## 📋 Quick Facts
- **Date Completed:** December 7, 2025
- **Time Spent:** 1 hour
- **Difficulty:** ★★☆☆ (Easy-Medium)
- **Category:** Network Security / Reconnaissance
- **Room URL:** https://tryhackme.com/room/networkservices-aoc2025-jnsoqbxgky

---

## 🎯 Challenge Overview

HopSec breached TBFC's QA environment and locked everyone out of the `tbfc-devqa01` server, defacing the website and freezing the entire SOC-mas pipeline. With only the server's IP address available, I used Nmap and various network tools to systematically discover open ports, enumerate hidden services (FTP on non-standard port 21212, a custom TBFC maintenance app on 25251, DNS on UDP 53), collect three key fragments, and ultimately regain access to the admin panel and MySQL database to expose all of HopSec's secrets.

**Learning Objectives:**
- Learn the basics of network service discovery with Nmap
- Understand core network protocols (TCP, UDP, FTP, DNS, SSH, HTTP, MySQL)
- Apply reconnaissance skills to regain access to a compromised server

---

## 💡 What I Learned

### Network Reconnaissance Engagement Workflow

```
1. Know your target  → Identify IP address
2. Scan open ports   → Nmap (common ports first, then all)
3. Explore services  → Investigate what's behind each port
4. Exploit weaknesses → Find entry points and gain access
```

### Nmap Port Scanning Techniques

**1. Basic TCP Scan (Top 1000 Ports)**

```bash
nmap MACHINE_IP
```

**Output:**
```
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
```

Scans only the **top 1000 most commonly used ports** out of 65,535 total TCP ports. Fast but incomplete.

**2. Full TCP Port Scan with Banner Grabbing**

```bash
nmap -p- --script=banner MACHINE_IP
```

**Flags:**
- `-p-` → Scan ALL 65,535 TCP ports
- `--script=banner` → Retrieve service banners (identify software/version)

**Full scan output:**
```
PORT      STATE SERVICE
22/tcp    open  ssh
|_banner: SSH-2.0-OpenSSH_9.6p1 Ubuntu-3ubuntu13.14
80/tcp    open  http
21212/tcp open  trinket-agent
|_banner: 220 (vsFTPd 3.0.5)          ← FTP on non-standard port!
25251/tcp open  unknown
|_banner: TBFC maintd v0.2            ← Custom maintenance app
```

**Key lesson:** Services don't always run on default ports. FTP typically uses port 21 but was configured on **21212** here. Always scan all ports.

**3. UDP Port Scan**

```bash
nmap -sU MACHINE_IP
```

**Output:**
```
PORT   STATE SERVICE
53/udp open  domain    ← DNS!
```

**Critical concept:**
```
TCP ports: 65,535
UDP ports: 65,535 (completely separate set)

Must scan BOTH to find all services.
```

### Service Enumeration — What I Found and How

**FTP Anonymous Access (Port 21212)**

```bash
ftp MACHINE_IP 21212
Name: anonymous       # No password needed!
ftp> ls               # List files
ftp> get tbfc_qa_key1 -   # Download/display key
ftp> !                # Exit FTP shell
```

**Finding:** Key fragment 1 retrieved.

**Security issue:** FTP anonymous login = misconfiguration. Anyone can access without credentials.

---

**Netcat Service Interaction (Port 25251)**

```bash
nc -v MACHINE_IP 25251
# Server responds: TBFC maintd v0.2 - Type HELP for commands
HELP
# Response: Commands: HELP, STATUS, GET KEY, QUIT
GET KEY
# Response: Key fragment 2
# Ctrl+C to exit
```

**What netcat does:** Universal tool for interacting with ANY network service. If you don't know the protocol, use `nc` to explore.

**Finding:** Key fragment 2 retrieved.

---

**DNS TXT Record Query (Port 53 UDP)**

```bash
dig @MACHINE_IP TXT key3.tbfc.local +short
```

**Flags explained:**
- `@MACHINE_IP` → Use this specific DNS server
- `TXT` → Request text records
- `+short` → Concise output only

**Finding:** Key fragment 3 retrieved.

**Why DNS matters:** TXT records are frequently used to store configuration data, SPF records, verification tokens — and sometimes secrets left by attackers.

---

**On-Host Service Discovery (After Admin Access)**

Once inside the admin panel (using combined 3 keys), ran `ss -tunlp` to see ALL listening ports from inside:

```bash
ss -tunlp
```

**Flags:**
- `-t` → TCP sockets
- `-u` → UDP sockets
- `-n` → Numeric (no hostname resolution)
- `-l` → Listening only
- `-p` → Show process info

**Full output revealed:**

```
# Externally accessible (0.0.0.0):
0.0.0.0:22     → SSH
0.0.0.0:80     → HTTP
0.0.0.0:53     → DNS
0.0.0.0:21212  → FTP
0.0.0.0:25251  → TBFC app

# Localhost only (127.0.0.1) - invisible to Nmap:
127.0.0.1:3306  → MySQL database ← This is why Nmap missed it!
127.0.0.1:8000  → Unknown service
127.0.0.1:7681  → Unknown service
```

**Critical insight:** Services bound to `127.0.0.1` can ONLY be accessed from the host itself — invisible to external scans. This is why Nmap didn't detect MySQL.

---

**MySQL Database Access (Port 3306 — Localhost)**

```bash
mysql -D tbfcqa01 -e "show tables;"
mysql -D tbfcqa01 -e "select * from flags;"
```

**Flags:**
- `-D tbfcqa01` → Connect to database named `tbfcqa01`
- `-e "query"` → Execute query and exit

**Finding:** Final flag retrieved from `flags` table.

**Security issue:** MySQL on localhost allowing unauthenticated connections = misconfiguration. Once inside the host, database is fully open.

### Network Protocols Reference

| Protocol | Default Port | Transport | Purpose |
|----------|-------------|-----------|---------|
| SSH | 22 | TCP | Secure remote shell |
| HTTP | 80 | TCP | Web server |
| FTP | 21 (21212 here) | TCP | File transfer |
| DNS | 53 | UDP (+ TCP) | Domain name resolution |
| MySQL | 3306 | TCP | Database server |
| Custom | 25251 | TCP | TBFC maintenance |

---

## 🛠️ Tools & Techniques Used

### Tools
1. **Nmap** - Network mapper for port scanning and service discovery
2. **FTP client** - File Transfer Protocol client (anonymous access)
3. **Netcat (nc)** - Universal network interaction tool
4. **dig** - Advanced DNS query tool
5. **ss** - Socket statistics (modern `netstat` replacement)
6. **mysql** - MySQL command-line client

### Techniques
- TCP port scanning (top 1000 and full range `-p-`)
- UDP port scanning (`-sU`)
- Banner grabbing (`--script=banner`)
- Anonymous FTP enumeration
- Custom protocol interaction (netcat)
- DNS TXT record queries
- On-host listening port enumeration
- Localhost service exploitation

---

## 🤔 Challenges I Faced

**Not Particularly Challenging:** I've used Nmap before in other CTFs, so core concepts were familiar. More of a review and skill reinforcement.

**New Things Learned:**
- `--script=banner` flag (hadn't used this specific script before)
- `mysql` command-line syntax and `-e` flag for one-liner queries
- `dig` TXT record query syntax (`@server`, `+short`)

**What I appreciated:**
Seeing how multiple tools chain together in a real workflow — Nmap reveals ports → FTP/nc/dig enumerate services → ss reveals hidden services → mysql exploits localhost access. Each tool leads to the next.

---

## ✅ How This Helps My Career

**Why Network Discovery Matters:**
- **65% of SOC analyst job postings** mention network security fundamentals
- Network scanning is the #1 reconnaissance technique in penetration testing
- Understanding exposed services = critical for attack surface management

**SOC Analyst Applications (Defensive — My Focus):**

**Attack Surface Management:**
- Identify unauthorized services running on company infrastructure
- Detect non-standard ports (FTP on 21212 instead of 21)
- Find services bound to `0.0.0.0` that should be localhost-only
- Regular Nmap scans of own infrastructure = security hygiene

**Incident Detection:**
- Recognize Nmap scan patterns in IDS/SIEM alerts
  - Fast sequential port connections = port scan in progress
  - `-sU` scans create specific UDP traffic patterns
- Identify suspicious DNS TXT record queries (data exfiltration)
- Detect new services appearing on unexpected ports

**Threat Hunting:**
- Hunt for anonymous FTP servers (major misconfiguration)
- Identify MySQL/databases accessible without authentication
- Find custom applications on non-standard ports (shadow IT)

**Interview Talking Point:** "I have hands-on experience with network reconnaissance using Nmap for both TCP and UDP scanning, including full port range enumeration and banner grabbing. I can enumerate services using protocol-specific tools like FTP client, netcat, and dig, differentiate between externally accessible and localhost-only services using ss, and chain reconnaissance findings into system access. I understand how to detect Nmap scan patterns in SIEM alerts, identify attack surface misconfigurations like anonymous FTP and unauthenticated database access, and apply these skills for both offensive penetration testing and defensive attack surface management."

---

## 🔗 Security+ Connection

**Domain 3.0 - Security Architecture (18%):** Network architecture, port security, service placement, segmentation, attack surface reduction, localhost vs. external service exposure.

**Domain 4.0 - Security Operations (28%):** Reconnaissance techniques, vulnerability scanning, network monitoring, threat hunting, incident detection.

---

## 📸 Evidence

**Note:** Screenshots were not captured during initial completion. Documentation based on hands-on completion and room content review.

### Key Findings:
- Basic Nmap scan: SSH (22), HTTP (80)
- Full scan revealed: FTP on 21212 (vsFTPd 3.0.5), custom app on 25251 (TBFC maintd v0.2)
- UDP scan revealed: DNS on 53
- FTP anonymous login → Key fragment 1
- Netcat GET KEY → Key fragment 2
- DNS TXT record `key3.tbfc.local` → Key fragment 3
- `ss -tunlp` revealed MySQL on 127.0.0.1:3306 (invisible to external Nmap)
- Unauthenticated MySQL access → Final flag from `flags` table

---

## 📚 Key Takeaways for Future Reference

### Nmap Quick Reference

**Essential Nmap Commands:**

```bash
# Basic scan (top 1000 TCP ports)
nmap <IP>

# Full TCP scan with version/banner
nmap -p- --script=banner <IP>

# UDP scan
nmap -sU <IP>

# Service version detection
nmap -sV <IP>

# OS detection
nmap -O <IP>

# Aggressive scan (OS + version + scripts + traceroute)
nmap -A <IP>

# Scan specific ports
nmap -p 22,80,443,3306 <IP>

# Scan port range
nmap -p 1-1024 <IP>

# Fast scan (top 100 ports)
nmap -F <IP>

# Output to file
nmap -oN output.txt <IP>
nmap -oX output.xml <IP>
```

**Key Nmap Flags:**

| Flag | Purpose |
|------|---------|
| `-p-` | Scan all 65,535 TCP ports |
| `-sU` | UDP scan |
| `-sV` | Service version detection |
| `-O` | OS detection |
| `-A` | Aggressive (all) |
| `-F` | Fast (top 100 ports) |
| `--script=banner` | Grab service banners |
| `-oN` | Normal output to file |
| `-Pn` | Skip host discovery (treat as up) |
| `-T4` | Faster timing (1=slowest, 5=fastest) |

### Service Enumeration Tools

**FTP (File Transfer Protocol):**
```bash
# Connect to FTP
ftp <IP>          # Default port 21
ftp <IP> 21212    # Custom port

# Anonymous login
Name: anonymous
Password: [blank or email]

# Common FTP commands
ls                # List files
get <filename>    # Download file
get <filename> -  # Display file contents
put <filename>    # Upload file
!                 # Exit FTP shell
bye               # Disconnect
```

**Netcat (Universal Network Tool):**
```bash
# Connect to any service
nc -v <IP> <port>

# Flags
-v    # Verbose output
-n    # No DNS resolution
-z    # Scan mode (no data)
-u    # UDP mode

# Exit: Ctrl+C
```

**DNS (dig):**
```bash
# Basic query
dig <domain>

# Query specific server
dig @<server_IP> <domain>

# Query specific record type
dig @<IP> TXT <domain>     # Text records
dig @<IP> MX <domain>      # Mail records
dig @<IP> A <domain>       # IPv4 records
dig @<IP> AAAA <domain>    # IPv6 records
dig @<IP> ANY <domain>     # All records

# Short output
dig @<IP> TXT <domain> +short

# Zone transfer (if allowed - often a misconfiguration!)
dig @<IP> AXFR <domain>
```

**Socket Statistics (ss):**
```bash
# Show all listening ports
ss -tunlp

# Flags breakdown
-t    # TCP
-u    # UDP
-n    # Numeric (no hostname resolution)
-l    # Listening only
-p    # Process information

# Filter by port
ss -tunlp | grep :3306

# Alternative (older systems)
netstat -tunlp
```

**MySQL (Command Line):**
```bash
# Connect to local MySQL
mysql -u root -p                    # With password prompt
mysql -u root                       # Without password

# Connect to specific database
mysql -D <database_name>

# Execute single query
mysql -D <db> -e "show tables;"
mysql -D <db> -e "select * from <table>;"
mysql -D <db> -e "show databases;"

# Common SQL commands
SHOW DATABASES;
SHOW TABLES;
SELECT * FROM <table>;
DESCRIBE <table>;    # Show table structure
```

### Port and Protocol Reference

**Well-Known Ports (Must Know):**

| Port | Protocol | Service |
|------|----------|---------|
| 21 | TCP | FTP |
| 22 | TCP | SSH |
| 23 | TCP | Telnet (insecure!) |
| 25 | TCP | SMTP (email) |
| 53 | TCP/UDP | DNS |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 (email) |
| 143 | TCP | IMAP (email) |
| 443 | TCP | HTTPS |
| 445 | TCP | SMB (file sharing) |
| 3306 | TCP | MySQL |
| 3389 | TCP | RDP (Remote Desktop) |
| 5432 | TCP | PostgreSQL |
| 6379 | TCP | Redis |
| 8080 | TCP | HTTP alternate |
| 8443 | TCP | HTTPS alternate |

### 0.0.0.0 vs 127.0.0.1 — Critical Concept

```
0.0.0.0 (all interfaces):
  - Accessible from ANYWHERE on network
  - Visible to Nmap external scans
  - Attack surface = EXTERNAL THREAT

127.0.0.1 (localhost only):
  - Accessible ONLY from the host itself
  - INVISIBLE to external Nmap scans
  - Attack surface = INTERNAL THREAT (after initial compromise)
  
::1 (IPv6 localhost):
  - Same as 127.0.0.1 but IPv6
```

**SOC Implication:**
Finding a service on `127.0.0.1` after compromising a host = additional attack surface for lateral movement. Attackers pivot from initial access to internal services.

### Common Network Misconfigurations (Detection Targets)

**Anonymous FTP:**
```
Risk: Anyone can login and download files
Detection: Look for FTP login with username "anonymous"
Prevention: Disable anonymous FTP or restrict to specific paths
```

**Unauthenticated Database:**
```
Risk: Database accessible without password from localhost
Detection: MySQL/PostgreSQL connections without credentials in logs
Prevention: Require authentication even from localhost
```

**Services on Non-Standard Ports:**
```
Risk: Security through obscurity (not real security)
Detection: Full port scan (-p-) reveals hidden services
Prevention: Firewall rules, not port obscurity
```

**Overly Exposed Services:**
```
Risk: Service bound to 0.0.0.0 instead of 127.0.0.1
Detection: ss -tunlp or netstat on host
Prevention: Bind to specific interface only
```

### Detecting Network Scans (SOC Perspective)

**Nmap Scan Signatures in Logs/IDS:**

```
Basic scan pattern:
- Sequential connection attempts to multiple ports
- Short timeframe (seconds)
- From single source IP
- Most connections = RST (port closed)

Full scan (-p-):
- 65,535 connection attempts
- Often triggers IDS "port scan" alert

UDP scan (-sU):
- ICMP "port unreachable" responses in logs
- Slower pattern than TCP scans

Banner grabbing (--script=banner):
- Full TCP connection to each open port
- Immediate disconnect after banner received
```

**Detection Rules to Create:**
```
Alert: Single IP connecting to >100 ports in <60 seconds
Alert: Sequential port access pattern from external IP
Alert: Connection attempts to known non-existent ports
Alert: Nmap user-agent in HTTP logs
```

### Recon → Exploitation Chain (Pattern Recognition)

**Standard Attacker Methodology:**
```
Phase 1: Nmap basic scan → Find obvious services
Phase 2: Nmap full scan  → Find hidden services on non-standard ports
Phase 3: UDP scan        → Find UDP services (DNS, SNMP, TFTP)
Phase 4: Service enum    → Test each service for misconfigs
Phase 5: Exploitation    → Use misconfig to gain access
Phase 6: On-host enum    → ss -tunlp to find internal services
Phase 7: Pivot           → Access internal services (databases, APIs)
```

**What SOC Watches For:**
- Each phase leaves distinct log signatures
- Phase 1-3 = IDS/firewall logs
- Phase 4-5 = Application/service logs
- Phase 6-7 = Host-based monitoring (EDR, auditd)

---
