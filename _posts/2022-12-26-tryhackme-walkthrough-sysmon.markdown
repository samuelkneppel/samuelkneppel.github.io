---
layout: post
title:  "TryHackMe Walkthrough - Sysmon"
date:   2022-12-26 01:00:00 -0400
categories: microsoft sysinternals sysmon tryhackme walkthrough windows
---

![](\content\2022-12-26-tryhackme-walkthrough-sysmon\2022-12-26-tryhackme-walkthrough-sysmon.png)

#### My **Introduction**

The purpose of this article is to document my journey through the TryHackMe platform. This article will contain answers to the questions provided along with the thought process as to how I obtained them. I will also include any additional notes along the way.

This [room](https://tryhackme.com/room/sysmon) was created to teach one how to utilize Sysmon to monitor and log endpoints and environments.

**NOTE:** only subscribers to TryHackMe are allowed to access this room. If you would like to subscribe to TryHackMe, sign up [here](https://tryhackme.com/why-subscribe).

#### **Task 1: Introduction**

**Task 1.1 –** Read through this section.

**Question 1.1 –** Complete the prerequisites listed above and jump into task 2.

**Answer 1.1 –** Click the **Completed** button to progress to the next task.

#### **Task 2: Sysmon Overview**

**Task 2.1 –** Read through this section.

**Question 2.1 –** Read the above and become familiar with the Sysmon Event IDs.

**Answer 2.1 –** Click the **Completed** button to progress to the next task.

#### **Task 3: Installing and Preparing Sysmon**

**Task 3.1 –** Read through this section.

**Task 3.2 –** Click **Start Machine** to start the machine.

**Task 3.3 –** RDP into the machine via it’s IP address and login using the credentials `THM-Analyst:5TgcYzF84tcBSuL1Boa%dzcvf`. Alternatively, you can use the build-in AttackBox or download the event logs for each task going forward and take a look at them on your local machine if you prefer.

**Question 3.1 –** Deploy the machine and start Sysmon.

**Answer 3.1 –** Click the **Completed** button to progress to the next task.

#### **Task 4: Cutting out the Noise**

**Task 4.1 –** Read through this section. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 4.1 –**  Read the above and practice filtering events.

**Answer 4.1 –** Click the **Completed** button to progress to the next task.

**Question 4.2 –** How many event ID 3 events are in C:\\Users\\THM-Analyst\\Desktop\\Scenarios\\Practice\\Filtering.evtx?

**Answer 4.2 –** 73,591

**Explanation 4.2 –** I opened up PowerShell and ran the following command to obtain this answer: `Get-WinEvent -Path "C:\Users\THM-Analyst\Desktop\Scenarios\Practice\Filtering.evtx" -FilterXPath '*/System/EventID=3' | Measure-Object`

**Question 4.3 –** What is the UTC time created of the first network event in C:\\Users\\THM-Analyst\\Desktop\\Scenarios\\Practice\\Filtering.evtx?

**Answer 4.3 –** 2021-01-06 01:35:50.464

**Explanation 4.3 –** This time, I used the WIndows Event Viewer GUI to filter by Event ID 3 and then sort by date and time. I found the `UtcTime` value within `EventData`.

#### **Task 5: Hunting Metasploit**

**Task 5.1 –** Read through this section.

**Question 5.1 –** Read the above and practice hunting Metasploit with the provided event file.

**Answer 5.1 –** Click the **Completed** button to progress to the next task.

**Explanation 5.1-** After starting sysmon.exe with the ion-storm config file using the following command: `.\Sysmon.exe -accepteula -i .\sysmonconfig\ion-storm-sysmonconfig-export.xml`, I was able to run the command provided to us to seach for Metasploit specific events: `Get-WinEvent -Path .\HuntingMetasploit.evtx -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data=4444'`.

#### **Task 6: Hunting Mimikatz**

**Task 6.1 –** Read through this section.

**Question 6.1 –** Read the above and practice detecting Mimikatz with the provided evtx.

**Answer 6.1 –** Click the **Completed** button to progress to the next task.

**Explanation 6.1-** As stated within this task, the command to run via PowerShell in order to query for abnormal ``lsass.exe` behavior is `Get-WinEvent -Path .\HuntingMimikatz.evtx -FilterXPath '*/System/EventID=10 and */EventData/Data[@Name="TargetImage"] and */EventData/Data="C:\Windows\system32\lsass.exe"'``.

![](\content\2022-12-26-tryhackme-walkthrough-sysmon\2022-12-26-tryhackme-walkthrough-sysmon-task-6.png)

#### **Task 7: Hunting Malware**

**Task 7.1 –** Read through this section.

**Question 7.1 –** Read the Above and practice hunting rats and C2 servers with back connect ports.

**Answer 7.1 –** Click the **Completed** button to progress to the next task.

**Explanation 7.1-** As stated within this task, the command to run via PowerShell in order to query for network connections to port `8080` is `Get-WinEvent -Path .\HuntingRats.evtx -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data="8080"'`.

![](\content\2022-12-26-tryhackme-walkthrough-sysmon\2022-12-26-tryhackme-walkthrough-sysmon-task-7.png)

### Task 8: Hunting Persistence

**Task 8.1 –** Read through this section.

**Question 8.1 –** Read the above and practice hunting persistence techniques.

**Answer 8.1 –** Click the **Completed** button to progress to the next task.

![](\content\2022-12-26-tryhackme-walkthrough-sysmon\2022-12-26-tryhackme-walkthrough-sysmon-task-8.png)

#### **Task 9: Hunting Evasive Techniques**

**Task 9.1 –** Read through this section.

**Question 9.1 –** Read the above and practice detecting evasion techniques

**Answer 9.1 –** Click the **Completed** button to progress to the next task.

**Explanation 9.1-** As stated within this task, the command to run via PowerShell in order to query remote threads is `Get-WinEvent -Path '.\Detection Evasion Events\Detecting_RemoteThreads.evtx' -FilterXPath '*/System/EventID=8'`.

![](\content\2022-12-26-tryhackme-walkthrough-sysmon\2022-12-26-tryhackme-walkthrough-sysmon-task-9.png)

#### **Task 10: Practical Investigations**

**Task 10.1 –** Read through this section.

**Task 10.2 –** Download the task files to be used for the following questions.

**Question 10.1 –** What is the full registry key of the USB device calling svchost.exe in Investigation 1?

**Answer 10.1 –** `HKLM\System\CurrentControlSet\Enum\WpdBusEnumRoot\UMB\2&37c186b&0&STORAGE#VOLUME#_??_USBSTOR#DISK&VEN_SANDISK&PROD_U3_CRUZER_MICRO&REV_8.01#4054910EF19005B3&0#\FriendlyName`

**Question 10.2 –** What is the device name when being called by RawAccessRead in Investigation 1?

**Answer 10.2 –** \\Device\\HarddiskVolume3

**Question 10.3 –** What is the first .exe the process executes in Investigation 1?

**Answer 10.3 –** rundll32.exe

**Question 10.4 –** What is the full path of the payload in Investigation 2?

**Answer 10.4 –** `C:\Users\IEUser\AppData\Local\Microsoft\Windows\Temporary Internet Files\Content.IE5\S97WTYG7\update.hta`

**Question 10.5 –** What is the full path of the file the payload masked itself as in Investigation 2?

**Answer 10.5 –** `C:\Users\IEUser\Downloads\update.html`

**Question 10.6 –** What signed binary executed the payload in Investigation 2?

**Answer 10.6 –** `C:\Windows\System32\mshta.exe`

**Question 10.7 –** What is the IP of the adversary in Investigation 2?

**Answer 10.7 –** 10.0.2.18

**Question 10.8 –** What back connect port is used in Investigation 2?

**Answer 10.8 –** 4443

**Question 10.9 –** What is the IP of the suspected adversary in Investigation 3.1?

**Answer 10.9 –** 172.30.1.253

**Question 10.10 –** What is the host name of the affected endpoint in Investigation 3.1?

**Answer 10.10 –** \`DESKTOP-O153T4R\`

**Question 10.11 –** What is the host name of the C2 server connecting to the endpoint in Investigation 3.1?

**Answer 10.11 – e**mpirec2

**Question 10.12 –** Where in the registry was the payload stored in Investigation 3.1?

**Answer 10.12 –** HKLM\\SOFTWARE\\Microsoft\\Network\\debug

**Question 10.13 –** What PowerShell launch code was used to launch the payload in Investigation 3.1?

**Answer 10.13 –** `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -c "$x=$((gp HKLM:Software\Microsoft\Network debug).debug);start -Win Hidden -A \"-enc $x\" powershell";exit;`

**Question 10.14 –** What is the IP of the adversary in Investigation 3.2?

**Answer 10.14 –** 172.168.103.188

**Question 10.15 –** What is the full path of the payload location in Investigation 3.2?

**Answer 10.15 –** c:\\users\\q\\AppData:blah.txt

**Question 10.16 –** What was the full command used to create the scheduled task in Investigation 3.2?

**Answer 10.16 –** `C:\WINDOWS\system32\schtasks.exe" /Create /F /SC DAILY /ST 09:00 /TN Updater /TR "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -NonI -W hidden -c \"IEX ([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String($(cmd /c ''more < c:\users\q\AppData:blah.txt'''))))\"`

**Question 10.17 –** What process was accessed by schtasks.exe that would be considered suspicious behavior in Investigation 3.2?

**Answer 10.17 –** lsass.exe

![](\content\2022-12-26-tryhackme-walkthrough-sysmon\2022-12-26-tryhackme-walkthrough-sysmon-task-10.png)

**Question 10.18 –** What is the IP of the adversary in Investigation 4?

**Answer 10.18 –** 172.30.1.253

**Question 10.19 –** What port is the adversary operating on in Investigation 4?

**Answer 10.19 –** 80

**Question 10.20 –** What C2 is the adversary utilizing in Investigation 4?

**Answer 10.20 –** empire

#### My **Conclusion**

After completing this room, I have become much better acquainted with Sysmon and how to use it in a practical sense, which I have not had the opportunity to do so up until now. I believe this room was very beneficial to me and I encourage anyone reading this post to sign up for THM and complete it yourself.