# Author: LT 'syreal' Jones

# Description
Unzip this archive and find the file named 'uber-secret.txt'

# Hints
1.  None

# Steps
1. Download the provided zip file.
2. Unzip the file.
3. In this archive, there are files and directories. You can manaully go in each directories to find the file but I will go more further.
4. I used "find . -type f -name "uber*" -exec cat {} +" or you can do "find . -type f -name "uber-secret.txt" -exec cat {} +" because we are already know what is the name of the file we're looking for.
5. Or you can used grep: "grep -ri "pico"" or "grep -ri "picoctf"" because we're already know the flag format but it's not the point of this room but an alternative.

Answer:  picoCTF{f1nd_15_f457_ab443fd1}
