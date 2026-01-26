# Author: LT 'syreal' Jones

# Description
Can you crack the password to get the flag? Download the password checker here and you'll need the encrypted flag in the same directory too.

# Hints
1.  To view the file in the webshell, do: $ nano level1.py
2.  To exit nano, press Ctrl and x and follow the on-screen prompts.
3.  The str_xor function does not need to be reverse engineered for this challenge.

# Steps
1. Download the password checker and the encrypted flag. Put the script and the flag in the same directory.
2. Using Vim or Nano to view the file.
3. Notice the " if( user_pw == "1e1a") " so this should be the password for the function to decrypt the flag.
4. Run the script using "pyhon3 level1.py" and the prompt popped up asking for the password. Type in the password and got the decrypted flag.

Answer:  picoCTF{545h_r1ng1ng_fa343060}
