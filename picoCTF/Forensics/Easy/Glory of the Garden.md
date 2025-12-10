# Author: jedavis/Danny

# Description
This file contains more than it seems. Get the flag from [garden.jpg](https://challenge-files.picoctf.net/c_fickle_tempest/ae74cbed5077635927f22095db7234ef717013f25d893a6993e4418696e586f0/garden.jpg).

# Hints
1.  What is a hex editor?

# What is Hexdump
A hexdump is a way to view the raw "atoms" of a computer file. While a regular image viewer interprets the data to show you a picture of a garden, a hexdump shows you the raw binary values (in hexadecimal) that actually make up that picture.

In a CTF writeup, you use a hexdump to analyze the file's structure "under the hood". It allows you to see data that your operating system normally ignores, such as hidden comments, corrupt headers, or files hidden inside other files.

# How to Read the "Gist" of xxd Output
When you ran xxd garden.jpg, the output is divided into three specific columns. Understanding these three parts is the key to "getting the gist":

    The Offset (Left):

        Example: 00000010:

        What it is: This is the "address" or line number. It tells you exactly how many bytes into the file you are.

    The Hex Data (Middle):

        Example: ff d8 ff e0 00 10 4a 46

        What it is: This is the actual file content in hexadecimal code. For a JPG, you specifically check the start (Magic Bytes) to see FF D8 (Start of Image) and the end to see FF D9 (End of Image).

    The ASCII Representation (Right):

        Example: ....JFIF....

        What it is: This translates the hex code into human-readable text. This is where you look for the flag. However, non-printable characters (like "formatting" bytes) appear as dots (.).

# Steps
1. Download the provided jpg file.
2. Used "xxd garden.jpg > hexdump.txt" to make a hexdump file.
3. Used "vim hexdump.txt" and do "/CTF" to search for a specific pattern. Copy those part to CyberChef and easily transform it to normal text using hexdump option.
4. Or Use " strings garden.jpg | grep -i "flag" " to avoid Line Breaks and Formatting Characters to occur. Instead of searching the text file, use the strings command on the original image. It extracts only the readable text and ignores the formatting issues

Answer: picoCTF{more_than_m33ts_the_3y395e12915}
