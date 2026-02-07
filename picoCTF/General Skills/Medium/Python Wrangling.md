# Author: syreal

# Description
Python scripts are invoked kind of like programs in the Terminal... Can you run ende.py using password.txt to get flag.txt.en?

# Hints
1. Get the Python script accessible in your shell by entering the following command in the Terminal prompt: $ wget followed by a link to the script. The link can be copied from the details section.
2. man python

# Steps
1. Downloaded the provided files.
2. Cat the password.txt and copy the password just in case.
3. First I ran the ende.py using "python3 ende.py". It return with "Usage: ende.py (-e/-d) [file]" I can guess what it means but let's try something else.
4. Ran "python3 ende.py flag.txt.en" and it return with "Please use '-e', '-d', or '-h'.".
5. So I used "python3 ende.py -h" and found the instruction on how to use this properly(I can just inspect the script using vim but let's play around lol).
6. -e is for encoding and -d is for decoding that's what is in my mind.
7. So I did "python3 ende.py -d flag.txt.en" and it prompt with the password, paste the password we got form before and we got the flag.

Answer: picoCTF{4p0110_1n_7h3_h0us3_9c5f9bcf}
