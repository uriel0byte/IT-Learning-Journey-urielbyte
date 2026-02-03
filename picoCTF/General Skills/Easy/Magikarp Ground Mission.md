# Author: syreal

# Description
Do you know how to move between directories and read files in the shell? Start the container, ssh to it, and then ls once connected to begin.

Login via ssh as c**-player with the password, ****** on the host w**y-courier.picoctf.net and port 516*8. (These numbers are not the same for each player)

# Hints
1. Finding a cheatsheet for bash would be really helpful!

# Steps
1. Used "ssh ctf-player@wily-courier.picoctf.net -p 51678" to connect to the remote host.
2. All the rest of the steps are easier to show than just explain...

```bash
ctf-player@pico-chall$ pwd
/home/ctf-player/drop-in

ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt

ctf-player@pico-chall$ cat 1of3.flag.txt 
picoCTF{xxsh_

ctf-player@pico-chall$ cat instructions-to-2of3.txt 
Next, go to the root of all things, more succinctly `/`

ctf-player@pico-chall$ cd /

ctf-player@pico-chall$ ls
2of3.flag.txt  bin  boot  challenge  dev  etc  home  instructions-to-3of3.txt  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

ctf-player@pico-chall$ cat 2of3.flag.txt 
0ut_0f_//4t3r_

ctf-player@pico-chall$ cat instructions-to-3of3.txt 
Lastly, ctf-player, go home... more succinctly `~`

ctf-player@pico-chall$ cd /home/ctf-player/

ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in

ctf-player@pico-chall$ cat 3of3.flag.txt 
0b24fc4f}

```

3. Finally, combine all the fragments and return the flag.

Answer: picoCTF{xxsh_0ut_0f_//4t3r_0b24fc4f}
