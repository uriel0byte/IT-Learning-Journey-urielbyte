# Author: Nana Ama Atombo-Sackey

# Description
A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?

# Hints
1.  Understanding hashes is very crucial. Read more [here](https://primer.picoctf.org/#_hashing).
2.  Can you identify the hash algorithm? Look carefully at the length and structure of each hash identified.
3.  Tried using any hash cracking tools?

# What is Hash?
A hash (or hash value/digest) is the output of a mathematical hash function—an algorithm that takes an input of any size (like a password, file, or message) and converts it into a fixed-length string of characters.

More info : https://primer.picoctf.org/#_hashing

# Steps
1. Click Start Instance. Open your terminal and paste your netcat server that is provided by the pico instance.
2. If you're familiar with identifying hash algorithms feel free to do so, if not here https://hashes.com/en/tools/hash_identifier.
3. After Identifyig the Hash algorithm, let's crack it by using Online Tool (https://10015.io/tools/md5-encrypt-decrypt) or you can use HashCat if you're familiar with that tool or want to learn abou that tool.
4. Just repeat the process untill you got the flag.

Answer: picoCTF{UseStr0nG_h@shEs_&PaSswDs!_4de57566}

