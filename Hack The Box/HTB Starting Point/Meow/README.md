# Steps
0.  First connect to HTB using OpenVPN by download the VPN Config provided. After that, spawn the target machine.
  
1.  Task 1
    What does the acronym VM stand for?
    
    Answer: Virtual Machine

2.  Task 2
    What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It's also known as a console or shell.
    
    Answer: Terminal

3.  Task 3
    What service do we use to form our VPN connection into HTB labs?
    
    Answer: OpenVPN

4.  Task 4
    What tool do we use to test our connection to the target with an ICMP echo request?
    
    Answer: ping

5.  Task 5
    What is the name of the most common tool for finding open ports on a target?
    
    Answer: Nmap

6.  Task 6
    What service do we identify on port 23/tcp during our scans?
    
    Answer: Telnet
    
7.  Task 7
    What username is able to log into the target over telnet with a blank password?
    
    Answer: root

8.  Submit root flag
    
     Answer: b40abdfe23665f766f9c61ecba8a4c19 | First, used nmap to scan the target. Found the telnet service on port 23. Connected to the server using telnet <ip>. Once logged in, the prompt will show up asking for username. Insert root as a username. Now, used ls to list all the files and then used cat to reveal the flag.txt.

Badge: https://labs.hackthebox.com/achievement/machine/2566537/394
