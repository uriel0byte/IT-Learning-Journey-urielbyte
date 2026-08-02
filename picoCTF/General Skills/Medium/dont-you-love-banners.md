# Author: Loic Shema / syreal

# Description
Can you abuse the banner?

# Hints
1. Do you know about symlinks?
2. Maybe some small password cracking or guessing

# Steps
1. Click start an instance, there are 2 ips given. One is for the password to connect to another server
2. Used nc to connect to the first server, grab the password and connect to the 2nd server using that password and answers general questions to get in.
3. Used ls found 2 files: banner and text. Used cat to get more info on both files. banner files is just a first banner/text showing when first connected to the server. The text file just said that "keep digging"
4. Following the instruction, navigate to `/root` directory found 2 files: script.py and flag.txt. The flag.txt we don't have enough perms to read it but not with script.py

```Python
player@challenge:~$ cat /root/script.py
cat /root/script.py

import os
import pty

incorrect_ans_reply = "Lol, good try, try again and good luck\n"

if __name__ == "__main__":
    try:
      with open("/home/player/banner", "r") as f:
        print(f.read())
    except:
      print("*********************************************")
      print("***************DEFAULT BANNER****************")
      print("*Please supply banner in /home/player/banner*")
      print("*********************************************")

try:
    request = input("what is the password? \n").upper()
    while request:
        if request == 'MY_PASSW@RD_@1234':
            text = input("What is the top cyber security conference in the world?\n").upper()
            if text == 'DEFCON' or text == 'DEF CON':
                output = input(
                    "the first hacker ever was known for phreaking(making free phone calls), who was it?\n").upper()
                if output == 'JOHN DRAPER' or output == 'JOHN THOMAS DRAPER' or output == 'JOHN' or output== 'DRAPER':
                    scmd = 'su - player'
                    pty.spawn(scmd.split(' '))

                else:
                    print(incorrect_ans_reply)
            else:
                print(incorrect_ans_reply)
        else:
            print(incorrect_ans_reply)
            break

except:
    KeyboardInterrupt
```

5. We can see a function `with open("/home/player/banner", "r") as f:` I don't know any python but I assume this function pulls a banner from `/home/player/banner`.
6. Plus when look at the hints(symlinks), we know we can replace the banner with flag.txt without changing the script itself since we don't have enough perms.
7. Used `ln -s /root/flag.txt banner` because symlink is like a shortcut to another file but before that we have to delete the original banner file.
8. So now we have banner file that has a content of flag.txt. Since we don't have enough perms on the flag.txt, we still don't have enough perms on the new banner file.
9. So we let the system do that for us. Exit out and reconnect to the server and the flag is there.

Answer: picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_b3ee718e}
