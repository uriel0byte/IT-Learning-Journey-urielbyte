# CTF collection Vol.1

# Description
Sharpening up your CTF skill with the collection. The first volume is designed for beginner.

# Task 1 Author note
Just another random CTF room created by me. Well, the main objective of the room is to test your CTF skills. For your information, vol.1 consists of 20 tasks and all the challenges are extremely easy. Stay calm and Capture the flag. :)

Note: All the challenges flag are formatted as THM{flag}, unless stated otherwise

# Task 2 What does the base said?

## Description
Can you decode the following? VEhNe2p1NTdfZDNjMGQzXzdoM19iNDUzfQ==

## Steps
1. Open an online tool like CyberChef (https://cyberchef.io/) or Use command "base64 -d <text>".
2. In this case, I used CyberChef.
3. Select the Base64.
4. Copy and paste the provided text.
5. Click BAKE or button to continue the process.
 
Answer: THM{ju57_d3c0d3_7h3_b453}

---

# Task 3 Meta meta

## Description
Meta! meta! meta! meta...................................

## Steps
1. Download the task file.
2. Use online tool to see the metadata of the file like (https://www.metadata2go.com/) or use command line tool like Exiftool .
3. In this case, I used Exiftool.
4. Type "exiftool <path to the file>".
5. Found the flag in Owner Name section.

Answer: THM{3x1f_0r_3x17}

---

# Task 4 Mon, are we going to be okay?

## Description
Something is hiding. That's all you need to know.

## Steps
1. Download the task file.
2. First, I look at the raw picture but found nothing. Then I used Exiftool to see the if there is anything in metadata.
3. Use command line tool Steghide.
4. Type "steghide extract -sf <yourfile>".
5. Then the prompt popped up with the "Enter passphrase", So I was trying to find that for a while, like phrases in the pictures but in fact you don't have to type anything just Enter.
6. Then the prompt popped up again just type "y".
7. Got the file that had been hiding inside the picture. Just cat it.

Answer: THM{500n3r_0r_l473r_17_15_0ur_7urn}

---

# Task 5 Erm......Magick

## Description
Huh, where is the flag?

## Steps
1. So basically, you just have to copy text inside the white box...

Answer: THM{wh173_fl46}

---

# Task 6 QRrrrr

## Description
Such technology is quite reliable.

## Steps
1. Download the task file.
2. It's QR code. Just use your phone or better use online tool to scan the provided QR code.

Answer: THM{qr_m4k3_l1f3_345y}

---

# Task 7 Reverse it or read it?

## Description
Both works, it's all up to you.

## Steps
1. Download the task file.
2. Use command line tool "strings"
3. Type " strings <file> | grep "THM" "
4. Got the flag.

Answer: THM{345y_f1nd_345y_60}

---

# Task 8 Another decoding stuff

## Description
Can you decode it? 3agrSy1CewF9v8ukcSkPSYm3oKUoByUpKG4L

## Steps
1. If you're not good at idetifying type of cipher, use online tool like (https://www.dcode.fr/cipher-identifier). It just takes time to be familiar with these (I am telling myself...)
2. So it looks like Base58. Let's use CyberChef again.
3. Got the flag.

Answer: THM{17_h45_l3553r_l3773r5}

---

# Task 9 Left or right

## Description
Left, right, left, right... Rot 13 is too mainstream. Solve this MAF{atbe_max_vtxltk}

## Steps
1. Fire up CyberChef again.
2. Choose ROT13 operation.
3. Now it said that it's too main stream let's try to decrease or increase the amount of rotation. (There is an option in ROT13 block on leftside for you to do that)
4. Got the flag.

Answer: THM{hail_the_caesar}

---

# Task 10 Make a comment

## Description
No downloadable file, no ciphered or encoded text. Huh .......

## Steps
1. The name says "comment". I think of comment in HTML langauge that make certain words or phrases unreadable by the browser or basically just a comment for developer to write something.
2. Right click on the Task 10 block. Click Inspect or just F12.
3. And there is a section that has a flag.

Answer: THM{4lw4y5_ch3ck_7h3_c0m3mn7}

---

# Task 11 Can you fix it?

## Description
I accidentally messed up with this PNG file. Can you help me fix it? Thanks, ^^ 

## Steps
1. Download the task file.
2. [Dump to Hex] Converts the binary file (spoil.png) into a single, continuous string of hexadecimal characters. Using "xxd -p spoil.png > spoil_hex" | Why? Hex is a text format that can be easily edited.
3. [Edit the Header] Opens the hex string file and replaces the wrong beginning bytes with the correct PNG signature (89504E470D0A1A0A). Using "vim spoil_hex_data" | Why? The operating system/renderer (like CyberChef) only knows a file is a PNG if it starts with this exact sequence.
4. [Repair & Render] The corrected hex string is converted back into binary data, and since the signature is now valid, the image is displayed, revealing the flag. Using CyberChef: "From Hex" → "Render Image" | Why? This reassembles the file correctly based on the fixed header.
5. Got the flag in picture form.

Answer: THM{y35_w3_c4n}

## Key Knowledge
The PNG file was corrupted by having its "Magic Number" (File Signature) removed or replaced. The fix is to convert the file to hex, replace the corrupted bytes with the correct PNG signature, and then convert it back to a readable image.

### How do I know it's the Magic Number problem (Well... I was in the dark too)
The core suspicion for a Magic Number problem comes from three main clues: Error Messages, the Challenge Description, and Hex Inspection.

The most direct clue is an error message when opening the file, like "Invalid file format" or "Could not decode image header," which tells you the software can't identify the file type. Second, the challenge description itself often gives it away, explicitly mentioning a "broken," "messed up," or "corrupted" file that needs "fixing." Finally, the definitive test is Hex Inspection: when you view the file's raw bytes (using a tool like xxd), the very first bytes do not match the known, required signature for that file type (e.g., the PNG signature 89504E470D0A1A0A). If those critical first bytes are wrong or missing, the operating system and programs cannot correctly read the file, confirming the magic number is the issue.

When a file (like PNG, JPEG, or ZIP) is broken and you suspect file corruption, the first step is always to check and fix the starting bytes (the Magic Number) using a hex editor or utility like xxd.

---

# Task 12 Read it

## Description
Some hidden flag inside Tryhackme social account.

## Steps
1. At first, I was like how tf am I supposed to know that so I click hint button and it said "reddit" F YOU
2. So I tried everything like TryHackMe CTF Collection Vol.1 flag or TryHackMe rooms reddit flag. I can't remember exactly what was the words.
3. If you're having a hard time to find just go to this (https://www.reddit.com/r/tryhackme/comments/eizxaq/new_room_coming_soon/) It's in here... 

Answer: THM{50c14l_4cc0un7_15_p4r7_0f_051n7}

---

# Task 13 Spin my head

## Description
What is this?

++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++++.------------.+++++.>+++++++++++++++++++++++.<<++++++++++++++++++.>>-------------------.---------.++++++++++++++.++++++++++++.<++++++++++++++++++.+++++++++.<+++.+.>----.>++++.

## Steps
1. At first, I was like yeah wtf is that?
2. So I search up and found that it's BrainFuck. It's an esoteric programming language consisting of characters like ++++---[+++].
3. So I used Dcode an online tool (https://www.dcode.fr/brainfuck-language).
4. Copy paste and you got the flag...

Answer: THM{0h_my_h34d}

---

# Task 14 An exclusive!

## Description
Exclusive strings for everyone!

S1: 44585d6b2368737c65252166234f20626d
S2: 1010101010101010101010101010101010

## Steps
1. I have no knowledge about this so again I clicked Hint button. It's S1 xor S2.
2. So i search for tools online (https://xor.pw/) or (https://www.compscilib.com/calculate/binaryxor?variation=default).
3. And just copy paste the given strings.

Answer: THM{3xclu51v3_0r}

# What is XOR
XOR, which stands for Exclusive OR, is a logical operation that outputs true (1) only when its inputs differ. If the inputs are the same, it outputs false (0).

In computing and cryptography, XOR is performed bit by bit on binary numbers, and it is represented by the symbol ⊕.

XOR is essential in cryptography because of its reversibility:

    Encryption: Data ⊕ Key = Ciphertext

    Decryption: Ciphertext ⊕ Key = Data

Applying the same key twice reverses the operation, making it a simple, fast method for encryption.

---

# Task 15 Binary walk

## Description
Please exfiltrate my file :)

## Steps
1. Download the task file.
2. I already know the "binwalk" tool used for analyzing, identifying, and extracting embedded files and executable code from binary files, especially firmware images.
3. So I did "binwalk <file>" and found that there is hello_there.txt inside.
4. Let's extract it by "binwalk -e <file>" and we got hell.jgp.extracted in return.
5. Let's check it by doing "ls <file/directory>" so it's a directory that has 2 files inside.
6. Let's just "cat" hello_there.txt
7. Got the flag.

Answer: THM{y0u_w4lk_m3_0u7}

---

# Task 16 Darkness

## Description
There is something lurking in the dark.

## Steps
1. Download the task file.
2. The hint for this is StegSolve. So I search up and download it.
3. Fire it up with "java -jar StegSolve.jar"
4. Add the dark picture file to it. And play around with it.

Answer: THM{7h3r3_15_h0p3_1n_7h3_d4rkn355}

## What is StegSolve
StegSolve is a powerful, graphical Java-based tool used primarily in Capture The Flag (CTF) competitions for image steganography analysis.

Its main function is to help reveal data hidden within images that is invisible to the naked eye. It does this by allowing users to manipulate and view the image's raw data through various filters and transformations, including:

- Bit Plane Viewing: Cycling through different color channels (Red, Green, Blue, Alpha) and their individual bit planes (Least Significant Bit/LSB, etc.) to look for subtle pixel changes that encode data.
- Color Inversion and Combinations: Applying transformations like XOR, addition, or subtraction to the image data, which can often make hidden patterns or messages appear.
- Layer/Frame Browsing: Viewing the separate layers of multi-layered files (like animated GIFs or multi-layered PNGs).

Essentially, it's the go-to utility for visually dissecting an image's structural data to uncover concealed messages.

---

# Task 17 A sounding QR

## Description
How good is your listening skill?

P/S: The flag formatted as THM{Listened Flag}, the flag should be in All CAPS

## Steps
1. Download the task file.
2. Scan it using online tool.
3. Brought us to the soundcloud. And I am pretty bad at this so...
4. There might be a way to download it and translate it to words right?

Answer: THM{SOUNDINGQR}

---

# Task 18 Dig up the past

## Description
Sometimes we need a 'machine' to dig the past

Targetted website: https://www.embeddedhacker.com/
Targetted time: 2 January 2020

## Steps
1. Search "Wayback machine". If you can't find it (https://web.archive.org/web/20200102131252/https://www.embeddedhacker.com/)
2. Copy paste the provided website, select the date, scroll through a bit you will find it. 

Answer: THM{ch3ck_th3_h4ckb4ck}

## What is WayBack Machine
The Wayback Machine is a massive digital archive of the World Wide Web, founded by the non-profit Internet Archive.

Its purpose is to provide "universal access to all knowledge" by periodically taking snapshots (or "captures") of websites and storing them permanently. This allows users to go "back in time" to see how a specific URL or website looked on a particular date in the past, even if the current website content has changed, moved, or been taken offline. It is an invaluable tool for historians, researchers, and forensic analysts.

---

# Task 19 Uncrackable!

## Description
Can you solve the following? By the way, I lost the key. Sorry >.<

MYKAHODTQ{RVG_YVGGK_FAL_WXF}

Flag format: TRYHACKME{FLAG IN ALL CAP}

## Steps
1. The description said he lost the key. It implied that it's "Vigenere Cipher"
2. Fire up CyberChef or Dcode select Vigenere Cipher.
3. So without a key, it's pretty hard to decrypt it. So let's guess what is the key?
4. At first, I tried "TRYHACKME" and the result is pretty close. but still looked weird.
5. So I tried "THM" and that's it...

Answer: TRYHACKME{YOU_FOUND_THE_KEY}

## What is Vigenere Cipher
The Vigenère Cipher is a method of encrypting alphabetic text using a series of different Caesar ciphers, making it a form of polyalphabetic substitution.

It uses a keyword (e.g., "LEMON"). This keyword is repeated over the entire plaintext message.

Each letter of the plaintext is shifted by an amount determined by the corresponding letter of the repeating keyword. For example, if the plaintext letter is 'A' and the key letter is 'L', the shift for 'A' is determined by the position of 'L' in the alphabet (L=11, where A=0).



---

# Task 20 Small bases

## Description
Decode the following text.

581695969015253365094191591547859387620042736036246486373595515576333693

## Steps
1. At first, I was like what? then I think it might be just a decimal. (https://www.rapidtables.com/convert/number/decimal-to-hex.html)
2. So I tried to convert it to normal ascii text but it's not working. So I convert it to hexadecimal first then to text.
3. Got the flag.

Answer: THM{17_ju57_4n_0rd1n4ry_b4535}

## What are Decimal, Hexadecimal, Binary, Octal and Plaintext
These terms refer to different number systems used in computing and a form of unencrypted text.

- Decimal (Base-10): This is the standard number system we use every day, employing ten unique digits (0 through 9). The value of a digit is based on its position, with each place representing a power of ten.

- Binary (Base-2): This is the fundamental number system for all computers, using only two digits: 0 and 1. It's used to represent all data and instructions within a computer as electrical signals (on or off).

- Octal (Base-8): This system uses eight digits (0 through 7). It was historically used in computing as a compact way to represent binary numbers, grouping three binary digits (bits) into one octal digit.

- Hexadecimal (Base-16): This system uses sixteen symbols: 0 through 9 and the letters A through F (where A=10,B=11, etc.). It's widely used in computing to represent large binary values efficiently, as four binary digits (bits) can be represented by a single hexadecimal digit.

- Plaintext: This is any data, usually text, that is not encrypted or encoded. It is human-readable and represents the original message before any cryptographic process is applied.

---

# Task 21 Read the packet

## Description
I just hacked my neighbor's WiFi and try to capture some packet. He must be up to no good. Help me find it.

## Steps
1. Fire up Wireshark, We have packet to analyse... load your packet capture file.
2. Let's put it into stream to utilize the packet capture data in a way that allows you to analyze the information more effectively. By streaming the data, you can filter and inspect packets in real-time, which can help you pinpoint specific anomalies, flags, or hidden messages.
3. In the filter bar at the top, you can enter expressions to narrow down the displayed packets. For example, to see only HTTP traffic, you can type http and press Enter.
4. Combine filters. For instance, tcp.port == 80 to see traffic on port 80.
5. Use the 'Follow TCP Stream' option (right-click on a packet) to view the entire conversation for a specific connection. This can help isolate potential flags or messages more easily.
6. I suggested looking at HTTP specifically because it's a common protocol used for web traffic, and flags are often embedded within HTTP requests or responses in network challenges. To determine which protocol to focus on, consider the context of your task or any hints provided. Analyzing the packet capture metadata can also reveal which protocols are present. For instance, if you notice a lot of traffic on port 80 or 443, it indicates HTTP or HTTPS traffic, respectively. By filtering for these protocols, you can more efficiently search for flags.
7. Found a frame that has text file in it. Look closely...

Answer: THM{d0_n07_574lk_m3}

---
