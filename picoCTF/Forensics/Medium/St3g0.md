# Author: LT 'syreal' Jones (ft. djrobin17)

# Description
Download this image and find the flag.

# Hints
1. We know the end sequence of the message will be $t3g0.

# Steps
1. Download the provided file.
2. Used file command to verify that it is actually a PNG image.
3. Since it's a png and the name of this ctf implies that it's about steganography, I used "zsteg <image>" to extract hidden text, files, or binary data within PNG image file.
4. It's there.
5. The problem is if the room doesn't provide the hint, I would not know that it's about steganography. Only knowledge I have at this moment is that if it's an image used binwalk, exiftool to have the overall picture of what this might mean. I have to learn more about this...

Answer: picoCTF{7h3r3_15_n0_5p00n_a1062667}
