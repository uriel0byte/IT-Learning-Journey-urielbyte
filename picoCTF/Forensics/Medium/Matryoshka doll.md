# Author: Susie/Pandu

# Description
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: dolls.jpg

# Hints
1. Wait, you can hide files inside files? But how do you find them?
2. Make sure to submit the flag as picoCTF{XXXXX}

# Steps
1. Download the provided file.
2. Used "binwalk" to see if there is any embedded file.
3. Used "binwalk -e <file>" to extract the embedded picture in it.
4. cd into the extracted directory and found another wooden dolls used "binwalk" and "exiftool" if there is any useful information or not.
5. Repeat the process untill it reach the point where there is no more image.

Answer: picoCTF{LL9lb1dR4QbGe4l4iWCvGq9pdtwt7392}
