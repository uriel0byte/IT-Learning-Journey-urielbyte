# Author: Sanjay C/Danny

# Description
This is a really weird text file. Can you find the flag? Get the flag from TXT.

# Hints
1.  How do operating systems know what kind of file it is? (It's not just the ending!)
2.  Make sure to submit the flag as picoCTF{XXXXX}

# Steps
1. Download the provided file.
2. At first, I used "file" "wc" "head" command to determine what type of file is this, how big is this, take a look at the content.

```
urielbyte-picoctf@webshell:~/Extension$ file flag.txt 
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
urielbyte-picoctf@webshell:~/Extension$ wc flag.txt 
  10   60 9984 flag.txt
urielbyte-picoctf@webshell:~/Extension$ head -10 flag.txt 
PNG

IHDR^sRGBgAMA
             a  pHYs%%IR$&IDATx^kB;.0L&_N=%LZJut$y'H&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>&l2>˿'~n疓?^xQ2>osD9
```

3. This looks like an PNG file and it looks like it's in a legit format. but let's check the header just in case.
4. Found that the header looks fine, now let's just try change the file extension from .txt to .png
5. Now I can see that flag.


Answer: picoCTF{now_you_know_about_extensions}
