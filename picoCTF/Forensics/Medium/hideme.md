# Author:  Geoffrey Njogu

# Description
Every file gets a flag. The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye here.

# Hints
1. None

# Steps
1. Download the provided file.
2. Used "file" command to verify the type of the image. It's PNG.
3. Used "binwalk" command to see if there is any embbeded file in this image or not. Found that there is a ZIP file in it 
```
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2997, uncompressed size: 3152, name: secret/flag.png`. Found another flag.png in that zip file.
```
4. Used "binwalk -e" command to automatically extract known file types. Got
```
urielbyte-picoctf@webshell:~/hideme$ ls -l _flag.png.extracted/
total 48
-rw-rw-r-- 1 urielbyte-picoctf urielbyte-picoctf     0 Mar 11 18:30 29
-rw-rw-r-- 1 urielbyte-picoctf urielbyte-picoctf 43017 Mar 11 18:30 29.zlib
-rw-rw-r-- 1 urielbyte-picoctf urielbyte-picoctf  3319 Mar 11 18:30 9B3B.zip
drwxr-xr-x 2 urielbyte-picoctf urielbyte-picoctf    30 Mar 16  2023 secret
```
5. cd into that secret directory and open the image.

Answer: 
