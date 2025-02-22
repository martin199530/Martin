# Incident handling with Splunk
An **incident** from a security perspective is "Any event or action, that has a negative consequence on the security of a user/computer or an organization"

![Image](https://github.com/user-attachments/assets/0f7ba928-423b-4d87-88b1-d99666b57b4f)

Below are a few of the events that would negatively affect the environment when they occurred:

- Crashing the system
- Execution of an unwanted program
- Access to sensitive information from an unauthorized user
- A Website being defaced by the attacker
- The use of USB devices when there is a restriction in usage is against the company's policy

## Lesson learned

- How to leverage OSINT sites during an investigation
- How to map Attacker's activities to Cyber Kill Chain Phases
- How to utilize effective Splunk searches to investigate logs
- Understand the importance of host-centric and network-centric log sources

## Incident Handling Life Cycle

![Image](https://github.com/user-attachments/assets/cfa50616-edf3-4edd-86c0-5a484bae89f9)

As an Incident Handler / SOC Analyst, I would aim to know the attackers' **tactics, techniques**, and **procedures**. ThenI can **stop/defend/prevent** against the attack in a better way. The Incident Handling process is divided into four different phases. 

*1. Preparation*

*2. Detection and Analysis*

*3. Containment, Eradication, and Recovery*

*4. Post-Incident Activity / Lessons Learnt*
## Incident Handling: Scenario

In this Scenario, we will investigate a cyber attack in which the attacker defaced an organization's website. This organization has Splunk as a SIEM solution setup. My task as a Security Analysis would be to investigate this cyber attack and map the attacker's activities into all 7 of the Cyber Kill Chain Phases

## Scenario

A Big corporate organization **Wayne Enterprises** has recently faced a cyber-attack where the attackers broke into their network, found their way to their web server, and have successfully defaced their website **http://www.imreallynotbatman.com**. Their website is now showing the trademark of the attackers with the message **YOUR SITE HAS BEEN DEFACED** as shown below.

![Image](https://github.com/user-attachments/assets/e6f8466b-8aa5-49fe-ade9-35c1587075a7)

They have requested "**ME**" to join them as a **Security Analyst** and help them investigate this cyber attack and find the root cause and all the attackers' activities within their network.

The good thing is, that they have Splunk already in place, so I have got all the event logs related to the attacker's activities captured. I need to explore the records and find how the attack got into their network and what actions they performed.

This Investigation comes under the **Detection and Analysis phase**.

## Splunk
During our investigation, I will be using Splunk as  **SIEM solution**. Logs are being ingested from **webserver/firewall/Suricata/Sysmon** etc. In the data summary tab, we can explore the log sources showing visibility into both network-centric and host-centric activities.

![Image](https://github.com/user-attachments/assets/e0217a98-b6a2-4d5a-a512-1e6e2b53ab11)

**Note:** All the event logs that we are going to investigate are present in 

      index=botsv1

## Reconnaissance Phase

![Image](https://github.com/user-attachments/assets/6ac8ac87-34f8-4800-871c-8a0c3ed50b0f)

**Reconnaissance** is an attempt to discover and collect information about a target. It could be knowledge about the system in use, the web application, employees or location, etc.

I will start The analysis by examining any reconnaissance attempt against the webserver **imreallynotbatman.com**

I am going to look for the event logs in the index **"botsv1**" which contains the term **imreallynotbatman.com**

      index=botsv1 imreallynotbatman.com

![Image](https://github.com/user-attachments/assets/35ff6b01-542a-4c59-95d6-7cbfdf8d3c08)

From the name of these log sources, it is clear what each log source may contain **imreallynotbatman.com**. My first task is to identify the **IP address** attempting to perform reconnaissance activity on the **web server**. It would be obvious to look at the web traffic coming into the network.

Let us begin looking at the log source **stream:http**, which contains the http traffic logs.

**Search Query:** 

      index=botsv1 imreallynotbatman.com sourcetype=stream:http

 This query will only look for the term  **imreallynotbatman.com** in the **stream:http** log source.

![Image](https://github.com/user-attachments/assets/d2cb46a8-6ff4-4ed3-b3c8-4cb71669e1d2)

So far, we have found two IPs in the src_ip field **40.80.148.42** and **23.22.63.114**. The first IP seems to contain a high percentage of the logs as compared to the other IP, which could be the answer.

      40.80.148.42

To further confirm our suspicion about the IP address **40.80.148.42**, click on the IP and examine the logs. We can look at the interesting fields like **User-Agent, Post request, URIs**, etc., to see what kind of traffic is coming from this particular IP.

![Image](https://github.com/user-attachments/assets/50c6e547-25de-45ed-8f6c-4c4d5b9d3da7)

## Validate the IP that is scanning

So what do I need to do to validate the scanning attempt? Simple, dig further into the weblogs. Let us narrow down the result, look into the **suricata** logs, and see if any rule is triggered on this communication.

**Search Query:** 

      index=botsv1 imreallynotbatman.com src=40.80.148.42 sourcetype=suricata

 This query will show the logs from the suricata log source that are detected/generated from the source IP **40.80.248.42**

 ![Image](https://github.com/user-attachments/assets/e69a0d3e-3fcd-44c9-b5db-b4b820aeb138)

I have narrowed our search on the **src IP** and looked at the **source type** suricata to see what Suricata triggered alerts. In the right panel, we could not find the field of our interest, so we clicked on more fields and searched for the fields that contained the **signature alerts** information, which is an important point to note.

**Question 1 :** One suricata alert highlighted the CVE value associated with the attack attempt. What is the CVE value?

![Image](https://github.com/user-attachments/assets/76e8cded-0f1d-4477-b258-e5a9cb089a09)

       Answer : CVE-2014-6271

**Question 2 :** What is the CMS our web server is using? (CMS: Content Management System )

![Image](https://github.com/user-attachments/assets/116fef1b-3c8d-4cb9-8b32-ce9458d9b141)

       Answer : Joomla

**Question 3 :** What is the web scanner, the attacker used to perform the scanning attempts?

![Image](https://github.com/user-attachments/assets/30a7f5a9-93e3-400c-b663-00435c7c48e1)

       Answer : acunetix

**Question 4 :** What is the IP address of the server imreallynotbatman.com?

![Image](https://github.com/user-attachments/assets/07489380-977e-4957-92da-b344db89e30c)

       Answer : 192.168.250.70

## Exploitation Phase

The attacker needs to exploit the vulnerability to gain access to the system/server.

To begin our investigation, let's note the information we have so far:

- We found two IP addresses from the reconnaissance phase with sending requests to our server.
- One of the IPs **40.80.148.42** was seen attempting to scan the server with IP **192.168.250.70**.
- The attacker was using the web scanner **Acunetix** for the scanning attempt.

## Count

Let's use the following **search query** to see the number of counts by each source IP against the webserver.

**Search Query**:

        index=botsv1 imreallynotbatman.com sourcetype=stream* | stats count(src_ip) as Requests by src_ip | sort - Requests

This query uses the stats function to display the count of the IP addresses in the field **src_ip**.

![Image](https://github.com/user-attachments/assets/9b3cea56-4563-41b4-b043-c45b7cadc084)

Additionally, we can also create different **visualization** to show the result.

![Image](https://github.com/user-attachments/assets/4293ac4c-e5e5-41bb-b7dd-e68b47bc9fe5)