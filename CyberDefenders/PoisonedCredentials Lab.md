# PoisonedCredentials Lab

**Category:** Network Forensics

**Scenario:** Your organization's security team has detected a surge in suspicious network activity. There are concerns that LLMNR (Link-Local Multicast Name Resolution) and NBT-NS (NetBIOS Name Service) poisoning attacks may be occurring within your network. These attacks are known for exploiting these protocols to intercept network traffic and potentially compromise user credentials. Your task is to investigate the network logs and examine captured network traffic.

**Tools:**
* Wireshark

> Q1: In the context of the incident described in the scenario, the attacker initiated their actions by taking advantage of benign network traffic from legitimate machines. Can you identify the specific mistyped query made by the machine with the IP address 192.168.232.162?

I looked up both **llmnr** and **nbns** in the filter as these pose huge risks to potential attacks. After searching, this is what I found:

<img width="3404" height="1510" alt="image" src="https://github.com/user-attachments/assets/ad47e0b0-e181-42e1-abfb-3122829e13fc" />

You can see the query 
