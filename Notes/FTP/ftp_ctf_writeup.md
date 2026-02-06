
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

