# Author: Geoffrey Njogu

# Description
Can you read files in the root file? The system admin has provisioned an account for you on the main server: ******* Can you login and read the root file?

# Hints
1. What permissions do you have?

# Steps
1. Connect to the remote server via ssh.
2. I tried a lot of things here...
3. First I go back to the root directory, Tried cd and ls to the root directory but the permission is not enough. Next, I tried using sudo cd, sudo ls to the root directory but it said that for my sudo permission cd and ls are not found. That could mean that I have sudo permission but for some applications.
4. I searched how to check what sudo commands are available for particular user and found that it's sudo -l
5. Found that I can use Vi or Vim with sudo.
6. So I did sudo vim root/ and found the text that contain the flag.
7. I am sure that there are other ways to do this but I did this on my own so I am going to stick with this but I will check other ways too. Thank you!

Answer: picoCTF{uS1ng_v1m_3dit0r_1cee9dcb}
