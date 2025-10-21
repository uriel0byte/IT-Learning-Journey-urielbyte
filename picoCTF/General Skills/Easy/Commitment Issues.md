# Author: Jeffery John

# Description
I accidentally wrote the flag down. Good thing I deleted it! You download the challenge files here: https://artifacts.picoctf.net/c_titan/138/challenge.zip

# Hints
1.  Version control can help you recover files if you change or lose them!
2.  Read the chapter on Git from the picoPrimer [here](https://primer.picoctf.org/#_git_version_control) <- Should read.
3.  You can 'checkout' commits to see the files inside them

# What is Git Version Control
[Git Notes](https://github.com/uriel0byte/IT-Learning-Journey-urielbyte/blob/cd93cdd5ee5b0f24ef79bf3329c708c1e94dc2bb/Notes/Git/git_version_control_writeup.md)

# Steps
1. Download the provided zip file.
2. Unzip the file and we got the "drop-in" directory.
3. It's a git repo and there is a text.file there.
4. So I first check the git log first. There are 2 commitment, so I check the first one with "git show <commit number>"
5. Found the flag.

Answer: picoCTF{s@n1t1z3_c785c319}
