# Author: Shuailin Pan (LeConjuror)

# Description
RED, RED, RED, RED Download the image: [red.png](https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png)

# Hints
1.  The picture seems pure, but is it though?
2.  Red?Ged?Bed?Aed?
3.  Check whatever Facebook is called now.

# What is Steganography
Steganography is the art and science of hiding secret data within an ordinary, non-secret file or message in order to avoid detection; the hidden data is effectively "hidden in plain sight." Unlike cryptography, which scrambles a message so it cannot be read, steganography conceals the very existence of the message itself, often by embedding it into the noise or unused bits of media files like images (PNG, JPG) or audio tracks.

# Steganography vs. Metadata
Steganography is the practice of concealing secret information within another non-secret file, such as hiding a text string inside the color values of an image's pixels. Unlike metadata (which yI normally analyzed with exiftool), which acts like a visible "shipping label" describing the file (time, date, camera model), steganography acts like a "hidden compartment" inside the package itself. While metadata is stored in readable headers attached to the image, steganographic data is interwoven into the actual visual data (bits), meaning the image looks normal to the human eye but contains hidden code that exiftool cannot see.

# What is Zsteg tool
zsteg is a specialized command-line tool for PNG and BMP forensics that automatically scans for hidden data effectively "brute-forcing" common steganography techniques. It iterates through various data encoding methods, most notably Least Significant Bit (LSB) steganography, where the last bit of a pixel's color value is swapped for secret data bits. In a CTF context, if exiftool or strings returns nothing, zsteg is often the next step because it peels back the visual layers of the image to find hidden text, flags, or files that are mathematically embedded in the pixel data. It is a Security Operations solution designed to help security teams with Steganography, PNG, Steganalysis.

# Steganography tools that I think it's used a lot
1. Steghide (Best for JPEG/WAV)

Steghide is a classic command-line tool used primarily to hide (embed) and extract secret data from JPEG images and WAV audio files. Unlike zsteg, which looks for visual bit manipulation, steghide uses graph-theoretic algorithms to scatter the hidden data, and it almost always requires a passphrase to extract the content. In CTFs, if you find a .jpg that seems suspicious, you often use steghide (sometimes paired with a brute-force tool like stegseek if you don't have the password) to unlock the flag.

2. Stegsolve (Best for Visual Inspection)

Stegsolve is a Java-based GUI tool that acts like an X-ray filter for images. Instead of using command-line arguments, you open an image in Stegsolve and click through different "color planes" (e.g., Red plane 0, Blue plane 3). It is perfect for challenges where the flag is visually hidden in a specific color layer or requires XORing (combining) two images to reveal the text. It is often the first step when you have a weird-looking image but no obvious file signature clues.

3. Binwalk (Best for Hidden Files)

While not strictly "steganography" (it's technically file carving), binwalk is essential for checking if one file is glued onto the end of another. For example, a CTF challenge might hide a ZIP file inside a PNG image. Running binwalk -e image.png will automatically detect the hidden ZIP header buried in the file's bytes and extract it for you.

# Steps
1. Download the provided png file.
2. Use Exiftool to view the metadata of the image " exiftool red.png "
3. Spotted the Poem Section : "Crimson heart, vibrant and bold,.Hearts flutter at your sight..Evenings glow softly red,.Cherries burst with sweet life..Kisses linger with your warmth..Love deep as merlot..Scarlet leaves falling softly,.Bold in every stroke." Looks a bit weird huh?
4. But there is nothing I know or can do more. So I thought of Steganography, did a little bit of research because I forgot what it is and the tools about it.
5. Used command "zsteg red.png" Found
```
urielbyte-picoctf@webshell:~$ zsteg red.png 
meta Poem           .. text: "Crimson heart, vibrant and bold,\nHearts flutter at your sight.\nEvenings glow softly red,\nCherries burst with sweet life.\nKisses linger with your warmth.\nLove deep as merlot.\nScarlet leaves falling softly,\nBold in every stroke."
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="
```
6. Looks like a repeated base64 encoding so I copied one of them and analyze it in CyberChef.

Answer: picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
