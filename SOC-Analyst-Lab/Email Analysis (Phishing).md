# Email Analysis (Phishing)
### Objective
The primary objective of **email analysis** in the context of **phishing** is to detect and prevent fraudulent emails that aim to deceive recipients into revealing sensitive information or performing malicious actions.

---
### Scenario

CoCanDa, a planet known as 'The Heaven of the Universe' has been having a bad year. A series of riots have taken place across the planet due to the frequent abduction of citizens, known as CoCanDians, by a mysterious force. CoCanDa’s Planetary President arranged a war-room with the best brains and military leaders to work on a solution. After the meeting concluded the President was informed his daughter had disappeared. CoCanDa agents spread across multiple planets were working day and night to locate her. Two days later and there’s no update on the situation, no demand for ransom, not even a single clue regarding the whereabouts of the missing people. On the third day a CoCanDa representative, an Army Major on Earth, received an email.

---
### Questions

At the end of this analysis we should be able to answer these questions
1. What is the email service used by the malicious actor?
1. What is the Reply-To email address?
2. What is the filetype of the received attachment which helped to continue the investigation?
3. What is the name of the malicious actor? 
4. What is the location of the attacker in this Universe? 
5. What could be the probable C&C domain to control the attacker’s autonomous bots? 
---
### Tools Used
- **Windows virtual machine**
- **Sublime Text** for text editor
- **HxD** to view files in HEX
- **7-Zip**
- **SquareX**
- **CyberChef**
- **Gary Kessler**
- **ExifTool** used to read, write, and manipulate metadata in various file formats

----
### Steps
**1**. Download the email file and extract it using 7-Zip

