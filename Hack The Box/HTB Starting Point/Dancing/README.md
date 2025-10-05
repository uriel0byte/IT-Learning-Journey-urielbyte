# Steps
0.  First connect to HTB using OpenVPN by download the VPN Config provided. After that, spawn the target machine.
  
1.  Task 1
    What does the 3-letter acronym SMB stand for? 
    Answer: Server Message Block

2.  Task 2
    What port does SMB use to operate at?  
    Answer: 445

3.  Task 3
    What is the service name for port 445 that came up in our Nmap scan?   
    Answer: microsoft-ds by doing nmap -sV 10.129.124.51

4.  Task 4
    What is the 'flag' or 'switch' that we can use with the smbclient utility to 'list' the available shares on Dancing?    
    Answer: -L by doing smbclient --help

5.  Task 5
    How many shares are there on Dancing?    
    Answer: 4 by doing smbclient -L 10.129.124.51

6.  Task 6
    What is the name of the share we are able to access in the end with a blank password?     
    Answer: Workshares by doing smbclient \\\\10.129.124.51\\{every sharename that popup} the result is the Workshares is the only one that we have access to. We can see our           terminal prompt changed to smb: \> , letting us know that our shell is now interacting with the service.

7.  Task 7
    What is the command we can use within the SMB shell to download the files we find?    
    Answer: get by simply type help and all the list of possible command shows up.

8.  Task 8
    Submit root flag     
    Answer: 5f61c10dffbc77a704d76016a22f1664 by doing ls to list all the files. We see two directories shows up so I just cd to each directories and ls to see all the files inside     each directories and we found flag.txt in James.P directory then I do get flag.txt. Then I disconnect from the smb server and cat that flag.txt BRAVO!
