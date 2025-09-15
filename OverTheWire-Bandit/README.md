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
`find -name`
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
      **Breakdown of the Command**
    **`find`**: This is the main command used to search for files and directories within a file system.
    **`-type f`**: This option restricts the search to only **files** (not directories, links, or other special file types).
    **`-exec file {} +`**: This part executes the `file` command on all the files found by `find`.
       **`-exec`**: This is an action that runs a command on each file found.
       **`file {}`**: The `file` command determines the **type of a file** (e.g., "ASCII text," "JPEG image data," "shell script"). The `{}` is a placeholder that `find` replaces with the name of each file it finds.
       **`+`**: This is a more efficient way to use `-exec`. It bundles the filenames together and passes them to the `file` command in one go, rather than running the command for each file individually.
    **`|`**: This is a **pipe**. It takes the output of the command on the left (`find ... -exec file {} +`) and uses it as the input for the command on the right (`grep "text"`).
    **`grep "text"`**: This command filters the output from the `file` command, displaying only the lines that contain the string **"text"**. Since the `file` command often describes plain text files as "ASCII text" or "UTF-8 text," this effectively filters for files that are **text-based**.
     **In short,** the `find` command locates files of a specific size, and the `grep` command then filters that list to show only the ones that the system identifies as a text file.
4.  So the result are `-file00` and `-file07` but the `-file00`: It says `"Non-ISO extended-ASCII text"`, which means it has unusual or outdated character encoding. It might look like gibberish or be unreadable.
5.  Next we do what we always do `cat` it!
    

[![asciicast](https://asciinema.org/a/ZUOHfWa4qJxvmY3MTp5wUcXqB.svg)](https://asciinema.org/a/ZUOHfWa4qJxvmY3MTp5wUcXqB)

**Key Takeaway:**
**Learn more about encoding types**

**Commands Used:**
`pwd`
`ls -la`
`cat`
`file`
`grep`
`find -type`
---

