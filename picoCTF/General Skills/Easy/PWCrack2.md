# Author: LT 'syreal' Jones

# Description
Can you crack the password to get the flag? Download the password checker here and you'll need the encrypted flag in the same directory too.

# Hints
1.  Does that encoding look familiar?
2.  The str_xor function does not need to be reverse engineered for this challenge.

# Steps
1. Download the password checker and the encrypted flag. Put the script and the flag in the same directory.
2. Using Vim or Nano to view the file.
3. Notice the " if( user_pw == chr(0x34) + chr(0x65) + chr(0x63) + chr(0x39) ): " so this should be the password for the function to decrypt the flag.
4. But The code provided the password as a series of hex values: 0x34, 0x65, 0x63, 0x39. Using Python's chr() function (or an online Hex decoder), these values translate to the ASCII characters '4', 'e', 'c', and '9', giving us the password 4ec9.
5. Run the script using "pyhon3 level2.py" and the prompt popped up asking for the password. Type in the password and got the decrypted flag.

Answer:  picoCTF{545h_r1ng1ng_fa343060}
