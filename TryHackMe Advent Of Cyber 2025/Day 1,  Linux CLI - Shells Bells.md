

Day one of the Advent of Cyber (AOC) involves some basic linux CLI usage. 

---

1. Which CLI command would you use to list a directory?

- We use `LS`to list a directory

---

2. Identify the flag inside of McSkidy's guide

**Solution**

Using `LS` we can see the guide's directory in McSkidy's directory. We can then `CD` into it. Upon using `LS` in the **Guides** directory, nothing appears, this means whatever we are looking for is hidden. adding an `-a` argument to LS will show all hidden files which shows the file containing the flag.

**Output**

![](AdventOfCyber%20Attatchments/Solutions-04.12.25-paste.png)

---

3. Which command helped you filter the logs for failed logins?

- We use`grep` to help filter the log for failed logins

---

4. Identify the flag inside the Eggstrike script

**Solution**

Using the information we have, we know that the eggstrike shell script is located in the `/socmas/2025` directory. By reading the script we can see the flag.

**Output**

![](AdventOfCyber%20Attatchments/Solutions-04.12.25-paste-2.png)

--- 

5. Which command would you run to switch to the root user?

- We use `sudo su` for this

--- 

6.  Finally, what flag did Sir Carrotbane leave in the root bash history?

**Solution**

   Using the `history` command we can view the history to find the flag

**Output**

![](AdventOfCyber%20Attatchments/Solutions-04.12.25-paste-1.png)

---

7. For those who consider themself intermediate and want another challenge, check McSkidy's hidden note in /home/mcskidy/Documents/ to get access to the key for Side Quest 1! 





