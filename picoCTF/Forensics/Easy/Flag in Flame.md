# Author: susie

# Description
Files can always be changed in a secret way. Can you find the flag? [cat.jpg](https://mercury.picoctf.net/static/c28a959c5605d5f67480d5dd3a77f302/cat.jpg)

# Hints
1.  Look at the details of the file
2.  Make sure to submit the flag as picoCTF{XXXXX}

# Steps
1. Download the provided jpg file.
2. Use Exiftool to view the metadata of the image " exiftool img.jpg "
3. Spotted the "License : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9 " looks like a base64 encoding.
4. Fire up CyberChef and paste it in with Base64 option.

Answer: picoCTF{the_m3tadata_1s_modified}
