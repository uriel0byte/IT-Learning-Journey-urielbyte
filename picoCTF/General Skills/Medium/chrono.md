# Author: Mubarak Mikail

# Description
How to automate tasks to run at intervals on linux servers?

# Hints
1. None

# Steps
1. Click start an instance, connect to the remote server via ssh using the provided credentials.
2. Used id and sudo -l to check if I have root access or any sudo commands available. Realized that I don't.
3. Used crontab -l to see if there is any tasks running by our current user and there is none.
4. Then I used cat /etc/crontab to check system-wide cron schedule and there it is.

Answer: picoCTF{Sch3DUL7NG_T45K3_L1NUX_7754e199}
