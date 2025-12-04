

Day two teaches us how to use the Social-Engineer Toolkit to send phishing emails

---

1. What is the password used to access the TBFC portal?

**solution**

First we run a listener script that will listen for all incoming credentials on the network. Next, by following the steps in the room, we use Social-Engineer Toolkit (SET) to create a phishing email to send. Then we wait for the listener script to pick up something.

![](AdventOfCyber%20Attatchments/Day%202,%20Phishing%20-%20Merry%20Clickmas-04.12.25-paste-3.png)

**Output**

![](AdventOfCyber%20Attatchments/Day%202,%20Phishing%20-%20Merry%20Clickmas-04.12.25-paste.png)


---

2. Browse to `http://10.82.161.77` from within the AttackBox and try to access the mailbox of the `factory` user to see if the previously harvested `admin` password has been reused on the email portal. What is the total number of toys expected for delivery?

**Solution**

Browsing to the IP using a browser, we can use the admin's password from the previous exercise to get into the account: unranked-wisdom-anthem. 
<br>
<br>


![](AdventOfCyber%20Attatchments/Day%202,%20Phishing%20-%20Merry%20Clickmas-04.12.25-paste-4.png)
<br>
<br>
Once we are in, we can see the phishing email we used SEtoolKit to send.
<br>
<br>

![](AdventOfCyber%20Attatchments/Day%202,%20Phishing%20-%20Merry%20Clickmas-04.12.25-paste-2.png)

<br>
<br>

**Output**
<br>
<br>
clicking on the other email gives us the answer: 1984000 toys
<br>
<br>


![](AdventOfCyber%20Attatchments/Day%202,%20Phishing%20-%20Merry%20Clickmas-04.12.25-paste-5.png)



