# Yellow Rat Lab

**Category:** Threat Intel

**Scenario:** During a regular IT security check at GlobalTech Industries, abnormal network traffic was detected from multiple workstations. Upon initial investigation, it was discovered that certain employees' search queries were being redirected to unfamiliar websites. This discovery raised concerns and prompted a more thorough investigation. Your task is to investigate this incident and gather as much information as possible.

**Tools:**
* VirusTotal

# Questions

> Q1: Understanding the adversary helps defend against attacks. What is the name of the malware family that causes abnormal network traffic?

<img width="3040" height="1832" alt="image" src="https://github.com/user-attachments/assets/86af0b05-dc63-460c-bfda-363a3f23f336" />

This challenge gave us the file hash of malware so we can start by searching it on VirusTotal which we can see that popular threat label of this file does not match the answer format but at least we know that this is Jupyter Infostealer

And we could go to the "Community" tab to find out the answer since there are so many community comments on this file.




<img width="441" height="132" alt="Screenshot 2025-12-02 at 8 38 48 PM" src="https://github.com/user-attachments/assets/ae99ceda-d7d5-43c1-afc9-935d430d2c1a" />

After scrolling for a bit, we now have the name and also reference links to do our own research.

<details>
  <summary>Answer</summary>

   ```
   Yellow Cockatoo RAT
   ```

</details>

> Q2: As part of our incident response, knowing common filenames the malware uses can help scan other workstations for potential infection. What is the common filename associated with the malware discovered on our workstations?

<img width="2926" height="1834" alt="image" src="https://github.com/user-attachments/assets/b61cde23-3d6d-42be-a139-b98eb23b5570" />

Take a look at file name again, it already matches answer format of this question

<img width="784" height="311" alt="image" src="https://github.com/user-attachments/assets/30bd1119-fcf0-42fc-a0d6-cbdad808d908" />

We can go to "Names" section in "Details" tab to see other names of this file but there is still only 1 that matches answer format.


<details>
  <summary>Answer</summary>

   ```
   111bc461-1ca8-43c6-97ed-911e0e69fdf8.dll
   ```

</details>

> Q3: Determining the compilation timestamp of malware can reveal insights into its development and deployment timeline. What is the compilation timestamp of the malware that infected our network?

<img width="1190" height="646" alt="image" src="https://github.com/user-attachments/assets/ef60dd8d-a753-4067-9936-705584842d81" />

PE files often contain their complication timestamp in their PE header so if we scroll down to "Portable Executable Info" we will then have the complication timestamp of this file

> Q4: Understanding when the broader cybersecurity community first identified the malware could help determine how long the malware might have been in the environment before detection. When was the malware first submitted to VirusTotal?

<img width="569" height="222" alt="image" src="https://github.com/user-attachments/assets/77b77f31-373a-425f-9317-b5cef5be15db" />

Going up to the "History" section, we can see that someone submitted this file to VirusTotal almost a month later after it was compiled.

<details>
  <summary>Answer</summary>

   ```
   2020-10-15 02:47:37
   ```

</details>

> Q5: To completely eradicate the threat from Industries' systems, we need to identify all components dropped by the malware. What is the file name dropped by the malware in the Appdata folder?

<img width="631" height="646" alt="image" src="https://github.com/user-attachments/assets/8ab40162-0a54-41a9-ac4e-753a716871b6" />

We need to change our intel source since VirusTotal did not catch the file dropped by this malware.

<img width="899" height="768" alt="image" src="https://github.com/user-attachments/assets/bb30b086-cd1c-4a64-9bbe-61f9dd81d118" />

We still have threat intel report from Red Canary that already conducted malware analysis for us and here is the file that dropped in Appdata folder


 
