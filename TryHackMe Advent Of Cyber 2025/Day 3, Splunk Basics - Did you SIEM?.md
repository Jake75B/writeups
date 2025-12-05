

Day 3 teaches us how to ingest and parse custom log data using Splunk.

---

1. What is the attacker IP found attacking and compromising the web server?

**Solution**

Using the command `index=main sourcetype=web_traffic | timechart span=1d count | sort by count | reverse` then clicking on the `client_ip` field in the sidebar will reveal this. The IP **198.51.100.55** is responsible for an overwhelming number of connections to the web server so it must be the attacker's IP.

**Output**

![](AdventOfCyber%20Attatchments/Day%203,%20Splunk%20Basics%20-%20Did%20you%20SIEM?-05.12.25-paste.png)


--- 

2. Which day was the peak traffic in the logs? (Format: YYYY-MM-DD)

**Solution**

Using the query: `index=main sourcetype=web_traffic | timechart span=1d count | sort by count | reverse` , we can sort the web traffic by count to see that **2025-10-12** had the most traffic.

**Output**

![](AdventOfCyber%20Attatchments/Day%203,%20Splunk%20Basics%20-%20Did%20you%20SIEM?-05.12.25-paste-1.png)


---

3. What is the count of Havij user_agent events found in the logs?

**Solution**

Navigating to the `user_agent` field we can see that 'havij' has a count of 993.

**Output**

![](AdventOfCyber%20Attatchments/Day%203,%20Splunk%20Basics%20-%20Did%20you%20SIEM?-05.12.25-paste-2.png)


---

4. How many path traversal attempts to access sensitive files on the server were observed?
   
**Solution**

`sourcetype=web_traffic client_ip="198.51.100.55" AND path="*..\/..\/*" OR path="*redirect*" | stats count by path` shows us the number of path traversal attempts

**Output**

![](AdventOfCyber%20Attatchments/Day%203,%20Splunk%20Basics%20-%20Did%20you%20SIEM?-05.12.25-paste-3.png)

---

5. Examine the firewall logs. How many bytes were transferred to the C2 server IP from the compromised web server?

**Solution**

Using the command `sourcetype=web_traffic client_ip="198.51.100.55" AND action="ALLOWED" | stats sum(bytes_transferred) by src_ip` tells us the answer to this.

**Output**

![](AdventOfCyber%20Attatchments/Day%203,%20Splunk%20Basics%20-%20Did%20you%20SIEM?-05.12.25-paste-4.png)

