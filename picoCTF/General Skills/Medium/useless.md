# Author: Loic Shema

# Description
There's an interesting script in the user's home directory The work computer is running SSH. We've been given a script which performs some basic calculations, explore the script and find a flag.

# Hints
1. None

# Steps
1. Connect the remote server via ssh using " ssh -p 65**7 picoplayer@sa****.picoctf.net" .
2. Run the script, and it said that go check the source code. I do so but found nothing useful except that "Read the manual"
3. So I did " man useless " which useless is the script pass as a argument.
4. Found the flag, and I did not know that man could use with a file or script.
5. I guess I know something new today...

Answer: picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_5657}
