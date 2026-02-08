# Author: LT 'syreal' Jones

# Description
Can you crack the password to get the flag? Download the password checker here and you'll need the encrypted flag and the hash in the same directory too. There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.

# Hints
1. To view the level3.hash.bin file in the webshell, do: $ bvi level3.hash.bin
2. To exit bvi type :q and press enter.
3. The str_xor function does not need to be reverse engineered for this challenge.

# What is Hashing?

Hashing (like MD5 used in this challenge) is a one-way function that scrambles data into a fixed-size string of characters. Unlike encryption, you cannot "decrypt" a hash back to its original text. To verify a password, the system takes the user's input, hashes it, and checks if that new hash matches the stored hash.

# Steps
1. Downloaded the provided files.
2. Inspect the python script. I opened level3.py and saw a list of 7 possible passwords right at the bottom:

```Python
pos_pw_list = ["f09e", "4dcf", "87ab", "dba8", "752e", "3961", "f159"]
```

3. The level_3_pw_check() function takes user input, hashes it using the hash_pw() function, and compares it to the correct_pw_hash. If they match, it decrypts the flag using str_xor.
4. At first, I ran the script 7 times, copying and pasting each password from that list until one worked. It worked, but it was tedious.
5. While I could manually run the script 7 times and test each password, that isn't efficient. Instead, we can automate this process by modifying the python code to loop through the pos_pw_list for us.
6. I modified the level_3_pw_check() function in the script. I commented out the input() prompt and added a for loop to iterate through the 7 possibilities:

```Python
def level_3_pw_check():
    pos_pw_list = ["f09e", "4dcf", "87ab", "dba8", "752e", "3961", "f159"]

    # user_pw = input("Please enter correct password for flag: ")

    for i in range(len(pos_pw_list)):
        user_pw = pos_pw_list[i]
        user_pw_hash = hash_pw(user_pw)

        # If the hash matches, print the flag and stop
        if( user_pw_hash == correct_pw_hash ):
            print(f"Correct Password found: {user_pw}")
            decryption = str_xor(flag_enc.decode(), user_pw)
            print(decryption)
            return

    print("That password is incorrect")
level_3_pw_check()
```

7. After modifying the code, I saved it and ran python3 level3.py again. The script looped through the list, found the matching hash, and automatically printed the decrypted flag!

Answer: picoCTF{m45h_fl1ng1ng_6f98a49f}