![File extraction](https://github.com/user-attachments/assets/22302590-04cb-45df-a2e1-0c6ae9fddc57)

**2**. Open the Email file with Sublime Text

![Image](https://github.com/user-attachments/assets/5aa2214d-54a1-4717-9cc2-e9df9f291b9c)

**3** Investigation of the Email header
 
 -  From the top the very first field is **delivered to**, this field indicates who received the email which. In this case, it is **themajoronearth@gmail.com** 

 ![1](https://github.com/user-attachments/assets/a0c16a41-0bc4-4980-816f-6ac47d344285)

 - Next we have **Received** or **Received by**. These are email servers that have received the email similar to how post office delivers their mail. The mail will end up in multiple post offices before reaching the post office that is closest to the recipient and the first **_Received by_** from the top is the closest mail server to the recipient. While the last **_Received by_** is the closest mail server to the sender

 ![2](https://github.com/user-attachments/assets/9a56670c-76a1-4af1-80fb-69f185b4c95e)
 ![3](https://github.com/user-attachments/assets/73708806-1786-442d-921e-bf70e53b7f7a)

  - Next we have **ARC headers**
  
  **ARC (Authenticated Received Chain)**  is a mechanism used in email security to maintain trust in email authentication results as a message passes through multiple intermediaries, such as forwarding services, mailing lists, or other relays.

Key Components of the ARC Protocol

The ARC protocol introduces three main header fields in email messages:

1. **ARC-Seal**: Ensures the integrity of the ARC headers added by an intermediary.
![4](https://github.com/user-attachments/assets/4befa448-12e7-4698-84e8-5c54b46b731e)

2. **ARC-Message-Signature (AMS)**: Verifies the content of the message as it was received by the intermediary, similar to a DKIM signature.
![5](https://github.com/user-attachments/assets/c40dff8d-99ac-4d6a-80e6-a6bf20b93939)

3. **ARC-Authentication-Results**: Records the authentication results (SPF, DKIM, DMARC) observed by the intermediary.
![6](https://github.com/user-attachments/assets/0c9ecefb-6b27-4519-9de1-774f88670bbc) 
**key information**

        spf=fail
* The **Sender Policy Framework (SPF)** check **_failed_**.
* This means the IP address **93.99.104.210** is not authorized to send emails on behalf of the domain **microapple.com.**

        smtp.mailfrom=billjobs@microapple.com
* This indicates the sender's email address that was specified in the **MAIL FROM** command during the SMTP transaction.

* Next we have **Return-Path**: this is the email address **< themajoronearth@gmail.com >** that will be used if the email fails to send which is typically used for troubleshooting purposes.
![8](https://github.com/user-attachments/assets/5d8c08a4-9176-4482-9796-d809c5d6d64e)

* **Investigation continuous** we have: 
![8](https://github.com/user-attachments/assets/3b0cbd75-0c59-4d89-b10b-55a5cf012fd2)



- The **To**: recipient of the email is **themajoronearth@gmail.com**

- The **Subject**: The email's subject is **"A Hope to CoCanDa"**. This could be designed to invoke curiosity or urgency, typical in phishing or socially engineered emails.

- The **From**: Displayed as **"Bill" <billjobs@microapple.com >**. 

- The **Reply-To**: **negeja3921@pashter.com**: This is the actual address the sender wants the recipient to reply to, which differs from the **"From** address". This discrepancy is a strong indicator of phishing. The domain **pashter.com** may be a disposable or malicious email provider.

- **Content-Type**: The used of **multipart/mixed** nSuggests the email contains both a text part and attachments. The **boundary** parameter separates these parts.

- The Message-ID: **<20210126064118.1993E221F8@localhost >**: Typically unique to the email. The inclusion of **localhost** raises suspicion, as legitimate emails usually show a fully qualified domain name.

- **Date**: **Tue, 26 Jan 2021 01:41:18 -0500 (EST)**: The timestamp of when the email was supposedly sent. Comparing this with other headers reveal inconsistencies.

### Email content
 ![9](https://github.com/user-attachments/assets/4e7003c3-7e91-4877-b28d-ad8b3d2d3440)

The content within the email is **base64-encoded**. Decoding it will reveal the **plain text** message hidden within this encoding. let's decode the message using a trusty tool called **Cyberchef** 

### Cyberchef
![10](https://github.com/user-attachments/assets/f1e26b86-cf36-48b0-b8a0-60d2ee8c982e)

Looking at the output of the encoded message the sender, mentioned something about an **attachment** so let's head back over to  our SublimeText
![11](https://github.com/user-attachments/assets/d701372e-f10a-4c68-8dbb-019746de051e)

The email contains an attachment encoded in **Base64** format. The file is labeled as **PuzzleToCoCanDa.pdf**, indicating it is a **PDF** file. let's decode the file using  **Cyberchef** 

![Image](https://github.com/user-attachments/assets/056f963b-c776-4cff-a582-65c2639ec03b)

Let's  look at the attachment signature by converting the **Output** into **Hexadecimal**
![Image](https://github.com/user-attachments/assets/0c90292a-3f02-4e12-83f5-05a0097d6540)

Let's examine the first four digits of the **Hexadecimal output** using a site called **Gary Kessler**: File Signatures
![Image](https://github.com/user-attachments/assets/09883223-000d-45d8-9079-e5ee13a4a7e6)
We can clearly see that, the said attachment is not a **PDF file** but a **ZIP file** . I will save this file and call it **attachment.zip** 


- Let's extract the **attachement** and we get a **PuzzleToCoCanDa** directory so let's go ahead and open that up and we see two files here but just in case there are any hidden files I click click on view and check off hidden items and now we see an additional file called **money. xlsx** which is a file extension for Microsoft Excel
  
![Image](https://github.com/user-attachments/assets/7eadfdee-e52b-40fe-b02f-94fe00877946)

 - let's figure out if **money. xlsx** it is actualy an Excel file
 - Using a tool called **HxD** , let view all these fils in their HEX format and discover thier real identity.
#### DaughtersCrown ![Image](https://github.com/user-attachments/assets/97dae948-7fcc-4b5c-8e1a-835f0567e7fb) we can clearly see that **DaughtersCrown** is a **JPEG** file. The actual image bellow

 ![Image](https://github.com/user-attachments/assets/a67ee664-20e1-417d-ad0a-89e9d7e7e713)
 
#### GoodJobMajor ![Image](https://github.com/user-attachments/assets/58fa1862-790c-4e34-bc59-90b50a8e6b3d) we can clearly see that **GoodJobMajor** is a **PDF** file. 
![Image](https://github.com/user-attachments/assets/51c435be-7576-42b3-8252-dd89c690537d)

#### money. xlsx ![Image](https://github.com/user-attachments/assets/cc9b9bf1-38bb-4d06-9b98-9a11e48593e7) We do se:
- **zip file** and  also 
-  **Microsoft open Office XML format**. 
But we can't safely say that **money. xlsx** is an Excel document 

let's see teh content of **money. xlsx** using a tool called **SquareX** ![Image](https://github.com/user-attachments/assets/c22752e3-1342-4f12-8690-1088f0451328)
We can see two differents sheets: **Sheet1** and **Sheet3** ![Image](https://github.com/user-attachments/assets/0e4ef136-3c01-4173-a437-3131a9075bdf)
 **Sheet3** is having an encoded message. Let's use **CyberChef** to decode it ![Image](https://github.com/user-attachments/assets/433bc172-a9aa-4ad8-83e3-5d18639ab45a) 
 The decoded message will propably be the **location** mentioned at **Sheet1**

 ----
 ### Recap
 These are fields we should take a good look at when analysing emails
 - **Received** : these are the mail service that receive the Email
 - **Return-Path**
 - **Authentication-Results**
 - **To**
 - **Subject**
 - **From**
 - **Reply-To**
 - **Content-Type**
 ![Image](https://github.com/user-attachments/assets/c4b3ab9f-ed4b-4396-9752-42685684aa77)
 Email service unsed by the malicious actor **emkei.cz** happened to be a **Fake Mailler**
 ![Image](https://github.com/user-attachments/assets/e683b271-5954-4301-a5c2-e7e3ccc35738)

---
### Answer to questions

1.What is the email service used by the malicious actor?

        emkei.cz
2. What is the Reply-To email address?

        negeja3921@pashter.com
2. What is the filetype of the received attachment which helped to continue the investigation?

        .zip

3. What is the name of the malicious actor? 

To answer this question we are using a tool called **Exiftool** to read metadata in the attachement we have downloaded. probably we will get the autor overthere
![Image](https://github.com/user-attachments/assets/cf590edd-a2cb-4d37-a7ea-21530a3267be)

         Pestero Negeja

4. What is the location of the attacker in this Universe? 

As we mentioned earlier the decoded message in the **Sheet3** of the  excel file give us the location 

        The Martian Colony, Beside Interplanetary Spaceport.

5. What could be the probable C&C domain to control the attacker’s autonomous bots? 

![Image](https://github.com/user-attachments/assets/28104871-90bc-48c9-94aa-3aa3b2ceeafb)

        pashter.com

# THANKS FOR READING.
