# Lespion Lab

**Category:** Threat Intel

**Scenario:** You have been tasked by a client whose network was compromised and brought offline to investigate the incident and determine the attacker's identity.
Incident responders and digital forensic investigators are currently on the scene and have conducted a preliminary investigation. Their findings show that the attack originated from a single user account, probably, an insider. Investigate the incident, find the insider, and uncover the attack actions.

**Tools:**
* Google Maps
* Google Image Search
* Sherlock

> Q1: File -> Github.txt: What API key did the insider add to his GitHub repositories?

<img width="365" height="184" alt="image" src="https://github.com/user-attachments/assets/37d3873b-baf2-41fa-8ac4-bb5357dfa0db" />

We're provided with these 3 files: 1 txt file, 1 jpg file, and 1 png file. Open up the Github file and paste the link in a new browser.

<img width="1412" height="763" alt="image" src="https://github.com/user-attachments/assets/014c8869-bd0a-44ba-8b91-b0d397f893e4" />

Most of the repos were forked but there was one project that was created which is [Project-Build---Custom-Login-Page](https://github.com/EMarseille99/Project-Build---Custom-Login-Page).

<img width="1288" height="617" alt="image" src="https://github.com/user-attachments/assets/e535e57d-e695-462d-88ff-0c511ed44206" />

<img width="1288" height="346" alt="image" src="https://github.com/user-attachments/assets/cde1b7d7-00ad-44d8-8165-1cd37f59cc15" />

After reviewing **fsociety.js**, I took a look at **Login Page.js**.

<img width="830" height="612" alt="image" src="https://github.com/user-attachments/assets/b80df508-9d66-4493-bea5-f64d55e373fd" />

You can see the API key is set on the first line.

<details>
  <summary>Answer</summary>

   ```
   aJFRaLHjMXvYZgLPwiJkroYLGRkNBW
   ```

</details>

> Q2: File -> Github.txt: What is the plaintext password the insider added to his GitHub repositories?
