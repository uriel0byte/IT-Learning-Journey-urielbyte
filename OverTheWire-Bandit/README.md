# OverTheWire Bandit Levels 0-33

Published - 2025

**Goal:** Solve all levels of the OverTheWire Bandit wargame to practice fundamental Linux commands.

---

# Level 0 -> 1

**Challenge:** The password for the next level is in a file called `readme` in the home directory.

**Methodology:**
1.  Logged in as `bandit0` using the provided password.
2.  Used `pwd` to print current directory path.
3.  Used the `ls` command to list the files in the current directory with `-l` flag to long listing format.
4.  Found the `readme` file.
5.  Used `file` to detetrmine the file type.
6.  Used the `cat` command to read the contents of the `readme` file.
7.  Copied the password and used it to log in to the next level.

[![asciicast](https://asciinema.org/a/6JgAIb20gnx1t2wWjn27kfEk1.svg)](https://asciinema.org/a/6JgAIb20gnx1t2wWjn27kfEk1)

**Commands Used:**
`pwd`
`ls`
`file`
`cat`
---

# Level 1 -> 2

**Challenge:** The password for the next level is stored in a file called - located in the home directory

**Methodology:**
1.  Logged in as `bandit1` using the password we got from the last time.
2.  Used `pwd` to print current directory path.
3.  Used the `ls` command to list the files in the current directory.
4.  Found the `-` file.
5.  Used `file` to detetrmine the file type.
6.  *The problem with this is our terminal interprets the HYPHEN as flags.*
7.  *Instead of specifying the name of the file, we specify the path to the file, which are Absolute path or Relative path.*
8.  Used the `cat` command to read the contents of the `-` file by using `cat ./-`. or `cat ~/-` or `cat /home/bandit1/-`

[![asciicast](https://asciinema.org/a/YEoDfLj1H4YgcSE3VlmVLVwOV.svg)](https://asciinema.org/a/YEoDfLj1H4YgcSE3VlmVLVwOV)

**Commands Used:**
`pwd`
`ls`
`file`
`cat`
---

# Level 2 -> 3

**Challenge:** The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

**Methodology:**
1.  Logged in as `bandit2` using the password we got from the last time.
2.  Used `pwd` to print current directory path.
3.  Used the `ls` command to list the files in the current directory.
4.  Found the `--spaces in this filename--` file.
5.  *The key problem is that the space character is a delimiter in the Linux shell, used to separate a command from its arguments. If you try to run `cat --spaces in this filename--`, the shell will interpret `--spaces, in, this, and filename--` as four separate arguments, causing an error.*
6. To solve this, you need to escape the spaces. Escaping tells the shell to treat the following character literally, not as a special character. The most common way to do this is with a backslash `\`
7. By running `cat --spaces\ in\ this\ filename--`, you instruct the shell to treat each space as part of the filename. 
8. Another common and often easier method is to enclose the entire filename in quotation marks. This also tells the shell to treat everything inside the quotes as a single argument. The command would be `cat "--spaces in this filename--"`.
9.  The trick I used in the video down below is `Tab completion` to automatically escape the spaces for you. By typing the first few characters `(--s)` and then pressing the `tab` key twice, the shell will complete the filename and add the necessary backslashes.

[![asciicast](https://asciinema.org/a/tY7ROPUXtUCa6eYCdXMxeBMr7.svg)](https://asciinema.org/a/tY7ROPUXtUCa6eYCdXMxeBMr7)

**Key Takeaway:**
Spaces and other special characters like `*`, `$`, and `&` have a specific meaning to the shell. To treat them as a literal part of a filename or string, you must escape them with a backslash `\` or enclose the entire string in single or double quotes.

**Commands Used:**
`pwd`
`ls`
`cat`
---

# Level 3 -> 4

**Challenge:** The password for the next level is stored in a hidden file in the inhere directory.

**Methodology:**
1.  Logged in as `bandit3` using the password we got from the last time.
2.  Used `pwd` to print current directory path.
3.  Used the `ls -l` command to list the files in the current directory.
4.  Found the `inhere` directory.
5.  Used `cd` to change directory to `inhere` directory then `ls -la`.
6.  *The key problem is that a hidden file has a `.` as the first character of their file name. A normal `ls` or `ls -l` won't show hidden files*
7. To solve this, you need can use `ls` with `-a` flag to show hidden files.
8. Or you can use `find` command to search for all files that start with `.`. By using `find -name ".*"`.
9. `find [directory path] [expression]` in the command above we use `find` without the `[directory path]` leaving it blank will search in current directory.
10. After we found a `Hidden file` we use `cat` command to reveal its content.
   

[![asciicast](https://asciinema.org/a/CPstDvPxH6EQP3OdDcioxfFeV.svg)](https://asciinema.org/a/CPstDvPxH6EQP3OdDcioxfFeV)

**Key Takeaway:**
**Wildcard (*):** Used to represent any sequence of characters, particularly useful when the exact file name is `unknown`. "For times where we do not know the exact file name we can add an aster at the end to search for all files that have names that include what you specified."

**Commands Used:**
`pwd`
`ls -la`
`cat`
`find <path> -name "<>"`
---

# Level 4 -> 5

**Challenge:** The password for the next level is stored in the only human-readable file in the inhere directory.

**Explanation:** `Human-readable` files is files that contain data that is easily read. Like text files and not binary file where software's are requied to understand its content.
There are a types of data of the file (e.g., "`ASCII text`," "`JPEG image data`," "`shell script`," "`ELF`," "`data`"). `ELF` or `data` file, for example, are not human-readable.

The most common data encodings that are human-readable are `ASCII` and `Unicode` such as `UTF-8`.

**Methodology 1:**
1.  Logged in as `bandit4` using the password we got from the last time.
2.  Used `pwd` to print current directory path.
3.  Used the `ls -l` command to list the files in the current directory.
4.  Found the `inhere` directory.
5.  Used `cd` to change directory to `inhere` directory then `ls -la`.
6.  *The key problem is there are a lots of files in this directory. We could just print the contents of every file `cat`. This is, however, not very efficient when we deal with a lot of files. And the Hyphen `(-)` as the first character but we already know how to deal with that*
7. Instead, We use `file ./-*` command to gives us the type of data of the files. We utilize the knowledge we got from before like `./` to specify this current directory and `*` to specify all files. The normal command structure is `file <filename>`
8. This tells us:

`file00`: Looks like text but uses a non-standard encoding

`file07`: A normal ASCII text file ← this one is the most promising

`Others`: Just say "`data`", which usually means it's not readable text (could be binary or garbage)

9. Now we `cat` as usual.


**Methodology 2 (More advanced):**
1.  We can used more advanced commands by combinding `find` `file` (we already know those) and `grep` commands
2.  `grep` command is used to search for patterns or texts within files.
3.  So, the command look like this  ```find -type f -exec file {} + | grep "text"```
  
      💡**Breakdown of the Command**
    
    **`find`**: This is the main command used to search for files and directories within a file system.
    
    **`-type f`**: This option restricts the search to only **files** (not directories, links, or other special file types).
    
    **`-exec file {} +`**: This part executes the `file` command on all the files found by `find`.
    
       **`-exec`**: This is an action that runs a command on each file found.
    
       **`file {}`**: The `file` command determines the **type of a file** (e.g., "ASCII text," "JPEG image data," "shell script"). The `{}` is a placeholder that `find` replaces with the name of each file it finds.
    
       **`+`**: This is a more efficient way to use `-exec`. It bundles the filenames together and passes them to the `file` command in one go, rather than running the command for each file individually.
    
    **`|`**: This is a **pipe**. It takes the output of the command on the left (`find ... -exec file {} +`) and uses it as the input for the command on the right (`grep "text"`).
    
    **`grep "text"`**: This command filters the output from the `file` command, displaying only the lines that contain the string **"text"**. Since the `file` command often describes plain text files as "ASCII text" or "UTF-8 text," this effectively filters for files that are **text-based**.
    
     **In short,** the `find` command locates files of a specific size, and the `grep` command then filters that list to show only the ones that the system identifies as a text file.
    
5.  So the result are `-file00` and `-file07` but the `-file00`: It says `"Non-ISO extended-ASCII text"`, which means it has unusual or outdated character encoding. It might look like gibberish or be unreadable.
6.  Next we do what we always do `cat` it!
    

[![asciicast](https://asciinema.org/a/ZUOHfWa4qJxvmY3MTp5wUcXqB.svg)](https://asciinema.org/a/ZUOHfWa4qJxvmY3MTp5wUcXqB)

**Key Takeaway:**
**Learn more about encoding types**

**Commands Used:**
`ls -la`
`cat`
`file`
`grep`
`find <path> -type <> -exec <> {} +`
---

# Level 5 -> 6

**Challenge:** The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

    human-readable
    
    1033 bytes in size
    
    not executable

**Methodology:**
1.  Logged in as `bandit5` using the password we got from the last time.
2.  Used the `ls -l` command to list the files in the current directory.
3.  Used `cd` to change directory to `inhere` directory then `ls -la`.
4.  Let's try to `ls la` one of the directories to see if it's empty or there are files in it.
5.  *The key problem is there are a lot of directories here. We could `cd` in each directory and print  `cat` the contents of every files then. This is, however, not efficient when we deal with a lot of directories and files.*
6. Now we can utilize the knowledge from the last level, but before we do that let's look at the properties of the file again:

   `human-readble` we already know that normal human-readable files are `ASCII text` or `Unicode` (`UTF-8`).

   `1033 bytes in size` we use flag `-size` and use `1033c` for bytes e.g. suffixes `c` bytes, `k` kilobytes and so on.

   `not executable` we use flag `-executable` and for `not` use `!` exclamation mark before the flag.
   
7. So the command would look like this `find -type f -size 1033c ! -executable -exec file {} + | grep "text"`.
8. Then we `cat` it!

[![asciicast](https://asciinema.org/a/18Z1GZUw2M3PvXD3niG8yFoNN.svg)](https://asciinema.org/a/18Z1GZUw2M3PvXD3niG8yFoNN)

**Key Takeaway:** `!` before a `primary` when using the `find command` to search for the file that `not match` that condition

**Commands Used:**
`cat`
`file`
`grep`
`find <path> -type <> -size <> ! -executable -exec <> {} +`
---

# Level 6 -> 7

**Challenge:** The password for the next level is stored somewhere on the server and has all of the following properties:

    owned by user bandit7
    owned by group bandit6
    33 bytes in size

**Methodology:**
1.  Logged in as `bandit6` using the password we got from the last time.
2.  Used the `ls -la` command to list the files in the current directory.
3.  Found some files but the challenge says that the password is stored somewhere on the server so we have to start searching from root `/`.
4.  Now we can utilize the knowledge from the last level, but before we do that let's look at the properties of the file again. There are new primaries that we do not know:
   
   `owned by user bandit7` we use `-user <name>`
   
   `owned by group bandit6` we use `-group <groups name>`
   
5.  So for this level it does not say that the file is `human-readble` file but let's assume that it's atleast store in a `file`
6.  The command would look like this (do not forget to specify the path, which start from the root `/`):

   `find / -type f -user bandit7 -group bandit6 -size 33c`

7.  *If you try that command, It would show a lot of `Permission Denied` because there are some files that we are not allow to use the command on. Basically, we do not have the enough permissions for those file. You can manaully scroll and find the file that does not show that message, which is pretty hard and not efficient.*
8.  So there is a better way for that, which is that we add `2>/dev/null` after the command.

   `2>/dev/null` hides error messages from your terminal.

   💡Let’s break it down:

   `2` → This refers to "Standard Error" (the channel where error messages go).

   `>` → This means redirect.

   `/dev/null` → This is a special place in Linux that throws things away. It's like a black hole — anything sent here disappears.
   
9.  The final command looks like this: `find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null`
10.  Then we `cat` the file by specifying the Absolute path.

[![asciicast](https://asciinema.org/a/whLGYb4u6g61msqAE6hkpFjkD.svg)](https://asciinema.org/a/whLGYb4u6g61msqAE6hkpFjkD)

**Key Takeaway:** Use `2>/dev/null` to hide unnecessary error messages, so you can focus only on the important output — like when searching through lots of files or running commands that might fail on some inputs.

**Commands Used:**
`ls -la`
`cat`
`find <path> -type <> -size <> -user <name> -group <group>`
---

# Level 7 -> 8

**Challenge:** The password for the next level is stored in the file data.txt next to the word millionth.

**Methodology:**
1.  Logged in as `bandit7` using the password we got from the last time.
2.  Used the `ls` command to list the files in the current directory.
3.  Found the `data.txt`file.
4.  Used `wc` to estimate the content inside. Just for a better understanding of what we are dealing with.

    `wc` shows number of lines, words, and byte count
    
    `-l` shows number of lines
    
    `-w` shows number of words
    
    `-m` shows number of characters
    
6.  We know that `the password` is stored next to the word `millionth`, and we know that `grep` return the entire line of the search pattern.
7.  So we do `cat data.txt | grep "millionth"` or `grep "millionth" data.txt`.

[![asciicast](https://asciinema.org/a/Wpms0rExRwqYurhqs5vpssBXU.svg)](https://asciinema.org/a/Wpms0rExRwqYurhqs5vpssBXU)

**Key Takeaway:** Use `wc` to have a better view of a file. Use `man` to learn a little more of `wc`

**Commands Used:**
`ls`
`cat`
`grep <pattern> <path>`
---

# Level 8 -> 9

**Challenge:** The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

**Methodology:**
1.  Logged in as `bandit8` using the password we got from the last time.
2.  Used the `ls` command to list the files in the current directory. Found the `data.txt`file.
3.  In this clip, I used `file` to see if it's a normal reable file or not and used `wc` to estimate the content inside.
4.  We know the `password` is `the only line of text that occurs only one` so there are tools for that, which are `sort` and `uniq`

    `sort` arranges all the lines in the file alphabetically.
    
    `uniq` compare a line with the **immediately preceding line**. with
           `-u` flag stands for "unique" and tells `uniq` to **only** print lines that appear exactly once in the input.
    
6.  Normal confusion that might happen:

    `uniq data.txt` or `uniq -u` doesn't work as you'd expect because the `uniq` command is designed to work on **adjacent, identical lines**. It requires the input to be sorted first.
    
    `sort data.txt | uniq` this command would give you a list of every single unique line in the file. If a line appeared 50 times, it would be printed once. The single password line would also be printed. This would leave you with a long list to manually search through.
    
    `sort data.txt | uniq -u` this is the right command for this level. we use `sort` first to arranges all the lines in the file alphabetically. This groups all the identical lines together, making them **adjacent** to each other. the `-u` flag is what specifically filters for the **single, non-duplicated** line.
    
7.  Final command : `sort data.txt | uniq -u`
   

[![asciicast](https://asciinema.org/a/DDXus5JYNqki0rklyMl9vglXh.svg)](https://asciinema.org/a/DDXus5JYNqki0rklyMl9vglXh)

**Key Takeaway:** Take it slowly, Slow progress is better than no progress!

**Commands Used:**
`ls`
`cat`
`sort <path>`
`uniq -u <path>`
---

# Level 9 -> 10

**Challenge:** The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

**Methodology:**
1.  Logged in as `bandit9` using the password we got from the last time.
2.  Used the `ls` command to list the files in the current directory. Found the `data.txt`file.
3.  Used `file` to see if it's a normal reable file or not and used `wc` to estimate the content inside.
4.  We know that the file is `data` type of file which is not human-readable and has a lot of chracters in it. So, Manaully finding it might not be very efficient.
5.  We know that the `password` is stored in `data.txt` in one of the few human-readable strings, preceded by several `=` characters. There is a tool for that `strings`

    `strings <options> <file>` print the sequences of printable characters in files
    
6.  So the command would be `strings data.txt | grep "="`. Do not forget that the password is preceded by serveral `=`.

[![asciicast](https://asciinema.org/a/8dnaOofESCcSPZsp73lxKDXGr.svg)](https://asciinema.org/a/8dnaOofESCcSPZsp73lxKDXGr)

**Key Takeaway:** Use `man` command to learn more about `strings`.

**Commands Used:**
`ls`
`cat`
`grep`
`strings <options> <file>`
---

# Level 10 -> 11

**Challenge:** The password for the next level is stored in the file data.txt, which contains base64 encoded data.

**Methodology:**
1.  Logged in as `bandit10` using the password we got from the last time.
2.  Used the `ls` command to list the files in the current directory. Found the `data.txt`file.
3.  Used `file` to see if it's a normal reable file or not and used `wc` to estimate the content inside.
4.  We know that the file is `ASCII text` type of file which is a human-readable but encoded in base64.
5.  There is a tool for decoding base64 which is `base64`

    `base64 <options> <file>` encode/decode data and print it out.

    `-d` for decoding in `base64`
    
6.  So the command would be `base64 -d data.txt` or `cat data.txt | base64 -d`. 

[![asciicast](https://asciinema.org/a/wepUute14a4fqb1IrbQNMZICL.svg)](https://asciinema.org/a/wepUute14a4fqb1IrbQNMZICL)

**Key Takeaway:** Use `man` command to learn more about `base64`. Learn more about types of encoded data.

**Commands Used:**
`ls`
`cat`
`file`
`wc`
`base64 <options> <file>`
---

# Level 11 -> 12

**Challenge:** The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

**Methodology:**
1.  Logged in as `bandit11` using the password we got from the last time.
2.  Used the `ls` command to list the files in the current directory. Found the `data.txt`file.
3.  Used `file` to see if it's a normal reable file or not and used `wc` to estimate the content inside.
4.  We know that the file is rotated by 13 position, At first I don't know what to do too, So we have to know about [ROT13](https://en.wikipedia.org/wiki/ROT13) just a bit.
5.  Now we know what Rot13 is, There is a tool for decoding Rot13 which is `tr`

    `tr <options> <string1> <string2>` translate or delete characters.

    
6.  So the command would be `cat data.txt | tr 'A-za-z' 'N-ZA-Mn-za-m`.
   
   The first argument (`'A-Za-z'`) is the set of characters you want to translate. This includes all uppercase letters (A-Z) and all lowercase letters (a-z).

   The second argument (`'N-ZA-Mn-za-m'`) is the replacement set. For a ROT13 cipher, you're shifting each letter by 13 places. The alphabet is 26 letters long, so shifting by      13 splits it in half. The first half (`A-M` and `a-m`) becomes the second half (`N-Z` and `n-z`), and the second half becomes the first. So, `A` becomes `N`, `B` becomes `O`,    and so on, until `M` becomes `Z`. Then the sequence wraps around, so `N` becomes `A`, `O` becomes `B`, and so on.

[![asciicast](https://asciinema.org/a/742087.svg)](https://asciinema.org/a/742087)

**Key Takeaway:** Use `man` command to learn more about `tr`. Learn more about types of encoded data.

**Commands Used:**
`ls`
`cat`
`tr <options> <string1> <string2>`
---

# Level 12 -> 13

**Challenge:** The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

**Methodology:**
1.  Logged in as `bandit11` using the password we got from the last time.
2.  Used the `ls` command to list the files in the current directory. Found the `data.txt` file.
3.  Used `file` to see if it's a normal reable file or not and used `wc` to estimate the content inside but we already know that it's hexdump file that has been compressed.
4.  Now let's make a tmp directory at `tmp/<your directory name>`. For me I do `mkdir /tmp/longinus`
5.  Then we `cp data.txt` to that directory `cp data.txt /tmp/longinus/` then we `cd /tmp/logninus`
6.  Before we start decompressing we have to reverse the hexdump file to a binary file first by doing `xxd -r data.txt > data1.bin`
7.  Next we `file` to see what type of compression it is.
8.  We know that it's `gzip` so the command for decompressing is `gunzip` but we have to rename the extension to match the type of file that we found from `file` first. So we do `mv data1.bin data1.gz`
9.  Let's decompress `gunzip data.gzip` then we `ls` and `file` to see what's the next compression type is and `mv` to rename the extension to match it.
10. Then repeated the process. That's is pretty much all it is. In this level we learn about compression types here are the commands and types in this level:

    `gzip` -> `gunzip <file>` or `gzip -d <file>` file extension: `.gz`
    
    `bzip2` -> `bunzip2 <file>` or `bzip2 -d <file>` file extension: `.bz`
    
    `tar` -> `tar -xf <file>` file extension: `.tar`
    
    -x: This flag means extract — it tells tar you want to extract files from an archive.

    -f: This flag means file — it tells tar that the next argument is the name of the archive file you want to work with.
11. The finally file type is `ASCII text` let's just `cat` it

[![asciicast](https://asciinema.org/a/742092.svg)](https://asciinema.org/a/742092)

**Key Takeaway:** Review this level commands.

**Commands Used:**
`ls`
`cat`
`mkdir`
`cp`
`mv`
`file`
`gzip`
`bzip2`
`tar`
---

# Level 13 -> 14

**Challenge:** The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

**Methodology:**
1.  Logged in as `bandit13` using the password we got from the last time.
2.  Used the `ls` command to list the files in the current directory. Found the `sshkey.private` file.
3.  Used `file` to see what type of file it is.
4.  There are 4 ways I can do think of. 1.copy the content manaully 2. use `scp` command 3. use `telnet` command 4. use `nc` command. I don't know much about `telnet` and `nc` so I will only show first two ways.
5.  First, we copy the content inside to a new file in our local machine that has the same name as the original file.
6.  Or Second, we use command `scp` to copy a file from a remote host to our local host so that command look like this `scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ./`

    `scp` stands for secure copy; it works exactly the way the cp command does, but allows you to copy from one host over to another host on the same network. It works via ssh, so all your actions are using the same authentication and security as ssh.

    `scp username@remotehost.com:/remote/directory/myfile.txt /local/directory/`

7.  After i used `scp` command, I have to provide a password of a user again(Bandit13)
8.  After we got the file, we have to change the permission of the file first because in the video I forgot to change the permission of the file and the server respond back with `Permission 0640 for sshkey.private are too open. It is required that private key files are not accessible by others`. So we change permission by using `chmod` command. The command look like this `sudo chmod 700 sshkey.private`
9.  Then we use `ssh` to connect to bandit14 by using `-i <location>` flag to identify the sshkey file so we `ssh -i ./sshkey.private bandit14@bandit.labs.overthewire.org -p2220`
10.  We successfully login into Bandit14. and we can go grab the normal password at `/etc/bandit_pass/bandit14` if you want to.

[![asciicast](https://asciinema.org/a/742265.svg)](https://asciinema.org/a/742265)

**Key Takeaway:** Learn more about Permissions in Linux, `chmod` command, `scp` command.

**Commands Used:**
`ls -l`
`scp`
`chmod`
---

# Level 14 -> 15

**Challenge:** The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

**Methodology:**
1.  Logged in as `bandit14` using the sshkey we got from the last time.
2.  Used the `ls` command to list the files in the current directory. Found nothing then i remember that the last level said that the password is stored at `/etc/bandit_pass/bandit14`.
3.  Used `cd` to or just `cat` the `/etc/bandit_pass/bandit14`.
4.  So I think of `nc` because I've seen it somewhere on the internet so I do some `man nc` and tried lots of command.
5.  After a while i realize how to use `nc` so that command i used is `nc localhost 30000`.
6.  After I do that, I realize that I have to summit the password in order to get the next level password so I `Ctrl + Insert` to paste the password I got from `/etc/bandit_pass/bandit14`
7.  Then we got the password!

[![asciicast](https://asciinema.org/a/742708.svg)](https://asciinema.org/a/742708)

**Key Takeaway:** Learn more about `nc`.

**Commands Used:**
`ls`
`cat`
`nc [destination] [port]`
---
