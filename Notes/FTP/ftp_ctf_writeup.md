
# FTP (File Transfer Protocol) - CTF Walkthrough

## What is FTP?

FTP is a standard network protocol used for the transfer of computer files between a client and server on a computer network. Built on a client-server model architecture using separate control and data connections, it is one of the oldest protocols still in use today.

## Key Concepts for CTF Challenges

### The "Cleartext" Problem
Unlike modern protocols, standard FTP sends data—including usernames and passwords—in cleartext (unencrypted). This makes it highly vulnerable to packet sniffing if you are on the same network.
- **Secure Alternative**: **SFTP** (SSH File Transfer Protocol), which runs over the SSH protocol (usually port 22) to provide encryption.

### Anonymous Access
Many FTP servers are misconfigured to allow "Anonymous" login. This is a feature, not a bug, intended for public file distribution, but in CTFs (and careless corporate environments), it often leaks sensitive data.

## Connecting to FTP

FTP typically runs on **Port 21**. You can interact with it using the standard client installed on most Linux systems:

```bash
ftp <host>
# or specifying port if non-standard
ftp <host> <port>
```

## Enumeration: Before connecting, it is common to scan the port to identify the specific server software (e.g., vsftpd 3.0.3) and the OS (e.g., Unix), as specific versions may have known vulnerabilities.
Bash

```bash
nmap -sV -p 21 <target>
```

## Common FTP Commands for CTF

Once connected to the FTP shell, you can use these commands to navigate and retrieve flags:

```bash
USER anonymous                 # Log in as anonymous (often requires blank password)
ls                             # List files in current directory (Linux standard)
dir                            # Alternative command to list files (Windows style)
cd <directory>                 # Change directory
get <filename>                 # Download a file to your local machine
put <filename>                 # Upload a file (if write permissions exist)
exit                           # Disconnect from server
?                              # Show help menu (or ftp -?)
```

## Connectivity Check: Before attempting to connect, you can verify the target is reachable using ICMP:

```bash
ping <target_ip>
```

## CTF Challenge Patterns

Anonymous Login: The most common check. Try logging in with the username anonymous and a blank password.

Hidden Files: Use ls -a (if supported) to look for hidden files starting with a dot (e.g., .env, .ssh).

Version Exploits: Identify the server version (e.g., vsftpd). Some older versions have famous backdoors (like vsftpd 2.3.4).
Security Considerations

- Disable Anonymous Access: Unless explicitly required for public data.

- Use Encryption: Use SFTP or FTPS (FTP over SSL) to protect credentials.

- Strong Authentication: Enforce strong passwords and consider IP restrictions.
