# OverTheWire Bandit Levels 0-10

**Goal:** Solve the first 10 levels of the OverTheWire Bandit wargame to practice fundamental Linux commands.

---

## Level 0 -> 1

**Challenge:** The password for the next level is in a file called `readme` in the home directory.

**Methodology:**
1.  Logged in as `bandit0` using the provided password.
2.  Used `pwd` to print current directory path.
3.  Used the `ls` command to list the files in the current directory with `-l` flag to long listing format.
4.  Found the `readme` file.
5.  Used `file` to detetrmine the file type
6.  Used the `cat` command to read the contents of the `readme` file.
7.  Copied the password and used it to log in to the next level.

[![asciicast](https://asciinema.org/a/6JgAIb20gnx1t2wWjn27kfEk1.svg)](https://asciinema.org/a/6JgAIb20gnx1t2wWjn27kfEk1)

**Commands Used:**
`pwd`
`ls`
`file`
`cat`
---

## Level 1 -> 2

**Challenge:** The password for the next level is stored in a file called - located in the home directory

**Methodology:**
1.  Logged in as `bandit1` using the password we got from the last time.
2.  Used `pwd` to print current directory path.
3.  Used the `ls` command to list the files in the current directory.
4.  Found the `-` file.
5.  Used `file` to detetrmine the file type
6.  !The problem with this is our terminal interprets the HYPHEN as flags.
7.  !Instead of specifying the name of the file, we specify the path to the file, which are Absolute path or Relative path.
8.  Used the `cat` command to read the contents of the `-` file by `cat ./-`.

[![asciicast](https://asciinema.org/a/YEoDfLj1H4YgcSE3VlmVLVwOV.svg)](https://asciinema.org/a/YEoDfLj1H4YgcSE3VlmVLVwOV)

**Commands Used:**
`pwd`
`ls`
`file`
`cat`
---
