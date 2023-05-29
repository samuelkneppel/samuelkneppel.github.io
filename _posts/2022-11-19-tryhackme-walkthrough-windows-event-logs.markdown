---
layout: post
title:  "TryHackMe Walkthrough - Windows Event Logs"
date:   2022-11-19 01:00:00 -0400
categories: event-logs microsoft tryhackme walkthrough windows
---

![](\content\2022-11-19-tryhackme-walkthrough-windows-event-logs\2022-11-19-tryhackme-walkthrough-windows-event-logs.png)

#### **Introduction**

The purpose of this article is to document my journey through the TryHackMe platform. This article will contain answers to the questions provided along with the thought process as to how I obtained them. I will also include any additional notes along the way.

This [room](https://tryhackme.com/room/windowseventlogs) was created as an introduction to Windows Event Logs and the tools to query them.

**NOTE:** only subscribers to TryHackMe are allowed to access this room. If you would like to subscribe to TryHackMe, sign up [here](https://tryhackme.com/why-subscribe).

#### **Task 1: What are event logs?**

**Task 1.1 –** Read through this section.

**Task 1.2 –** Click **Start Machine** to start the machine.

**Task 1.3 –** RDP into the machine via it’s IP address and login using the credentials `administrator:blueT3aming!`. Alternatively, you can use the build-in AttackBox if you prefer.

**Question 1.1 –** Let’s begin…

**Answer 1.1 –** Click the **Completed** button to progress to the next task.

#### **Task 2: Event Viewer**

**Task 2.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 2.1 –** For the questions below, use Event Viewer to analyze **Microsoft-Windows-PowerShell/Operational** log.

**Answer 2.1 –** Click the **Completed** button to progress to the next task.

**Question 2.2 –** What is the Event ID for the first recorded event?

**Answer 2.2 –** 40961

**Question 2.3 –** Filter on Event ID 4104. What was the 2nd command executed in the PowerShell session?

**Answer 2.3 –** `whoami`

**Question 2.4 –** What is the Task Category for Event ID 4104?

**Answer 2.4 –** Execute a Remote Command

**Question 2.5 –** Analyze the Windows PowerShell log. What is the Task Category for Event ID 800?

**Answer 2.6 –** Pipeline Execution Details

#### **Task 3: wevtutil.exe**

**Task 3.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 3.1 –** How many log names are in the machine?

**Answer 3.1 –** 1071

**Question 3.2 –** What event files would be read when using the query-events command?

**Answer 3.2 –** event log, log file, structured query

**Question 3.3 –** What option would you use to provide a path to a log file?

**Answer 3.3 –** `/lf:true`

**Question 3.4 –** What is the VALUE for `/q`?

**Answer 3.4 –** XPath query

**Question 3.5 –** The questions below are based on this command: wevtutil qe `Application /c:3 /rd:true /f:text`

**Answer 3.5 –** Click the **\*\*Completed\*\*** button to progress to the next task.

**Question 3.6 –** What is the log name?

**Answer 3.6 –** Application

**Question 3.7 –** What is the `/rd` option for?

**Answer 3.7 –** event read direction

**Question 3.8 –** What is the `/c` option for?

**Answer 3.8 –** Maximum number of events to read

#### **Task 4: Get-WinEvent**

**Task 4.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section, Microsoft’s [online](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent?view=powershell-7.1) documentation, the machine you are connected to.

**Question 4.1 –** Answer the following questions using the [online](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent?view=powershell-7.1) help documentation for `Get-WinEvent`

**Answer 4.1 –** Click the **Completed** button to progress to the next task.

**Question 4.2 –**  Execute the command from **Example 1** (as is). What are the names of the logs related to **OpenSSH**?

**Answer 4.2 –** `OpenSSH/Admin`, `OpenSSH/Operational`

**Question 4.3 –**  Execute the command from **Example 8**. Instead of the string **`/`**_`*Policy/*`_ search for **`/`**_`*PowerShell/*`_. What is the name of the 3rd log provider?

**Answer 4.3 –** `Microsoft-Windows-PowerShell-DesiredStateConfiguration-FileDownloadManager`

**Question 4.4 –** Execute the command from **Example 9**. Use **Microsoft-Windows-PowerShell** as the log provider. How many event ids are displayed for this event provider?

**Answer 4.4 –** 192

**Question 4.5 –** How do you specify the number of events to display?

**Answer 4.5 –** -MaxEvents

**Question 4.6 –** When using the **FilterHashtable** parameter and filtering by level, what is the value for **Informational**?

**Answer 4.6 –** 4

#### **Task 5: XPath Queries**

**Task 5.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section and the machine you are connected to.

**Question 5.1 –** Using **Get-WinEvent** and **XPath**, what is the query to find WLMS events with a System Time of `2020-12-15T01:09:08.940277500Z`?

**Answer 5.1 –** `Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"] and */System/TimeCreated[@SystemTime="2020-12-15T01:09:08.940277500Z"]'reated[@SystemTime="2020-12-15T01:09:08.940277500Z"]'`

**Question 5.2 –** Using **Get-WinEvent** and **XPath**, what is the query to find a user named Sam with an Logon Event ID of 4720?

**Answer 5.2 –** `Get-WinEvent -LogName Security -FilterXPath '*/System/EventID=4720 and */EventData/Data[@Name="TargetUserName"]="sam"'`

**Question 5.3 –** Based on the previous query, how many results are returned?

**Answer 5.3 –** 2

**Question 5.4 –** Based on the output from the question #2, what is Message?

**Answer 5.4 –** A user account was created

**Question 5.5 –** Still working with Sam as the user, what time was Event ID 4724 recorded? (MM/DD/YYYY H:MM:SS \[AM/PM\])

**Answer 5.5 –** 12/17/2020 1:57:14 PM

**Question 5.6 –** What is the Provider Name?

**Answer 5.6 –** **Microsoft-Windows-Security-Auditing**

#### **Task 6: Event IDs**

**Task 6.1 –** Read through this section and complete the tasks outlined.

**Question 6.1 –** I’m ready to look at some event logs…

**Answer 6.1 –** Click the **Completed** button to progress to the next task.

#### **Task 7: Putting theory into practice**

**Task 7.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section, the machine you are connected to, and online.

**Question 7.1 –** What event ID is to detect a PowerShell downgrade attack?

**Answer 7.1 –** 400

**Question 7.2 –** What is the _Date and Time_ this attack took place? (_MM/DD/YYYY H:MM:SS \[__AM/PM__\]_)

**Answer 7.2 –** 12/18/2020 7:50:33 AM

**Question 7.3 –** A Log clear event was recorded. What is the ‘Event Record ID’?

**Answer 7.3 –** 27736

**Question 7.4 –** What is the name of the computer?

**Answer 7.4 –** `PC01.example.corp`

**Question 7.5 –** What is the name of the first variable within the PowerShell command?

**Answer 7.5 –** `$Va5w3n8`

**Question 7.6 –** What is the _Date and Time_ this attack took place? (_MM/DD/YYYY H:MM:SS \[__AM/PM__\]_)

**Answer 7.6 –** 8/25/2020 10:09:28 PM

**Question 7.7 –** What is the _Execution Process ID_?

**Answer 7.7 –** 6620

**Question 7.8 –** What is the _Group Security ID_ of the group she enumerated?

**Answer 7.8 –** `S-1-5-32-544`

**Question 7.9 –** What is the _event ID_?

**Answer 7.9 –** 4799

#### **Task 8: Conclusion**

**Task 8.1 –** Read through this section and complete the tasks outlined.

**Question 8.1 –** Hope you enjoyed this room and learned a thing or two.

**Answer 8.1 –** Click the **Completed** button to progress to the next task.

#### My Conclusion

After completing this room, I obtained a better understanding of how Windows Event Logs work and how to manipulate them using the Event Viewer application, `wevtutil.exe`, and `Get-WinEvent`. As stated within the room, this knowledge will be used as a foundation for other technologies such as SIEMs, Sysmon, etc.

**Reference**: [TryHackMe - Windows Event Logs](https://tryhackme.com/room/windowseventlogs)