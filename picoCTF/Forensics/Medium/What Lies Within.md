# Author: Julio/Danny

# Description
There's something in the building. Can you retrieve the flag?

# Hints
1. There is data encoded somewhere... there might be an online decoder.

# Steps
1. Download the provided file.
2. When the context is about hidden, encoded data in a picture, think of Steganography here.
3. So I used steghide info <file> , exiftool <file> , binwalk <file> to help me find the flag but all of them came back with nothing. So I realize that the picture is in .png format which used the different tool than steghide.
4. Next I used, zsteg tool to extract the hidden data in the png image. (Online tool works too)
5. I've done this in exact method in the picoctf past room, I guess sometimes we forgot things.

```
urielbyte-picoctf@webshell:~/WhatLiesWithin$ zsteg buildings.png 
b1,r,lsb,xy         .. text: "^5>R5YZrG"
b1,rgb,lsb,xy       .. text: "picoCTF{h1d1ng_1n_th3_b1t5}"
b1,abgr,msb,xy      .. file: PGP Secret Sub-key -
b2,b,lsb,xy         .. text: "XuH}p#8Iy="
b3,abgr,msb,xy      .. text: "t@Wp-_tH_v\r"
b4,r,lsb,xy         .. text: "fdD\"\"\"\" "
b4,r,msb,xy         .. text: "%Q#gpSv0c05"
b4,g,lsb,xy         .. text: "fDfffDD\"\""
b4,g,msb,xy         .. text: "f\"fff\"\"DD"
b4,b,lsb,xy         .. text: "\"$BDDDDf"
b4,b,msb,xy         .. text: "wwBDDDfUU53w"
b4,rgb,msb,xy       .. text: "dUcv%F#A`"
b4,bgr,msb,xy       .. text: " V\"c7Ga4"
b4,abgr,msb,xy      .. text: "gOC_$_@o"
```


Answer: picoCTF{h1d1ng_1n_th3_b1t5}
