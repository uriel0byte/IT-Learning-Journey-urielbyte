# Author: Prince Niyonshuti N.

# Description
The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log.
Download the encoded data here: [Logs Data](https://challenge-files.picoctf.net/c_amiable_citadel/1cb8d8924eb719b54af443989023e3ebc86051dc7e294a87634d5bffb84be2a1/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .

# Hints
1.  Use base64 to decode the data and generate the image file.

# Steps
1. Download the logs file.
2. Go to [base64.org](https://www.base64decode.org/) to decode and download the decoded file.
3. Got the PNG file with text on the image. So I go to this website https://www.imagetotext.info/ to extract the text from the image.
4. There are some other gibberish text but found the same text on the image which is 7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F63373564643038657D.
5. The text looks like a ASCII code or you can use Cipher Idenfifier online tool like [Dcode](https://www.dcode.fr/cipher-identifier) to identify what type of encryption/encoding from a text message.
6. Now we use online tool like Dcode to convert ASCII code to a normal text.

Answer: picoCTF{forensics_analysis_is_amazing_c75dd08e}
