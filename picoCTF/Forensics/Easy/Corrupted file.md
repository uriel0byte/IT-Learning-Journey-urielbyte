# Author: Yahaya Meddy

# Description
This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life?
Download the file [here](https://challenge-files.picoctf.net/c_amiable_citadel/bdd976098377529fe779dbd31b424f69e51327b5ba68fd247dfcc074f0684141/file).

# Hints
1.  Try checking the file’s header.
2.  JPEG
3.  Tools like xxd or hexdump can help you inspect and edit file bytes.

# Steps
1. Download the provided file.
2. I just followed the hints. If they didn't provide the hints, I wouldn't know that I have to edit file byte to a JPEG file...
3. I just used an online hex editor, import the file and edit the filefirst few bytes to (FF D8) which is JPEG file's header.
4. Download the edited file and change the file extension to JPG. Open the file and the flag is there, but I just used the [Image to Text Converter](https://www.imagetotext.info/) instead of manually typing it.

Answer: picoCTF{r3st0r1ng_th3_by73s_249e4e3c}
