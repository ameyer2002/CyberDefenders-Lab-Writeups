# Investigating Windows TryHackMe

> Q1: Whats the version and year of the windows machine? 

This one is quite simple. Once opening up the lab, we'll want to use PowerShell and the command **systeminfo** which will give us the answer.

<img width="1884" height="927" alt="image" src="https://github.com/user-attachments/assets/096a6055-36f6-4453-978f-0d3434e2c6ee" />

<details>
  <summary>Answer</summary>

   ```
   Windows Server 2016
   ```

</details>

> Q2: Which user logged in last?

What we can do here is search for the users in the system with the command **net user**. We can then search for a specific user's last login by doing **net user username**. I will search for all 5 users and see which account had the most recent login which appears to be **Administrator**.

<img width="1885" height="917" alt="image" src="https://github.com/user-attachments/assets/af5ac6b9-aaa6-4541-99e4-b50fa909277a" />

<details>
  <summary>Answer</summary>

   ```
   Administrator
   ```

</details>

> Q3: When did John log onto the system last?

Similar to the last question, I can use the **net user John** command in PowerShell to check John's last login.

<img width="1887" height="925" alt="image" src="https://github.com/user-attachments/assets/61a5e204-ce13-4c77-85e7-d22845d697b4" />

<details>
  <summary>Answer</summary>

   ```
   03/02/2019 5:48:32 PM
   ```

</details>

> Q4: What IP does the system connect to when it first starts?

We can run the command **Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Run"** which reads startup programs registered for all users. Get-ItemProperty retrieves the values stored in this registry key. In the UpdateSvc, I can see the IP address is listed.

<img width="1904" height="920" alt="image" src="https://github.com/user-attachments/assets/5e928085-fc45-4ecd-9a88-137f8e8b8d6c" />

<details>
  <summary>Answer</summary>

   ```
   10.34.2.3
   ```

</details>

> Q5: What two accounts had administrative privileges (other than the Administrator user)?

To find which users have adminitrative privileges, I can run the command **net localgroup Administrators**.

<img width="1881" height="874" alt="image" src="https://github.com/user-attachments/assets/5b44262d-fc97-4575-a296-01ad44d209ab" />

<details>
  <summary>Answer</summary>

   ```
   Guest, Jenny
   ```

</details>

> Q6: Whats the name of the scheduled task that is malicous?

To find this, I can open up Task Scheduler and go into the library. I am seeing some of the tasks didn't run because the admin refused the request. I think of the 2 reuqests that were refused, the **Clean file system** looks the most suspicious. I also went to the actions of this request and saw **C:\TMP\nc.ps1 -I 1348**. 


<img width="1875" height="876" alt="image" src="https://github.com/user-attachments/assets/ab1ad7a3-f995-401f-9bed-dbea19bdae9d" />

<details>
  <summary>Answer</summary>

   ```
   Clean file system
   ```

</details>

> Q7: What file was the task trying to run daily?

When viewing the actions for this request, I can see the path, **C:\TMP\nc.ps1 -I 1348** leads to a file.

<img width="1872" height="857" alt="image" src="https://github.com/user-attachments/assets/d66c3160-de3b-4985-a01a-7e6f209bb22c" />

<details>
  <summary>Answer</summary>

   ```
   nc.ps1
   ```

</details>

> Q8: What port did this file listen locally for?

Still in the actions of this request, I can see the port is listed under the details.

<img width="1872" height="857" alt="image" src="https://github.com/user-attachments/assets/d66c3160-de3b-4985-a01a-7e6f209bb22c" />

<details>
  <summary>Answer</summary>

   ```
   1348
   ```

</details>

> Q9: When did Jenny last logon?

I can open up PowerShell and run the command **net user Jenny** to see her last login which looks like she's never logged in.

<img width="1903" height="875" alt="image" src="https://github.com/user-attachments/assets/19e5f6e5-0d1f-442b-b905-5fe9275adbc1" />

