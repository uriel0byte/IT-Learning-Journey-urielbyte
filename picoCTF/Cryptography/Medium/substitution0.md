# Author: Will Hong

# Description
A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher?
Download the message here.

# Hints
1.  Try a frequency attack. An online tool might help.

# What is Mono-alphabetic Substitution
An alphabetic substitution is a substitution cipher where the letters of the alphabet are replaced by others according to a 1-1 correspondence (a plain letter always corresponds to the same cipher letter).

The substitution is said to be monoalphabetic because it uses only one alphabet, this alphabet is said to be disordered.

# Steps
1. Download the ciphertext.
2. Examine the provided text with Dcode Identifier and the result came back with it being a Vigenere Cipher but I couldn't crack the code. So, trying to find another cipher method.
3. Came across a Mono-alphabetic Substitution with the Knowing the substitution alphabet Decryption method so I thought of the key that was expressed in the description.
4. Turn out I was right. Got the plaintext.

Answer: picoCTF{5UB5717U710N_3V0LU710N_357BF9FF}
