# Author: Alex Fulton/Danny Tunitis

# Description
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?

# Hints
1. Remember the flag format is picoCTF{XXXX}
2. What's a pipe? No not that kind of pipe... This kind

# Steps
1. Connected to the remote server via nc.
2. Found that the server respond with a lot of text so it's better to output this to a new file with nc fickle-tempest.picoctf.net 50361 > plumbling
3. Then we can search for the flag with cat plumbling | grep -i "picoctf"

Answer: picoCTF{digital_plumb3r_0BAc587E}
