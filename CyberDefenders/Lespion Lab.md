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

<img width="614" height="396" alt="image" src="https://github.com/user-attachments/assets/9e467700-7deb-46c2-95c2-8b3d5893243b" />

Scroll to line 46~59, where the user's credentials can be found.

<img width="695" height="455" alt="image" src="https://github.com/user-attachments/assets/2da257b1-c474-4a2e-b324-f13b4969c6a2" />

You'll then want to use Cyberchef to decode the password

<details>
  <summary>Answer</summary>

   ```
   PicassoBaguette99
   ```

</details>

> Q3: File -> Github.txt: What cryptocurrency mining tool did the insider use?

Scroll down the user's repositories until you find one about crypto mining.

<img width="575" height="213" alt="image" src="https://github.com/user-attachments/assets/a784a953-1939-442f-a5d2-74e5a0d3a585" />


After reading the README.md, it is confirmed that this is the crypto mining tool that we're looking for.

<img width="911" height="487" alt="image" src="https://github.com/user-attachments/assets/51b6a6d0-affe-42d1-8edb-ab44b9792427" />

<details>
  <summary>Answer</summary>

   ```
   XMRig
   ```

</details>

> Q4: On which gaming website did the insider have an account?

To find the username EMarseille99 across different platforms, in the terminal, we can run the command: **sherlock EMarseille99**

This is what came up after this search:

<img width="1012" height="180" alt="image" src="https://github.com/user-attachments/assets/d86d136a-f027-45e1-be81-aa894d03a343" />


<details>
  <summary>Answer</summary>

   ```
   Steam
   ```

</details>

> Q5: What is the link to the insider Instagram profile?

By searching for EMarseille99, the first link that appears is to their instagram account.

<img width="3050" height="1832" alt="image" src="https://github.com/user-attachments/assets/c46b8b71-3569-4ec7-9f40-5ddea9955fbc" />

<img width="3050" height="1832" alt="image" src="https://github.com/user-attachments/assets/e846caf4-5916-4743-abda-a9f7c811f094" />

<details>
  <summary>Answer</summary>

   ```
   https://www.instagram.com/emarseille99/
   ```

</details>

> Q6: Which country did the insider visit on her holiday?

<img width="2954" height="1662" alt="image" src="https://github.com/user-attachments/assets/56f66346-587c-49ea-b631-faad51bf1bd2" />

After reading the caption of this post, I will then copy the image, open up another tab and search for Google. I'll use Google Lens and paste the image to see what comes up.

<img width="3054" height="1662" alt="image" src="https://github.com/user-attachments/assets/3d7eda6b-8c7c-4d71-a5c4-d7a0f042e805" />

We can see this a picture of the Marina Bay Sands Hotel in **Singapore**.

<details>
  <summary>Answer</summary>

   ```
   Singapore
   ```

</details>

> Q7: Which city does the insider family live in?

On her Instagram, there are two pictures that the user mentioned her family.


We can see in the post of the house, there is an UAE flag which means it'll be a city in this country. Using context clues is important.
<img width="3054" height="1662" alt="image" src="https://github.com/user-attachments/assets/3683ba34-e417-43f9-a6f5-ce862b142462" />

<img width="3054" height="1662" alt="image" src="https://github.com/user-attachments/assets/5abc0b3f-ceae-478b-be04-2884fb906d19" />

Again, I will copy the image, open up another tab and search for Google. I'll use Google Lens and paste the image to see what comes up.

<img width="3054" height="1662" alt="image" src="https://github.com/user-attachments/assets/ed13b337-b695-436b-bf7a-46775a6ebce1" />

<details>
  <summary>Answer</summary>

   ```
   Dubai
   ```

</details>

> Q8: File -> office.jpg: You have been provided with a picture of the building in which the company has an office. Which city is the company located in?

This is the image provided to us:

<img width="3062" height="1630" alt="image" src="https://github.com/user-attachments/assets/002d65dd-1b82-4df4-8195-3d01dbf0b188" />

We can then use Google Lens to see where this image is located:

<img width="2644" height="1678" alt="image" src="https://github.com/user-attachments/assets/2e4e6392-e650-4e34-9874-e96fcb3946ad" />

<details>
  <summary>Answer</summary>

   ```
   Birmingham
   ```

</details>

> Q9: File -> Webcam.png: With the intel, you have provided, our ground surveillance unit is now overlooking the person of interest suspected address. They saw them leaving their apartment and followed them to the airport. Their plane took off and landed in another country. Our intelligence team spotted the target with this IP camera. Which state is this camera in?

This is the image provided to us:

<img width="2660" height="1742" alt="image" src="https://github.com/user-attachments/assets/e761a930-5efe-43c5-8f14-70a56ef45fa9" />

We can then use Google Lens to see where this image is located:

<img width="2788" height="1710" alt="image" src="https://github.com/user-attachments/assets/49225230-fe1f-4fde-a51f-ee6057aa62b9" />

The University of Notre Dame is located in **Indiana**.

<details>
  <summary>Answer</summary>

   ```
   Indiana
   ```

</details>

