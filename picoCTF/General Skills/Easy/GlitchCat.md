# Author: LT 'syreal' Jones

# Description
Our flag printing service has started glitching!

Additional details will be available after launching your challenge instance.

# Hints
1. ASCII is one of the most common encodings used in programming
2. We know that the glitch output is valid Python, somehow!
3. Press Ctrl and c on your keyboard to close your connection and return to the command prompt.

# Steps
1. Connect to the remote server using netcat.
2. We got the flag but it's encoded in hexadecimal format (picoCTF{gl17ch_m3_n07_' + chr(0x61) + chr(0x34) + chr(0x33) + chr(0x39) + chr(0x32) + chr(0x64) + chr(0x32) + chr(0x65) + '}) To retrieve the flag, I had to reverse the Character Encoding process.
3. Since this challenge was literally Python code (chr(0x61)), sometimes the fastest app is just an online python runner. Like (https://www.programiz.com/python-programming/online-compiler/) So I can just paste print(chr(0x61) + ...) directly there and hit "Run."
4. Or you can use CyberChef. Paste your hex codes (e.g., 61 34 33 39) into the Input box. Search for "From Hex" in the left menu and drag it to the Recipe area.
5. After decoded the Python expression, just put them all together.

Answer:  picoCTF{gl17ch_m3_n07_a4392d2e}
