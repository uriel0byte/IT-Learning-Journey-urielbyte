# Author: Kevin Cooper/Danny

# Description
Find the flag in this [picture](https://challenge-files.picoctf.net/c_fickle_tempest/739119ebf098a2424ccce7d9e08e1af162dab0dc358950a6047750e37ec2bf2b/pico_img.png).

# Hints
1.  Ever heard of metadata?
2.  What does meta mean in the context of files?

# Steps
1. Download the provided file.
2. At first, I used "file" command to determine what type of file is this.

```
urielbyte-picoctf@webshell:~$ file pico_img.png 
pico_img.png: PNG image data, 600 x 600, 8-bit/color RGB, non-interlaced
```

3. Used the only tool I can think of "exiftool" to extract/read metadata information and found the flag in the Artist field.

```
urielbyte-picoctf@webshell:~$ exiftool pico_img.png 
ExifTool Version Number         : 12.40
File Name                       : pico_img.png
Directory                       : .
File Size                       : 106 KiB
File Modification Date/Time     : 2025:11:21 19:11:06+00:00
File Access Date/Time           : 2026:01:22 15:11:07+00:00
File Inode Change Date/Time     : 2026:01:22 15:10:54+00:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 600
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Software                        : Adobe ImageReady
XMP Toolkit                     : Adobe XMP Core 5.3-c011 66.145661, 2012/02/06-14:56:27
Creator Tool                    : Adobe Photoshop CS6 (Windows)
Instance ID                     : xmp.iid:A5566E73B2B811E8BC7F9A4303DF1F9B
Document ID                     : xmp.did:A5566E74B2B811E8BC7F9A4303DF1F9B
Derived From Instance ID        : xmp.iid:A5566E71B2B811E8BC7F9A4303DF1F9B
Derived From Document ID        : xmp.did:A5566E72B2B811E8BC7F9A4303DF1F9B
Artist                          : picoCTF{s0_m3ta_81e30680}
Image Size                      : 600x600
Megapixels                      : 0.360
```

4. The exiftool output reveals that the image was processed using Adobe Photoshop CS6. The XMP metadata (specifically the Derived From and Instance IDs) confirms the file is an exported version of a previous project, tracking its edit history.

# Explanation of the XMP IDs
Instance ID, Document ID, etc. are part of Adobe's XMP (Extensible Metadata Platform) system. They are used to track the history and lineage of a file as it gets edited.

1. Document ID (xmp.did)

    Definition: This identifies the "conceptual document."

    What it tells you: If you have five different versions of an image (e.g., draft1.psd, draft2.psd, final.png), they will often share the same Document ID because they are all the same project.

    Forensic use: It helps link different files together to prove they originated from the same source project.

2. Instance ID (xmp.iid)

    Definition: This identifies the specific state of the file at a specific moment in time.

    What it tells you: Every time you save or export a file in Photoshop, a new Instance ID is generated.

    Forensic use: It distinguishes between version 1 and version 2. If two files have different Instance IDs, they are different "saves."

3. Derived From (Derived From Instance/Document ID)

    Definition: This points back to the parent file.

    What it tells you: This specific PNG was not created from scratch; it was "derived" (exported or Save As'd) from a previous version.

    Forensic use: It proves the file was edited. The Creator Tool: Adobe Photoshop CS6 confirms this image was likely opened in Photoshop and then exported, creating this "child" file from a "parent" file.

Answer: picoCTF{s0_m3ta_81e30680}
