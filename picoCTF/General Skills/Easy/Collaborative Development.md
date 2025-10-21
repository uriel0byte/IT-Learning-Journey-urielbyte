# Author: Jeffery John

# Description
My team has been working very hard on new features for our flag printing program! I wonder how they'll work together? You can download the challenge files here: https://artifacts.picoctf.net/c_titan/69/challenge.zip

# Hints
1.  git branch -a will let you see available branches
2.  How can file 'diffs' be brought to the main branch? Don't forget to git config!
3.  Merge conflicts can be tricky! Try a text editor like nano, emacs, or vim.

# What is Git Version Control
[Git Notes](https://github.com/uriel0byte/IT-Learning-Journey-urielbyte/blob/cd93cdd5ee5b0f24ef79bf3329c708c1e94dc2bb/Notes/Git/git_version_control_writeup.md)

# Steps
1. Download the provided zip file.
2. Unzip the file and we got the "drop-in" directory.
3. It's a git repo and there is a text.file there.
4. It's a first part of the actual python script. What we have to do is check branches. Go into each branches copy the python script in each branches. Merge them into one single script.
5. Using Vim or other text editor to merge them.
6. Run the script " python3 flag.py "

Answer: picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_e4b79efb}
