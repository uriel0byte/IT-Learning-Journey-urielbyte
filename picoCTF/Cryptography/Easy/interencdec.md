# Author: NGIRIMANA Schadrack

# Description
Can you get the real meaning from this file. Download the file(https://artifacts.picoctf.net/c_titan/109/enc_flag) here. 

The enc_file 's content : YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyMHdNakV5TnpVNGZRPT0nCg==

# Hints
1.  Engaging in various decoding processes is of utmost importance

# What is Base64
Base64 is a binary-to-text encoding scheme that represents any kind of binary data (like images, sound, or files) in an ASCII string format.

Base64 is easy to recognize. It consists of letters (about 50% uppercase and 50% lowercase), as well as numbers, and often equal-characters (=) at the end. 

Its main purpose is to enable the safe transmission and storage of binary data over systems and protocols (like email or older versions of HTTP) that were originally designed to handle only plain ASCII text.

Key Points

    - Not Encryption: Base64 is not a form of encryption; it is easily reversible.

    - Size Increase: The encoded data is approximately 33% larger than the original binary data. (Three 8-bit bytes are represented by four 6-bit characters).

# What is Caesar Cipher
The Caesar Cipher is one of the simplest and oldest known encryption techniques, named after Julius Caesar, who is said to have used it.

It's a type of substitution cipher where each letter in the plaintext (original message) is replaced by a letter some fixed number of positions down or up the alphabet. This fixed number is the key (or shift).

# Steps
1. Open an online tool like Dcode or CyberChef or Use the terminal to decrypt the text.
2. If you are not sure what is the type of encrypted text, you can use online tool to help you identify the type such as Dcode(https://www.dcode.fr/cipher-identifier) or Boxen(https://www.boxentriq.com/code-breaking/cipher-identifier).
3. The provided text looks like Base64 (== at the end) so let's try that first.
4. Select the Base64 Cipher Tool. or Using the CLI command `echo "YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyMHdNakV5TnpVNGZRPT0nCg==" | base64 -d`
5. Got `b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX20wMjEyNzU4fQ=='` still looks like Base64 so let's try that again, but it fail probably because of that `b` at the start and `' '`. let's try to remove that and decrypt again.
6. Got `wpjvJAM{jhlzhy_k3jy9wa3k_m0212758}` This one looks like a Caesar Cipher .
7. Use Dcode(https://www.dcode.fr/caesar-cipher) to decrypt the message and we got the final flag.

Answer: picoCTF{caesar_d3cr9pt3d_f0212758}
