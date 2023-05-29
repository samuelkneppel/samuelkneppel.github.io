---
layout: post
title:  "TryHackMe Walkthrough - Splunk 2"
date:   2023-02-28 01:00:00 -0400
categories: splunk tryhackme walkthrough
---

![](\content\2023-02-28-tryhackme-walkthrough-splunk-2\2023-02-28-tryhackme-walkthrough-splunk-2.png)

#### My Introduction

The purpose of this post is to document my journey through the TryHackMe platform. This article contains answers to the questions provided along with the commands I used to obtain the answers. I will also include any additional notes along the way.

This [room](https://tryhackme.com/room/splunk2gcd5) was is a continuation of the [Splunk: Basics room](https://tryhackme.com/room/splunk101).

NOTE: only subscribers to TryHackMe are allowed to access this room. If you would like to subscribe to TryHackMe, sign up [here](https://tryhackme.com/why-subscribe).

### Task 1: Deploy!

**Task 1.1** **–** Read through this section.

**Task 1.2 –** Connect to the VPN and navigate to http://MACHINE\_IP:8000 after you click **Start Machine**.

**Question 1.1** **–** Deployed the virtual machine and connected to the website found at MACHINE\_IP:8000

**Answer 1.1** **–** Click the **Completed** button to progress to the next task.

#### Task 2: Dive into the data

**Task 2.1** **–** Read through this section.

**Question 2.1** **–** I’m ready to get hunting with Splunk.

**Answer 2.1** **–** Click the **Completed** button to progress to the next task.

![](\content\2023-02-28-tryhackme-walkthrough-splunk-2\2023-02-28-tryhackme-walkthrough-splunk-2-task-2.png)

### Task 3: 100 series questions

**Task 3.1 –** Read through this section and answer the following questions.

**Question 3.1 –** Amber Turing was hoping for Frothly to be acquired by a potential competitor which fell through, but visited their website to find contact information for their executive team. What is the website domain that she visited?

**Answer 3.1 –** www.berkbeer.com

**Explanation 3.1 –** The final Splunk query I used to find this answer is: `index="botsv2" 10.0.2.101 sourcetype="stream:HTTP" _beer_ | dedup site | table site`

**Question 3.2 –** Amber found the executive contact information and sent him an email. What image file displayed the executive’s contact information? Answer example: /path/image.ext

**Answer 3.2 –** /images/ceoberk.png

**Explanation 3.2 –** `index="botsv2" 10.0.2.101 sourcetype="stream:HTTP" www.berkbeer.com | dedup uri_path | table uri_path`

**Question 3.3 –** What is the CEO’s name? Provide the first and last name.

**Answer 3.3 –** Martin Berk

**Explanation 3.3 –** `index="botsv2" sourcetype="stream:smtp" [[email protected]](/cdn-cgi/l/email-protection) [[email protected]](/cdn-cgi/l/email-protection)`

**Question 3.4 –** What is the CEO’s email address?

**Answer 3.4 –** `[[email protected]](/cdn-cgi/l/email-protection)`

**Question 3.5 –** After the initial contact with the CEO, Amber contacted another employee at this competitor. What is that employee’s email address?

**Answer 3.5 –** [\[email protected\]](/cdn-cgi/l/email-protection)

**Explanation 3.5 –** `index="botsv2" sourcetype="stream:smtp" [[email protected]](/cdn-cgi/l/email-protection)`

**Question 3.6 –** What is the name of the file attachment that Amber sent to a contact at the competitor?

**Answer 3.6 –** Saccharomyces\_cerevisiae\_patent.docx

**Explanation 3.6 –** `index="botsv2" sourcetype="stream:smtp" [[email protected]](/cdn-cgi/l/email-protection) [[email protected]](/cdn-cgi/l/email-protection)`

**Question 3.7 –** What is Amber’s personal email address?

**Answer 3.7 –** [\[email protected\]](/cdn-cgi/l/email-protection)

**Explanation 3.7 –** First, I ran the following query to get the Base64 encoded response Amber sent to [\[email protected\]](/cdn-cgi/l/email-protection): `index="botsv2" sourcetype="stream:smtp" [[email protected]](/cdn-cgi/l/email-protection) [[email protected]](/cdn-cgi/l/email-protection)`. Then, I took the Base64 encoded content and used [CyberChef](https://cyberchef.org/) to decode it.

### Task 4: 200 series questions

**Task 4.1 –** Read through this section and answer the following questions.

**Question 4.1 –** What version of TOR Browser did Amber install to obfuscate her web browsing? Answer guidance: Numeric with one or more delimiter.

**Answer 4.1 –** 7.0.4

**Explanation 4.1 –** `index="botsv2" amber tor install | reverse`

**Question 4.2 –** What is the public IPv4 address of the server running www.brewertalk.com?

**Answer 4.2 –** 52.42.208.228

**Explanation 4.2 –** `index="botsv2" sourcetype="stream:http" site="www.brewertalk.com"`

**Question 4.3 –** Provide the IP address of the system used to run a web vulnerability scan against www.brewertalk.com.

**Answer 4.3 –** 45.77.65.211

**Explanation 4.3 –** `index="botsv2" sourcetype="stream:http" site="www.brewertalk.com"`

**Question 4.4 –** The IP address from Q#2 is also being used by a likely different piece of software to attack a URI path. What is the URI path? Answer guidance: Include the leading forward slash in your answer. Do not include the query string or other parts of the URI. Answer example: /phpinfo.php

**Answer 4.4 –** /member.php

**Explanation 4.4 –** `index="botsv2" sourcetype="stream:http" src_ip="45.77.65.211"`

**Question 4.5 –** What SQL function is being abused on the URI path from the previous question?

**Answer 4.5 –** updatexml

**Explanation 4.5 –** `index="botsv2" sourcetype="stream:http" src_ip="45.77.65.211" uri_path="/member.php"`

**Question 4.6 –** What was the value of the cookie that Kevin’s browser transmitted to the malicious URL as part of an XSS attack? Answer guidance: All digits. Not the cookie name or symbols like an equal sign.

**Answer 4.6 –** 1502408189

**Explanation 4.6 –** `index="botsv2" sourcetype="stream:http" kevin src_ip="71.39.18.125" brewertalk.com`

**Question 4.7 –** What brewertalk.com username was maliciously created by a spear phishing attack?

**Answer 4.7 –** kIagerfield

**Explanation 4.7 –** `index="botsv2" sourcetype="stream:http" kevin src_ip="71.39.18.125" brewertalk.com`

### Task 5: 300 series questions

**Task 5.1 –** Read through this section and answer the following questions.

**Question 5.1 –** Mallory’s critical PowerPoint presentation on her MacBook gets encrypted by ransomware on August 18. What is the name of this file after it was encrypted?

**Answer 5.1 –** Frothly\_marketing\_campaign\_Q317.pptx.crypt

**Explanation 5.1 –** `index="botsv2" host="maclory-air13" (*.ppt OR * .pptx)`

**Question 5.2 –** There is a Games of Thrones movie file that was encrypted as well. What season and episode is it? 

**Answer 5.2 –** S07E02

**Explanation 5.2 –** `index="botsv2" host="maclory-air13" (*.crypt)`

**Question 5.3 –** Kevin Lagerfield used a USB drive to move malware onto kutekitten, Mallory’s personal MacBook. She ran the malware, which obfuscates itself during execution. Provide the vendor name of the USB drive Kevin likely used. Answer Guidance: Use time correlation to identify the USB drive.

**Answer 5.3 –** Alcor Micro Corp.

**Explanation 5.3 –** `index="botsv2" host="kutekitten" usb`

**Question 5.4 –** What programming language is at least part of the malware from the question above written in?

**Answer 5.4 –** Perl

**Explanation 5.4 –** [https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/details](https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/details)

**Question 5.5 –** When was this malware first seen in the wild? Answer Guidance: YYYY-MM-DD

**Answer 5.5 –** 2017-01-17

**Explanation 5.5 –** [https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/details](https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/details)

**Question 5.6 –** The malware infecting kutekitten uses dynamic DNS destinations to communicate with two C&C servers shortly after installation. What is the fully-qualified domain name (FQDN) of the first (alphabetically) of these destinations?

**Answer 5.6 –** eidk.duckdns.org

**Explanation 5.6 –** [https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/relations](https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/relations)

**Question 5.7 –** From the question above, what is the fully-qualified domain name (FQDN) of the second (alphabetically) contacted C&C server?

**Answer 5.7 –** eidk.hopto.org

**Explanation 5.7 –** [https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/relations](https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271/relations)

### Task 6: 400 series questions

**Task 6.1 –** Read through this section and answer the following questions.

**Question 6.1 –** A Federal law enforcement agency reports that Taedonggang often spear phishes its victims with zip files that have to be opened with a password. What is the name of the attachment sent to Frothly by a malicious Taedonggang actor?

**Answer 6.1 –** invoice.zip

**Explanation 6.2 –** `index="botsv2" sourcetype="stream:smtp" *.zip`

**Question 6.2 –** What is the password to open the zip file?

**Answer 6.2 –** 912345678

**Explanation 6.2 –** `index="botsv2" invoice.zip`

**Question 6.3 –** The Taedonggang APT group encrypts most of their traffic with SSL. What is the “SSL Issuer” that they use for the majority of their traffic? Answer guidance: Copy the field exactly, including spaces.

**Answer 6.3 –** C = US

**Explanation 6.3 –** `index="botsv2" sourcetype="stream:tcp" 45.77.65.211`

**Question 6.4 –** What unusual file (for an American company) does winsys32.dll cause to be downloaded into the Frothly environment?

**Answer 6.4 –** 나는\_데이비드를\_사랑한다.hwp

**Explanation 6.4 –** `index="botsv2" sourcetype="stream:ftp" method=RETR`

**Question 6.5 –** What is the first and last name of the poor innocent sap who was implicated in the metadata of the file that executed PowerShell Empire on the first victim’s workstation? Answer example: John Smith

**Answer 6.5 –** Ryan Kovar

**Explanation 6.5 –** [https://www.hybrid-analysis.com/sample/d8834aaa5ad6d8ee5ae71e042aca5cab960e73a6827e45339620359633608cf1/598155a67ca3e1449f281ac4](https://www.hybrid-analysis.com/sample/d8834aaa5ad6d8ee5ae71e042aca5cab960e73a6827e45339620359633608cf1/598155a67ca3e1449f281ac4)

**Question 6.6 –** Within the document, what kind of points is mentioned if you found the text?

**Answer 6.6 –** CyberEastEgg

**Explanation 6.6 –** [https://app.any.run/tasks/15d17cd6-0eb6-4f52-968d-0f897fd6c3b3/](https://app.any.run/tasks/15d17cd6-0eb6-4f52-968d-0f897fd6c3b3/)

**Question 6.7 –** To maintain persistence in the Frothly network, Taedonggang APT configured several Scheduled Tasks to beacon back to their C2 server. What single webpage is most contacted by these Scheduled Tasks? Answer example: index.php or images.html

**Answer 6.7 –**

**Explanation 6.7 –** `index="botsv2" schtasks.exe | reverse`

### Task 7: Conclusion

**Task 7.1 –** Read through this section.

**Question 7.1 –** You leveled up your Splunk-fu thanks to the BOTSv2 dataset.

**Answer 7.1 –** Click the **Completed** button to complete this room.