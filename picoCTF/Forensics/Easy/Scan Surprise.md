# Author: Jeffery John

# Description
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? You can download the challenge files here:

[challenge.zip](https://artifacts.picoctf.net/c_atlas/3/challenge.zip)

Additional details will be available after launching your challenge instance.

# Hints
1.  QR codes are a way of encoding data. While they're most known for storing URLs, they can store other things too.
2.  Mobile phones have included native QR code scanners in their cameras since version 8 (Oreo) and iOS 11
3.  If you don't have access to a phone, you can also use zbar-tools to convert an image to text

# Steps
1. Download the zip file.
2. Unzip the file with "unzip challenge.zip"
3. Found the flag.png which contain QR code.
4. Scan it with mobile phone or use online tool such as zbar-tools!

Answer: picoCTF{p33k_@_b00_a81f0a35}
