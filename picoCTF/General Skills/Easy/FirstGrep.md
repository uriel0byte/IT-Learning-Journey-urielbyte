# Author: Alex Fulton/Danny Tunitis

# Description
Can you find the flag in the file? This would be really tedious to look through manually, something tells me there is a better way. The flag is in this file.

# Hints
1. grep tutorial

# Steps
1. Download the provided file.
2. Used wc to evaluate the file and found that it's a lot of bytes.
3. Used "grep -i "picoctf" file" and found the flag but since this file only one line that contains a lot of characters, it's pretty hard to see it but still easier to manually detect it (the word is highlighted).

Answer: picoCTF{grep_is_good_to_find_things_e3C4b360}
