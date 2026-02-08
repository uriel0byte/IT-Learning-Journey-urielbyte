# Author: LT 'syreal' Jones

# Description
Can you crack the password to get the flag? Download the password checker here and you'll need the encrypted flag and the hash in the same directory too. There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.

# Hints
1. To view the level3.hash.bin file in the webshell, do: $ bvi level3.hash.bin
2. To exit bvi type :q and press enter.
3. The str_xor function does not need to be reverse engineered for this challenge.

# What is Hashing (MD5)?

In this challenge, the script imports hashlib and uses MD5. Hashing is different from encryption because it is one-way. You can turn a password like "apple" into a scrambled hash, but you cannot turn the hash back into "apple." To check if a password is correct, the computer hashes your guess and compares it to the stored hash. If they match, the password is correct.

# Steps
1. Downloaded the provided files.
2. Inspect the python script. I opened level3.py and saw a list of 7 possible passwords right at the bottom:
Python

pos_pw_list = ["f09e", "4dcf", "87ab", "dba8", "752e", "3961", "f159"]

Answer: 
