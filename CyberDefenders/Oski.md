# Oski

My first step for this lab is to take the hash from the file provided and search for it in VirusTotal.

<img width="2231" height="861" alt="image" src="https://github.com/user-attachments/assets/053f07f3-4048-4502-8a0f-c57bc50dbcd2" />

# Questions
> Q1: Determining the creation time of the malware can provide insights into its origin. What was the time of malware creation?

<img width="2019" height="1134" alt="image" src="https://github.com/user-attachments/assets/8170ac39-97b3-4ab7-8398-45f5fc55e7e8" />

I can see in the details section that there are some dates related to the history of the file. The creation date is listed right on the page.

<details>
  <summary>Answer</summary>

   ```
   2022-09-28 17:40
   ```

</details>

> Q2: Identifying the command and control (C2) server that the malware communicates with can help trace back to the attacker. Which C2 server does the malware in the PPT file communicate with?

Looking in the Relations section, I can see there are two contacted URLs, both of which were scanned by different security vendors as malicious. I did some research and the php link is likely the C2 endpoint because it’s a server-side script that can receive data from an infected machine and send back commands, enabling ongoing communication. The dll link is a shared library that allows applications to access common functions without having the code embedded within their own executable file. Also, looking at each URL, I can see the php link contains crowdsourced intelligence that this this URL steals botnet C2.

<img width="2085" height="1106" alt="image" src="https://github.com/user-attachments/assets/ee5052e2-bebe-4dc2-8450-e68886095d5e" />

<img width="2137" height="1110" alt="image" src="https://github.com/user-attachments/assets/e9de27ef-000d-4d9e-b6b9-d50e8e8335c8" />

<details>
  <summary>Answer</summary>

   ```
   	http://171.22.28.221/5c06c05b7b34e8e6.php
   ```

</details>

> Q3: Identifying the initial actions of the malware post-infection can provide insights into its primary objectives. What is the first library that the malware requests post-infection?

A lot of good info came from the behavior section so I spent most of my time looking through here. Since I was looking for a specific library that the malware requested, I looked at any file that could have some indication it was requesting a library. Looking around, I found a dll file under files dropped which means the malware created or wrote that file onto the system during execution.

<img width="1953" height="1110" alt="image" src="https://github.com/user-attachments/assets/2a991e11-2cbe-4d18-9de9-be734f24f35b" />

<details>
  <summary>Answer</summary>

   ```
   	sqlite3.dll
   ```

</details>

> Q4: By examining the provided Any.run report, what RC4 key is used by the malware to decrypt its base64-encoded string?

A link was provided to the report that had the RC4 key posted in the malware configuration.

<img width="1977" height="915" alt="image" src="https://github.com/user-attachments/assets/acda5dc7-7c29-4645-89d8-714e755b7322" />

<details>
  <summary>Answer</summary>

   ```
   	5329514621441247975720749009
   ```

</details>

> Q5: By examining the MITRE ATT&CK techniques displayed in the Any.run sandbox report, identify the main MITRE technique (not sub-techniques) the malware uses to steal the user’s password.

As soon as I opened the Any.run sandbox report, I saw a few different .exe files with VPN.exe being marked as 100/100 for malicious activity. I checked the MITRE ATT&CK techniques and looked under the Credential access tactic. I checked the Credentials from Password Stores and saw this threat was related to stealing credentials from web browsers.

<img width="2234" height="1111" alt="image" src="https://github.com/user-attachments/assets/517a7a17-002b-40dd-9715-e7aacf5e3080" />

<img width="2219" height="968" alt="image" src="https://github.com/user-attachments/assets/6cd082ef-4678-4b6b-be66-91f3f6119900" />

<details>
  <summary>Answer</summary>

   ```
   	T1555
   ```

</details>

> Q6: By examining the child processes displayed in the Any.run sandbox report, which directory does the malware target for the deletion of all DLL files?

After opening the sandbox report, we can see the parent process is **VPN.exe** and the child processes are **cmd.exe** and **timeout.exe**. After clicking on both of these processes, I can see cmd used for the cmd.exe process was **"C:\Windows\system32\cmd.exe" /c timeout /t 5 & del /f /q "C:\Users\admin\AppData\Local\Temp\VPN.exe" & del "C:\ProgramData\*.dll"" & exit** which I can see contains a delete command for files in the ProgramData directory.

<img width="2232" height="1099" alt="image" src="https://github.com/user-attachments/assets/df5112ae-2abc-47e0-b7f5-e95db8508900" />

<details>
  <summary>Answer</summary>

   ```
   	C:\ProgramData
   ```

</details>
