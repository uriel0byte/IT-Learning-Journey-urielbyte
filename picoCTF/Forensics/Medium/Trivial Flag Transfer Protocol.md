# Author: Danny

# Description
Figure out how they moved the flag. `tftp.pcapng`

# Hints
1. What are some other ways to hide data?

# Steps
1. Download the provided `pcapng` file.
2. Open up Wireshark for analyzing the file.
3. Since it's TFTP, I used Wireshark's `File -> Export Objects -> TFTP` function.
4. Got 3 Pictures (`.bmp`), 2 Text files, and 1 Package (`.deb`).
5. First, I inspected the package and found that it's a `steghide` installer. This gave me the first hint that this challenge involves steganography.
6. Second, I opened the 2 text files (`instruction.txt` and `plan`) but they were encoded. I used the [dCode Cipher Identifier](https://www.dcode.fr/cipher-identifier) to identify the encoding technique. It turned out to be **ROT13**. After decoding them, I found what looked like a passphrase ("DUEDILIGENCE").
7. Third, I ran `steghide extract -sf <picture>` on the images one by one using the passphrase until I found the one containing a file called `flag.txt`. Finally, I used the `cat` command to reveal the plain text flag.

# What is a PCAPNG file?
**PCAPNG** (Packet Capture Next Generation) is a file that records network traffic. Think of it like a "recording" of all the data flowing through a network cable at a specific time. In forensics, we use tools like **Wireshark** to replay this recording and inspect exactly what data (passwords, files, websites) was sent between computers.

# What is TFTP?
**TFTP** stands for **Trivial File Transfer Protocol**. It is a very simple way to move files between computers. The "Trivial" part means it lacks security features—it has no login prompts and, most importantly, **no encryption**. This means anyone listening to the network (like us with the `.pcapng` file) can see and grab the files exactly as they were sent.

# What is "Export Object" and when to use it?
**Export Object** is a feature in Wireshark that automatically reassembles bits of data from the network traffic back into actual files.

* **How to know when to use it:** When you open a pcap file, look at the **Protocol** column. If you see protocols designed to transfer files—like **TFTP**, **HTTP**, **FTP**, or **SMB**—that is your clue.
* **Why use it:** Instead of manually trying to piece together thousands of tiny data packets, this function acts like a "Download" button, extracting the complete files (images, text, zips) directly to your computer.

# Why use Steghide instead of Zsteg?
While both tools are used for image steganography, the choice depends on the clues:

1.  **The Hint:** We extracted a file named `steghide-installer.deb` from the network traffic. The challenge author was literally giving us the tool they used!
2.  **The Method:** **Zsteg** is typically used for PNG/BMP files where data is hidden visually (LSB) without a password. **Steghide**, however, requires a **passphrase** to embed and extract data. Since we found a password ("DUEDILIGENCE") in the text files, Steghide was the logical tool to use.

*While zsteg is the standard tool for BMP files, it primarily detects LSB (Least Significant Bit) steganography which acts like a hidden layer of noise. Steghide, however, uses a different algorithm that scatters encrypted data across the file. Since zsteg cannot detect this scattered, encrypted data without a key, and I had found a passphrase ('DUEDILIGENCE'), steghide was the required tool to unlock the files.*

**Answer:** picoctf{h1dd3n_1n_pLa1n_51GHT_18375919}
