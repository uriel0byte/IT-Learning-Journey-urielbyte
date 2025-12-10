# Author: syreal

# Description
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file? Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/98/flag2of2-final.pdf). 

# Hints
1.  This problem can be solved by just opening the file in different ways

# Steps
1. Download the provided file.
2. After I used "wget" command to download the file, I used "file flag2of2-final.pdf" command to see what kind of file it  actually is. Found that it's PNG file.
3. Used "binwalk flag2of2-final.pdf" command to see if there is any hidden or embedded file in it. As the result, I don't understand anything so I asked AI...
 
   AI said
   
   This output comes from the binwalk tool and indicates that the file named flag2of2-final.pdf is a polyglot file, meaning it is deliberately structured to be valid for multiple file formats.

Here is a breakdown of what each line means:
🔬 Output Explanation

    urielbyte-picoctf@webshell:~/SecretOfPolyglot$ binwalk flag2of2-final.pdf

        This is the command executed. The user ran binwalk on a file that is ostensibly a PDF. The context (SecretOfPolyglot) further suggests this is a challenge related to files with multiple identities.

    Row 1: PNG Image (Offset 0)

        DECIMAL: 0

        HEXADECIMAL: 0x0

        DESCRIPTION: PNG image, 50 x 50, 8-bit/color RGBA, non-interlaced

        Meaning: binwalk's signature scanner found a PNG file header at the very beginning of the file (offset 0). This means the file starts with the correct "magic number" bytes to be recognized as a PNG image.

    Row 2: PDF Document (Offset 914)

        DECIMAL: 914

        HEXADECIMAL: 0x392

        DESCRIPTION: PDF document, version: "1.4"

        Meaning: binwalk found a PDF file header (which typically starts with %PDF-) at byte offset 914 (or 0x392 in hexadecimal) within the file. This means the file is also a valid PDF document.

    Row 3: Zlib Compressed Data (Offset 1149)

        DECIMAL: 1149

        HEXADECIMAL: 0x47D

        DESCRIPTION: Zlib compressed data, default compression

        Meaning: At offset 1149, there is a block of data compressed using the Zlib algorithm. This is not necessarily an embedded file, but often the content within PDF files (like streams or objects) is compressed using Zlib, or it could be a piece of data hidden inside the PNG structure.
        
4. Used "exiftool flag2of2-final.pdf" command to see if there is any useful information.

```
urielbyte-picoctf@webshell:~/SecretOfPolyglot$ ls
flag2of2-final.pdf

urielbyte-picoctf@webshell:~/SecretOfPolyglot$ file flag2of2-final.pdf 
flag2of2-final.pdf: PNG image data, 50 x 50, 8-bit/color RGBA, non-interlaced

urielbyte-picoctf@webshell:~/SecretOfPolyglot$ binwalk flag2of2-final.pdf 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 50 x 50, 8-bit/color RGBA, non-interlaced
914           0x392           PDF document, version: "1.4"
1149          0x47D           Zlib compressed data, default compression

urielbyte-picoctf@webshell:~/SecretOfPolyglot$ exiftool flag2of2-final.pdf 
ExifTool Version Number         : 12.40
File Name                       : flag2of2-final.pdf
Directory                       : .
File Size                       : 3.3 KiB
File Modification Date/Time     : 2024:03:12 00:36:42+00:00
File Access Date/Time           : 2025:12:10 09:35:43+00:00
File Inode Change Date/Time     : 2025:12:10 09:35:28+00:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 50
Image Height                    : 50
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Profile Name                    : ICC profile
Profile CMM Type                : Little CMS
Profile Version                 : 4.3.0
Profile Class                   : Display Device Profile
Color Space Data                : RGB
Profile Connection Space        : XYZ
Profile Date Time               : 2023:11:02 17:42:31
Profile File Signature          : acsp
Primary Platform                : Apple Computer Inc.
CMM Flags                       : Not Embedded, Independent
Device Manufacturer             : 
Device Model                    : 
Device Attributes               : Reflective, Glossy, Positive, Color
Rendering Intent                : Perceptual
Connection Space Illuminant     : 0.9642 1 0.82491
Profile Creator                 : Little CMS
Profile ID                      : 0
Profile Description             : GIMP built-in sRGB
Profile Copyright               : Public Domain
Media White Point               : 0.9642 1 0.82491
Chromatic Adaptation            : 1.04788 0.02292 -0.05022 0.02959 0.99048 -0.01707 -0.00925 0.01508 0.75168
Red Matrix Column               : 0.43604 0.22249 0.01392
Blue Matrix Column              : 0.14305 0.06061 0.71393
Green Matrix Column             : 0.38512 0.7169 0.09706
Red Tone Reproduction Curve     : (Binary data 32 bytes, use -b option to extract)
Green Tone Reproduction Curve   : (Binary data 32 bytes, use -b option to extract)
Blue Tone Reproduction Curve    : (Binary data 32 bytes, use -b option to extract)
Chromaticity Channels           : 3
Chromaticity Colorant           : Unknown (0)
Chromaticity Channel 1          : 0.64 0.33002
Chromaticity Channel 2          : 0.3 0.60001
Chromaticity Channel 3          : 0.15001 0.06
Device Mfg Desc                 : GIMP
Device Model Desc               : sRGB
Pixels Per Unit X               : 11811
Pixels Per Unit Y               : 11811
Pixel Units                     : meters
Modify Date                     : 2023:11:02 17:57:06
Comment                         : Created with GIMP
Warning                         : [minor] Trailer data after PNG IEND chunk
Image Size                      : 50x50
Megapixels                      : 0.003
```

5. So I used binwalk's extraction function (binwalk -e) to automatically extract the embedded file(s).
```
urielbyte-picoctf@webshell:~/SecretOfPolyglot$ binwalk -e flag2of2-final.pdf 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 50 x 50, 8-bit/color RGBA, non-interlaced
914           0x392           PDF document, version: "1.4"
1149          0x47D           Zlib compressed data, default compression

urielbyte-picoctf@webshell:~/SecretOfPolyglot$ ls
_flag2of2-final.pdf.extracted  flag2of2-final.pdf

urielbyte-picoctf@webshell:~/SecretOfPolyglot$ cd _flag2of2-final.pdf.extracted/

urielbyte-picoctf@webshell:~/SecretOfPolyglot/_flag2of2-final.pdf.extracted$ ls
47D  47D.zlib

urielbyte-picoctf@webshell:~/SecretOfPolyglot/_flag2of2-final.pdf.extracted$ ls -l
total 8
-rw-rw-r-- 1 urielbyte-picoctf urielbyte-picoctf  109 Dec 10 09:54 47D
-rw-rw-r-- 1 urielbyte-picoctf urielbyte-picoctf 2213 Dec 10 09:54 47D.zlib

urielbyte-picoctf@webshell:~/SecretOfPolyglot/_flag2of2-final.pdf.extracted$ file 47D
47D: ASCII text

urielbyte-picoctf@webshell:~/SecretOfPolyglot/_flag2of2-final.pdf.extracted$ cat 47D
q 0.1 0 0 0.1 0 0 cm
0 g
q
10 0 0 10 0 0 cm BT
/R7 16 Tf
1 0 0 1 50 250 Tm
(1n_pn9_&_pdf_1f991f77})Tj
ET
Q
Q
```

6. Looks like I found half of the flag.
7. So I tried opening the file in a pdf form, and found the same text.
8. Next I tried changing the extention or the type of the file (pdf -> png) and open it.
9. Voila! We got it...

Answer: picoCTF{f1u3n7_1n_pn9_&_pdf_1f991f77}
