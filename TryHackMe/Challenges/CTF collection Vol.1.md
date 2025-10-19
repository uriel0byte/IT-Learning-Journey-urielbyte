# CTF collection Vol.1

# Description
Sharpening up your CTF skill with the collection. The first volume is designed for beginner.

# What is 
A cipher is a method, or algorithm, used in cryptography for performing encryption (converting readable text into unreadable text) and decryption (converting it back).

A cipher takes the original readable message, called plaintext, and a key to transform it into the unreadable form, called ciphertext.

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
2. 

Answer:

---
