# PsExec Hunt

Category: Network Forensics

An alert from the Intrusion Detection System (IDS) flagged suspicious lateral movement activity involving PsExec. This indicates potential unauthorized access and movement across the network. As a SOC Analyst, your task is to investigate the provided PCAP file to trace the attacker’s activities. Identify their entry point, the machines targeted, the extent of the breach, and any critical indicators that reveal their tactics and objectives within the compromised environment.

Tools: Wireshark

> Q1: To effectively trace the attacker's activities within our network, can you identify the IP address of the machine from which the attacker initially gained access?

Looking in Wireshark, I wanted to identify a packet that contained some sort of suspicious information. With just a bit of scrolling, I found a packet with the following info: **1514 Write Request Len: 65536 Off: 0, File: PSEXESVC.exe**. A SMB2 write request is a network operation where a client tells a server, "write these bytes into this file at this location". However, this specific packet, a SMB2 write request involving a PowerShell file likely means a system is remotely transferring a script or executable to another machine via SMB.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/5fc62761-8d5a-4d1a-80e9-9712af873c04" />

<details>
  <summary>Answer</summary>

   ```
   10.0.0.130
   ```

</details>

> Q2: To fully understand the extent of the breach, can you determine the machine's hostname to which the attacker first pivoted?

This one took me some time to find the hostname that was targeted but I found it. Essentially, I used the filter **ntlmssp.challenge.target_name** to find the challenge pakcet. Through digging in the packet's details, I found the hostname was listed underneath the NTLM Secure Service Provider.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/16fe331c-2551-4185-b118-bd9bde28d47b" />

<details>
  <summary>Answer</summary>

   ```
   Sales-pc
   ```

</details>

> Q3: Knowing the username of the account the attacker used for authentication will give us insights into the extent of the breach. What is the username utilized by the attacker for authentication?

Similarly to the previous question, I applied the filter **ntlmssp.auth.username** which highlights the account name submitted during authentication. After scrolling down in the packet details, I found the username.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/d725204c-febc-4fdf-92d9-619f30591c68" />

<details>
  <summary>Answer</summary>

   ```
   ssales
   ```

</details>

> Q4: After figuring out how the attacker moved within our network, we need to know what they did on the target machine. What's the name of the service executable the attacker set up on the target?

Given the name of the lab and some of the packets I found earlier in the lab that contained details on **PSEXESVC.exe**, I knew this was the service executable that the attacker had set up.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/a2082dfe-4840-4e69-a116-d46bc6d59918" />

<details>
  <summary>Answer</summary>

   ```
   PSEXESVC.exe
   ```

</details>

> Q5: We need to know how the attacker installed the service on the compromised machine to understand the attacker's lateral movement tactics. This can help identify other affected systems. Which network share was used by PsExec to install the service on the target machine?

In the same place, I found the network share in the hostname. This was for the .exe file.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/137217b1-41ee-4421-b5b0-474ca00e6393" />

<details>
  <summary>Answer</summary>

   ```
   ADMIN$
   ```

</details>

> Q6: We must identify the network share used to communicate between the two machines. Which network share did PsExec use for communication?

In the same place, I found the network share used for comms between the two machines. This was not the executable file however.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/1a448134-edef-4746-bec7-70a0016c5795" />

<details>
  <summary>Answer</summary>

   ```
   IPC$
   ```

</details>

> Q7: Now that we have a clearer picture of the attacker's activities on the compromised machine, it's important to identify any further lateral movement. What is the hostname of the second machine the attacker targeted to pivot within our network?

Similarly to how I found the first computer's name that was targeted, I set the filter **ntlmssp.challenge.target_name** and checked a packet that came from the IP **10.0.0.131** which was the other machine targeted by the attacker. I then checked the NTLM Secure Service Provider an found the name.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/be13cc60-6e69-4884-b9a7-e8950f7b665a" />

<details>
  <summary>Answer</summary>

   ```
   MARKETING-PC
   ```

</details>
