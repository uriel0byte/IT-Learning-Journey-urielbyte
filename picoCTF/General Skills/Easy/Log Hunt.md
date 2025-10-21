# Author: Yahaya Meddy

# Description
Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag? Download the logs and figure out the full flag from the fragments.

# Hints
1.  You can use grep to filter only matching lines from the log.
2.  Some lines are duplicates; ignore extra occurrences.

# If you enjoy this kind of ctf, LabEx has more of this kind. Not Sponsered btw just love the website.


# Steps
1. Download the provided log file.
2. First check the file with "file <file>" and "wc <file>" to see the file's overall.
3. We see the flag is contained in the same line as "FLAGPART" word.
4. Used " cat server.log | grep -i "FLAGPART" | sort | uniq "
5. Rearrage the flag.

Answer: picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}
