# SpookyPass
### *CHALLENGE DESCRIPTION*

All the coolest ghosts in town are going to a Haunted Houseparty - can you prove you deserve to get in?

## CATEGORY
Reversing

## Steps
1. First download the zip file and unzip it using the provided password.
2. I use `file` and `wc` to estimate the file and realize the most of the content is `binary` and know that it is `executable`
3. So I try to execute it by `sudo ./pass` and it require the password which I don't know.
    ```bash
    Welcome to the SPOOKIEST party of the year.
    Before we let you in, you'll need to give us the password:
    ```
    
5. Then I used `strings` to see if there is any readable strings in this file or not.
6. And the result come back something like this:

  ```bash
  Welcome to the 
  [1;3mSPOOKIEST
  [0m party of the year.
  Before we let you in, you'll need to give us the password: 
  s3cr3t_p455_f0r_gh05t5_4nd_gh0ul5
  Welcome inside!
  You're not a real ghost; clear off!
  ```
7. Noticing the `s3cr3t` line and I think that's the password. I copied it and paste it when I do `sudo ./pass`
8. And the Flag show up!
