# Author: Mubarak Mikail

# Description
How about some hide and seek? Download this file [here](https://artifacts.picoctf.net/c_titan/129/unknown.zip). 

# Hints
1.  How can you view the information about the picture?
2.  If something isn't in the expected form, maybe it deserves attention?

# Steps
1. Download the provided file.
2. Unzip it and found the jpg file. Open it found nothing maybe it's in the metadata.
3. Used "exiftool ukn_reality.jpg" command and found "Attribution URL : cGljb0NURntNRTc0RDQ3QV9ISUREM05fYjMyMDQwYjh9Cg== " where it looks like a base64 encoding.
4. Open CyberChef and paste it in and got it.

Answer: picoCTF{ME74D47A_HIDD3N_b32040b8}
