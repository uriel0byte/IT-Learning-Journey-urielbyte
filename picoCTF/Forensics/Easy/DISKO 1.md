# Author: Darkraicg492

# Description
Can you find the flag in this disk image?
Download the disk image [here](https://artifacts.picoctf.net/c/538/disko-1.dd.gz).

# Hints
1.  Maybe Strings could help? If only there was a way to do that?


# What is Disk Image


# Steps
1. Download the disk image with wget.
2. Got the "disko-1.dd.gz" gzip file. Unzip it with "gunzip disko-1.dd.gz" got disko-1.dd then use "file disko-1.dd" and "wc disko-1.dd" commands to see what kind of file it is and how big the file is.
3. Found that it's some kind of disk image "disko-1.dd: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "mkfs.fat", Media descriptor 0xf8, sectors/track 32, heads 8, sectors 102400 (volumes > 32 MB), FAT (32 bit), sectors/FAT 788, serial number 0x241a4420, unlabeled" I don't really know what it's called exactly. and also found that it's quite a big file with 52428800 bytes in total.
4. First I used "less" command to see if there is any readable text in this binary file or not.
5. Found that there are quite some so I used " cat disko-1.dd | strings | grep "pico" "
6. And Voila! Found it.

Answer: picoCTF{1t5_ju5t_4_5tr1n9_e3408eef}