<details>
  <summary>Answer</summary>

   ```
   Never
   ```

</details>

> Q10: At what date did the compromise take place?

I wanted to check the C: Drive for any extra potential folders which I found a TMP folder. I went in there and saw all files were modified on the same date which tells me this is when the compromise took place.

<img width="1856" height="909" alt="image" src="https://github.com/user-attachments/assets/2cd50a9a-5c25-4cd1-9b4e-ab7365415309" />

<details>
  <summary>Answer</summary>

   ```
   03/02/2019
   ```

</details>

> Q11: During the compromise, at what time did Windows first assign special privileges to a new logon?

My filtering isn't working but what I would do here is go to Event Viewer, Windows Logs, and Security. I would then set a filter for the time range to be between 03/02/2019 12:00:00 AM - 03/02/2019 11:59:59 PM to check all the logs on this day. I would also set the Event ID to 4672 which means: Special privileges assigned to new logon. https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4672

<details>
  <summary>Answer</summary>

   ```
   03/02/2019 4:04:49 PM
   ```

</details>

> Q12: What tool was used to get Windows passwords?

Going back to the TMP directory, I wanted to see if there were any other suspicious files in here that would tell us which tool the attacker was using to gather passwords. I saw a file called **mim-out** which I opened up to see what this was and I can tell it's a credential dumping tool.

<img width="1910" height="877" alt="image" src="https://github.com/user-attachments/assets/0ff01acc-aad0-4d78-87ff-2c152f9b4932" />

<details>
  <summary>Answer</summary>

   ```
   Mimikatz
   ```

</details>

> Q13: What was the attackers external control and command servers IP?

I took a look at the hosts file which is located at “C:\Windows\System32\drivers\etc”. This file serves as a local DNS allowing the local machine to map hostnames to IP addresses. Looking at the file, “google.com” definitely does not use the IP address it was assigned to.

<img width="1910" height="873" alt="image" src="https://github.com/user-attachments/assets/fa83333b-3097-4a4e-ae9c-85c4f74a8a9d" />

<details>
  <summary>Answer</summary>

   ```
   76.32.97.132
   ```

</details>

> Q14: What was the extension name of the shell uploaded via the servers website?

 I went to the “C:\inetpub” directory which is the location of web server log files for Microsoft Internet Information Services, which is the common web server for Windows. In it, there is another folder called **wwwroot**. I can see 2 files with a **.jsp** extension.

<img width="1899" height="877" alt="image" src="https://github.com/user-attachments/assets/b204cdad-5b32-44c8-9bea-0a32b06b1482" />

I will open PowerShell and change to this directory with **C:\inetpub\wwwroot**. I can then run **Get-Content .\tests.jsp** which will display the contents of the file. 

<img width="1857" height="849" alt="image" src="https://github.com/user-attachments/assets/edc59047-4193-4d46-b600-7f1747db4d0d" />

<details>
  <summary>Answer</summary>

   ```
   .jsp
   ```

</details>

> Q15: What was the last port the attacker opened?

To check this, I can go to **Windows Firewall with Advanced Security** and check the Inbound Rules. Right away, I can see the first rule at the top is **Allow outside connections for development** which is essentially a rule to allow external users to connect to the local machine which is very dangerous. After clicking on the properties of this rule, I can see the local port.

<img width="1900" height="878" alt="image" src="https://github.com/user-attachments/assets/1df8f686-ced1-4017-9810-aae9540811a0" />

<details>
  <summary>Answer</summary>

   ```
   1337
   ```

</details>

> Q16: Check for DNS poisoning, what site was targeted?

Earlier when I opened the hosts file, I saw the IP address for google.com was definitely not google's IP which tells me the attacker was spoofing the domain to redirect users to 76.32.97.132.

<img width="1910" height="873" alt="image" src="https://github.com/user-attachments/assets/fa83333b-3097-4a4e-ae9c-85c4f74a8a9d" />

<details>
  <summary>Answer</summary>

   ```
   google.com
   ```

</details>
