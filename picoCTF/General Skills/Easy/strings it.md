# Author: Sanjay C/Danny Tunitis

# Description
Can you find the flag in file without running it?

# Hints
1. strings

# Steps
1. Download the provided file.
2. Inspect the file using file command, noticing that it is LF 64-bit LSB pie executable, which I have no idea what that is but it's executable for sure.
3. Used strings command to display printable strings "strings <file> | grep -i "picoctf"

Answer: picoCTF{5tRIng5_1T_FB7D7Bb6}
