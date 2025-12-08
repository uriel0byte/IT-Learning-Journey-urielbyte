# Author: Prince Niyonshuti N.

# Description
Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered.
Find the PDF file here [Hidden Confidential](https://challenge-files.picoctf.net/c_amiable_citadel/a8aa03694837741eed59c479749fc7f5bfd14fa66f4295b83776f16b2003a67d/confidential.pdf) Document and uncover the flag within the metadata.

# Hints
1.  Don't be fooled by the visible text; it’s just a decoy!
2.  Look beyond the surface for hidden clues

# What is Metadata
Metadata in cybersecurity, particularly in the context of a CTF challenge, is the data that describes other data, and it serves as a critical, often overlooked, source of forensic evidence or hidden clues. This information can be embedded directly within files as EXIF data (revealing creation times, authors, or even GPS coordinates), exist as network traffic headers (detailing IP addresses, ports, and connection timings without showing the message content), or appear in web source code (like hidden HTML comments or specific HTTP response headers). In a CTF writeup, the metadata explanation demonstrates the process of using tools like exiftool or Wireshark to successfully extract these seemingly benign details, which ultimately unlock the path to finding the flag or exploiting a vulnerability.

# Steps
1. Download the provided PDF file.
2. First read the PDF file, found no useful info.
3. Move on to CLI to find more info in the metadata section with exiftool. Used "exiftool confidential.pdf"
4. In the Author section there's a Base64 text. Just copy and decrypt it with CyberChef.

Answer: picoCTF{puzzl3d_m3tadata_f0und!_c2073669}
