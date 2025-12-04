# WebStrike

**Category:** Network Forensics

**Scenario:** A suspicious file was identified on a company web server, raising alarms within the intranet. The Development team flagged the anomaly, suspecting potential malicious activity. To address the issue, the network team captured critical network traffic and prepared a PCAP file for review.
Your task is to analyze the provided PCAP file to uncover how the file appeared and determine the extent of any unauthorized activity.

**Tools:**
* Wireshark
* [ipgeolocation](https://ipgeolocation.io/)

# Questions
> Q1: Understanding the geographical origin of the attack aids in geo-blocking measures and threat intelligence analysis. What city did the attack originate from?

<img width="1476" height="861" alt="image" src="https://github.com/user-attachments/assets/0931ddd3-2896-442d-b4e1-b3baeb4b654c" />


After taking a look at the PCAP file, we can see that only 2 IP addresses were captured. 117.11.88.124 is probably the client (attacker) and 24.49.63.79 is the web server.

# IP in China
<img width="2050" height="1718" alt="image" src="https://github.com/user-attachments/assets/3385299b-35a4-466b-a243-fba356f93df0" />

# IP in US
<img width="2050" height="1718" alt="image" src="https://github.com/user-attachments/assets/428b1f49-a2f6-43a2-8f4c-42de5917b2ac" />

<details>
  <summary>Answer</summary>

   ```
   Tianjin
   ```

</details>

> Q2: Knowing the attacker's user-agent assists in creating robust filtering rules. What's the attacker's user agent?

<img width="798" height="317" alt="image" src="https://github.com/user-attachments/assets/2b157936-01fd-420d-8fde-6426cc75d1ec" />

Follow the HTTP stream or TCP stream of the HTTP traffic. Here you can find the user-agent of the attacker.

<details>
  <summary>Answer</summary>

   ```
   Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
   ```

</details>

> Q3: We need to identify if there were potential vulnerabilities exploited. What's the name of the malicious web shell uploaded?

<img width="784" height="666" alt="image" src="https://github.com/user-attachments/assets/b16a2ae8-d458-41c4-9c42-3ac0d9881ab9" />

After browsing the website, the attacker found the upload page and sent a POST request to upload the php reverse shell to the server which was successful. It is important to check for packets sent with POST requests as these are commonly used for file uploads. You can also filter with **http.request.method == POST** to check for packets that were only sent using a POST request.

<details>
  <summary>Answer</summary>

   ```
   image.jpg.php
   ```

</details>

> Q4: Knowing the directory where files uploaded are stored is important for reinforcing defenses against unauthorized access. Which directory is used by the website to store the uploaded files?

<img width="861" height="668" alt="image" src="https://github.com/user-attachments/assets/f508c69d-2902-4fd3-910f-737e5e0ce258" />

The php reverse shell was uploaded to this directory as a link

<details>
  <summary>Answer</summary>

   ```
   /reviews/uploads/
   ```

</details>

> Q5: Identifying the port utilized by the web shell helps improve firewall configurations for blocking unauthorized outbound traffic. What port was used by the malicious web shell?

Look at the content of the php reverse shell 

<img width="1496" height="322" alt="image" src="https://github.com/user-attachments/assets/4f374199-51ff-4ca5-81ad-1d8a9050651c" />

<details>
  <summary>Answer</summary>

   ```
   8080
   ```

</details>

> Q6: Understanding the value of compromised data assists in prioritizing incident response actions. What file was the attacker trying to exfiltrate?

<img width="717" height="653" alt="image" src="https://github.com/user-attachments/assets/9c707bf4-05c3-4b51-915d-7f705622a52c" />

<details>
  <summary>Answer</summary>

   ```
   passwd
   ```

</details>

**Takeaway:** 
This forensics lab was a great way to get some hands-on experience, teaching me how to pick apart a packet capture to figure out exactly how this web server got compromised. By using Wireshark and ipgeolocation, I was able to track down where the attack came from and identify the hacker by checking their HTTP traffic. Filtering the network stream for POST requests made it easy to find the malicious file upload that planted the web shell, which let me find its filename and the vulnerable directory it landed in. I finished up by digging into the shell's code to figure out the unauthorized port it was using for C2 communication and identifying the sensitive file the attacker was trying to steal, collecting all the key clues needed to fix the system.
