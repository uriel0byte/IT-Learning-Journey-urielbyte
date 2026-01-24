# Author: Sanjay C/Daniel Tunitis

# Description
Decrypt this message. Message: [message](https://challenge-files.picoctf.net/c_fickle_tempest/588d56d087048c798295f56dc7c2bb760063a75827c2033ecb13f8a88a9c502a/data.enc)

# Hints
1.  Caesar cipher tutorial

# What is Caesar Cipher?
The Caesar cipher (or Caesar code) is a monoalphabetic substitution cipher, where each letter is replaced by another letter located a little further in the alphabet (therefore shifted but always the same for given cipher message).

The shift distance is chosen by a number called the offset, which can be right (A to B) or left (B to A).

For every shift to the right (of +N), there is an equivalent shift to the left (of 26-N) because the alphabet rotates on itself, the Caesar code is therefore sometimes called a rotation cipher.

# Steps
1. Download the encrypted flag using wget and read the file with cat
2. Open an online tool like [Dcode](https://www.dcode.fr/caesar-cipher)
3. Paste the encrypted text also delete the (picoCTF) because it's already a plaintext. Decrypt it and the answer is the first one.

Answer: picoCTF{crossingtherubiconbqllkxqb}
