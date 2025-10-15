
0. The goal of this level is for you to log into the game using `SSH`. The host to which you need to connect is **bandit.labs.overthewire.org**, on port **2220**. The username is **bandit0** and the password is **bandit0**. 

**Solution:**

By SSH'ing into the first game room using the provided username bandit0 and password bandit0, we are granted access.

**Output:**

The image below should show
![](Pasted%20image%2020251015184937.png)



![[Pasted image 20251015170242.png]]
This room automatically puts us into room 1 after logging in.

---
0. The password for the next level is stored in a file called readme located in the home directory.

**Solution:**

By typing the`ls`command, we can see one file in our directory named "readme". We can use cat to read the contents of this file.

**Output:**

![[Pasted image 20251015171657.png]]

--- 

2. 

---
8. The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once.

**Solution:**

`` sort data.txt | uniq -u

sort: sort in lexicographical order
" | " , "piping": takes output of command on left and uses as input on right
uniq: removes extra duplicates and keeps a copy
uniq -u: keeps only lines that occur once originally

**Output:**

![[Pasted image 20250828163404.png]]

--- 

9. The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

**Solution:**

`grep "===" data.txt -a`

- grep, search using regex
- -a , treat file as text 

**Output:**

As you can see, the password for the next room is split between the last and second last line.

![[Pasted image 20250828163149.png]]

---

10. The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

**Solution**

- As we can see, when using `cat` on data.txt, the base64 encoded data is shown. 
- We can decode this using the `base64` command in `--decode mode` using `<<<` to pass the base64 straight in.

**Output**

![[Pasted image 20250828164905.png|800]]

--- 

11. The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

**Solution**

The password is contained within this caesar cipher: 
`"Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4"` 
requiring a rotation by 13 positions. To get around this, we can use the `tr` (translate) command.

`tr 'A-Za-z' 'N-ZA-Mn-za-m' <<< " Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4"`

`'A-Za-z'` take all uppercase and lower case
 `'N-ZA-Mn-za-m'` uppercase and lower case shift the alphabet by 13 places

**Output**

![[Pasted image 20250902003124.png|500]]

![[Pasted image 20250902003104.png]]

--- 
12. The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

**Solution** 

As this task requires the creation of new files, we need a temporary directory to store them so we use `"mktemp -d"` and then copy the hexdump to the new directory.

![[Pasted image 20250908134145.png]]

Knowing that `data.txt` is a hexdump, we can use `xxd -r` on the hexdump to reverse it's contents back into the original binary. Doing that we get this which isn't the answer.

![[Pasted image 20250908134305.png|600]]

 The question gives us a clue that the hexdump was compressed, so by checking the file type, we can see the compression tool used on it which was `gzip`
 
![[Pasted image 20250908134559.png]]

In order to decompress the gzip, we need to add `.gz` to reversed_hex using `mv` so that the gzip tool is able to decompress it. Note that adding a file extension is only necessary for .gz archives.

![[Pasted image 20250908134815.png]]

Now we decompress it using the `-d` flag. Upon doing this and checking the file type, we discover the file is still compressed by a different compression tool (`bzip2`).

![[Pasted image 20250908135012.png]]

Decompressing using bzip2 and using file shows it's further compressed using gzip.

![[Pasted image 20250908135221.png|700]]

Decompressing further...

![[Pasted image 20250908135453.png]]

The next compression software used is `tar` so we use `"tar -xvf"` to decompress the file which produces `data5.bin` this time.
`"-x"` Decompresses
`"-v"` List files extracted from archive
`"-f"` Specify the filename to be decompressed (reversed_hex)

![[Pasted image 20250908140305.png]]
The next decompress cycle requires tar once again, then bzip2, tar, gzip in that order. 

The final decompression produces an ASCII text file containing the password to the next level...

**Output**

![[Pasted image 20250908140551.png]]


--- 

13. The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note:** **localhost** is a hostname that refers to the machine you are working on

**solution**

Since the bandit14 file in banditpass can only be accessed by the bandit14 user, our objective is to log in as that account. We are provided with an SSH private key for authentication, so the first step is to find the key's path so that it can be inputted into the bandit14 ssh command.

![[Pasted image 20250908141311.png]]

Taking the file path, we can use the command below to ssh in as bandit14. 

`**bandit13@bandit**:**~**$ ssh -p 2220  -i '/home/bandit13/sshkey.private' bandit14@bandit.labs.overthewire.org`

Once in, we cd to /etc/bandit_pass to `cat` bandit14 to find the password.

**Output**

![[Pasted image 20250908141924.png]]

--- 

14.

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

**Solution**

Using `netcat`, we can send a message containing the current level’s password to port 30000 on `localhost` , which will return the password for the next level.

**Output**

![[Pasted image 20250910013612.png]]

--- 

15. The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

**Solution**

This task requires us to send the current level’s password to port 30001 on localhost, but unlike the previous challenge, the connection must use SSL/TLS encryption. `NC` does not support this so we have to use `openssl` 

**Solution**

![[Pasted image 20250910203345.png]] 

**Output**

![[Pasted image 20250910203427.png]] 

---

16. The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
