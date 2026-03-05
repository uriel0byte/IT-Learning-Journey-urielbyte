# Author: Danny

# Description
We found this file. Recover the flag.

# Hints
1. Try fixing the file header

# Steps
1. Download the provided file.
2. First I open Hexeditor online or can also use xxd utility too.
3. First I check the file trailer to have a hint on what kind of this file actually is. Found that it's 49 45 4E 44 AE 42 60 82 which indicate that it might be PNG file.
4. So I change the file header to a standard PNG header which is 89 50 4E 47 0D 0A 1A 0A
5. I also check the next 8 byte which is IHDR Chunk if it's in the correct form which is 00 00 00 0D 49 48 44 52.
6. Next, I check for the next few byte if there is any IDAT but found something unsual but similiar to IDAT so I change it to 49 44 41 54
7. Save the file and change the extension to .png

Answer: picoCTF{c0rrupt10n_1847995}
