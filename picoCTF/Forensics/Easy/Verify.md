# Author: Jeffery John

# Description
People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate.

Additional details will be available after launching your challenge instance.

# Hints
1.  Checksums let you tell if a file is complete and from the original distributor. If the hash doesn't match, it's a different file.
2.  You can create a SHA checksum of a file with sha256sum <file> or all files in a directory with sha256sum <directory>/*.
3.  Remember you can pipe the output of one command to another with |. Try practicing with the 'First Grep' challenge if you're stuck!

# Steps
1. Connect to the remote server via ssh with the provided password.
2. After launching the instance just follow the instruction. It's pretty easy.
3. The point of this challenge is where you combine the right sequence of commands. Have a look at mine.
   
```
ctf-player@pico-chall$ ls
checksum.txt  decrypt.sh  files

ctf-player@pico-chall$ cat checksum.txt 
5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda

ctf-player@pico-chall$ sha256sum ./files/* | grep -f checksum.txt
5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda  ./files/8eee7195

ctf-player@pico-chall$ sha256sum ./files/* | grep $(cat checksum.txt )
5848768e56185707f76c1d74f34f4e03fb0573ecc1ca7b11238007226654bcda  ./files/8eee7195

ctf-player@pico-chall$ ./decrypt.sh files/8eee7195 
picoCTF{trust_but_verify_8eee7195}
```
4. In the example, I used two type of commands to show that there is more than one way to do this.
5. Or you can just do " sha256sum ./files/* " and manaully find the right one that match the content of the checksum.txt file. Trying to practice grep or combinding commands is better.

Answer: picoCTF{trust_but_verify_8eee7195}
