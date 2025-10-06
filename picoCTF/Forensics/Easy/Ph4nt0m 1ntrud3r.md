# Author: Prince Niyonshuti N.

# Description
A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag. To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder! Find the PCAP file here Network Traffic PCAP file and try to get the flag. 

# Hints
1.  Filter your packets to narrow down your search.
2.  Attacks were done in timely manner.
3.  Time is essential

# What is PCAP file
A data file that records network traffic.

# This is my first time using Wireshark (It was hell)

# Steps
1. Download the provided PCAP file.
2. Open the Wireshark, open the PCAP file.
3. There were 22 tcp packets present, which is not a lot i thought. So I sift through all the packets and saw some base64-encoding strings located in the binaries of some of the packets.
4. So I click at the Time Bar above to rearrange the time of the packets. So the 7 packets that have length of 12 bytes that are adjacant to each other looks promising. Then I inspect each of the 7 packets and copy the base64 strings and convert them in cyberchef one by one but packet 20 is only 4 bytes but have the == which indicate that it's base64 so i combine these strings to packet 4 which is adjacant to each other. We got the flag!

Answer: picoCTF{1t_w4snt_th4t_34sy_tbh_4r_966d0bfb}
