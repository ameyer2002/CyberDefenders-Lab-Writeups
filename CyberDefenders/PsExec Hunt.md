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
