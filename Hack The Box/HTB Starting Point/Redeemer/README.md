# Redis
[Redis](https://github.com/uriel0byte/IT-Learning-Journey-urielbyte/blob/a3262fcf819cb81b6ac2389d7702883ebf3486a8/Notes/Redis/redis_ctf_writeup.md)

# Steps

0.  First connect to HTB using OpenVPN by download the VPN Config provided. After that, spawn the target machine.
  
1.  Task 1
    Which TCP port is open on the machine? 
    
    Answer: 6379 | by using Nmap to run a port scan, scanning all ports with '-p-'. This can be really slow, so consider adding '-T5' to speed it up.

2.  Task 2
    Which service is running on the port that is open on the machine? 
    
    Answer: Redis

3.  Task 3
    What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database 

    Answer: In-memory Database | Use Google

4.  Task 4
    Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments. 
    Which flag is used with the Redis command-line utility to specify the hostname?
    
    Answer: redis-cli | Search "command-line utility for Redis"

6.  Task 5
    Which flag is used with the Redis command-line utility to specify the hostname? 
    
    Answer: -h | redis-cli --help

7.  Task 6
    Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server? 
    
    Answer: info | Search Google
    
8.  Task 7
    What is the version of the Redis server being used on the target machine?
    
    Answer: 5.0.7 | connect to the target redis by " redis-cli redis-cli -h <ip> -p 6379 " after connected do " info "

9.  Task 8
    Which command is used to select the desired database in Redis? 
    
    Answer: select | Use Google

10.  Task 9
    How many keys are present inside the database with index 0? 
    
     Answer: 4 | Refer to the output of the "info" command, under the "Keyspace" section.

11.  Task 10
     Which command is used to obtain all the keys in a database? 
    
     Answer: KEYS * | Use Google


12.  Task 11
     Submit root flag 
    
     Answer: 03e1d2b376c37ab3f5319922053953eb | Use GET command " get <key> "
