# Author: Jeffery John

# Description
Someone's commits seems to be preventing the program from working. Who is it? You can download the challenge files here: [challenge.zip]

# Hints
1.  In collaborative projects, many users can make many changes. How can you see the changes within one file?
2.  Read the chapter on Git from the picoPrimer [here.](https://primer.picoctf.org/#_git_version_control)
3.  You can use python3 <file>.py to try running the code, though you won't need to for this challenge.

# Steps
1. Download the provided files.
2. Unzip the folder and do "ls -la" to see all the files.
3. Found message.py and .git directory. Change directory to .git/
4. Used "git log" to examine the history and state especially commit logs, but there's a twist because there were a lot of commits and we got a hint from that "message.py" file's name.
5. So, I used "git log -- message.py" to specify that we are looking for this file in the logs. Found 2 commits and one of them had the flag.

Answer: picoCTF{@sk_th3_1nt3rn_2c6bf174}
