# Author: Yahaya Meddy

# Description
You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag.
Download the jpg image [here](https://challenge-files.picoctf.net/c_saffron_estate/984460cb7eebc16b2908f91210cb8dc4936c63cb6d28c9475fa38dc6a443d1d6/img.jpg).

# Hints
1.  Download the jpg image and read its metadata

# Steps
1. Download the provided jpg file.
2. Use Exiftool to view the metadata of the image " exiftool img.jpg "
3. Spotted the Comment section : "c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9" looks like a base64 encryption.
4. Check with CyberChef, turned out it is base64 with this output : " steghide:cEF6endvcmQ= "
5. " cEF6endvcmQ= " also looks like a base64, turned out it is with output : pAzzword It's probably a passphase for a steghide
6. Now go back to terminal and extract the hidden file with " steghide extract -sf img.jpg "
7. Put the passphrase in and got the flag.txt in return then cat it.

Answer: picoCTF{h1dd3n_1n_1m4g3_2ac27d95}
