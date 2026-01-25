# Author: LT 'syreal' Jones

# Description
Unzip this archive and find the flag.
[Download zip file](https://artifacts.picoctf.net/c/503/big-zip-files.zip)

# Hints
1.  Can grep be instructed to look at every file in a directory and its subdirectories?

# Steps
1. Download the provided zip file.
2. Unzip the file.
3. Now we have to use grep the way that it can search in directory and subdirectories. So, I used "grep -ri "pico"" if we are inside the unzip directory or "grep -ri "pico" big-zip-files/" to specify the destination.

Answer:  picoCTF{gr3p_15_m4g1c_ef8790dc}
