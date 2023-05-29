---
layout: post
title:  "TryHackMe Walkthrough - Osquery"
date:   2023-02-07 01:00:00 -0400
categories: microsoft osquery tryhackme walkthrough windows
---

![](\content\2023-02-07-tryhackme-walkthrough-osquery\2023-02-07-tryhackme-walkthrough-osquery.png)

#### **My Introduction**

The purpose of this article is to document my journey through the TryHackMe platform. This article will contain answers to the questions provided along with the thought process as to how I obtained them. I will also include any additional notes along the way.

This [room](https://tryhackme.com/room/sysmon) was created as an introduction to Osquery and its use cases.

**NOTE:** only subscribers to TryHackMe are allowed to access this room. If you would like to subscribe to TryHackMe, sign up [here](https://tryhackme.com/why-subscribe).

#### **Task 1: Introduction**

**Task 1.1 –** Read through this section.

**Question 1.1 –** Move on to the next task.

**Answer 1.1 –** Click the **Completed** button to progress to the next task.

#### **Task 2: Connect with the Lab**

**Task 2.1 –** Read through this section.

**Task 2.2 –** Click **Show Split View** at the top of the page to connect to the machine.

**Question 2.1 –** How many tables are returned when we query “table process” in the interactive mode of Osquery?

**Answer 2.1 –** 3

**Question 2.2 –** Looking at the schema of the processes table, which column displays the process id for the particular process?

**Answer 2.2 –** pid

![](\content\2023-02-07-tryhackme-walkthrough-osquery\2023-02-07-tryhackme-walkthrough-osquery.png)

**Question 2.3 –** Examine the .help command, how many output display modes are available for the .mode command?

**Answer 2.3 –** 5

#### **Task 4: Schema Documentation**

**Task 4.1 –** Read through this section.

**Question 4.1 –** In Osquery version 5.5.1, how many common tables are returned, when we select both Linux and Window Operating system?

**Answer 4.1 –** 56

**Question 4.2 –** In Osquery version 5.5.1, how many tables for MAC OS are available?

**Answer 4.2 –** 180

**Question 4.3 –** In the Windows Operating system, which table is used to display the installed programs?

**Answer 4.3 –** programs

**Question 4.4 –** In Windows Operating system, which column contains the registry value within the registry table?

**Answer 4.4 –** data

#### **Task 5: Creating SQL queries**

**Task 5.1 –** Read through this section.

**Question 5.1 –** Using Osquery, how many programs are installed on this host?

**Answer 5.1 –** 19

**Explanation 5.1 –** `select count(*) from programs;`

**Question 5.2 –** Using Osquery, what is the description for the user James?

**Answer 5.2 –** Creative Artist

**Explanation 5.2 –** `select * from users;`

**Question 5.3 –** When we run the following search query, what is the full SID of the user with RID 1009? Query: `select path, key, name from registry where key = 'HKEY_USERS';`

**Answer 5.3 –** S-1-5-21-1966530601-3185510712-10604624-1009

**Question 5.4 –** When we run the following search query, what is the Internet Explorer browser extension installed on this machine? Query: `select * from ie_extensions;`

**Answer 5.4 –** C:\\Windows\\System32\\ieframe.dll

**Question 5.5 –** After running the following query, what is the full name of the program returned? Query: `select name,install_location from programs where name LIKE '%wireshark%';`

**Answer 5.5 –** Wireshark 3.6.8 64-bit

#### **Task 6: Challenge and Conclusion**

**Task 6.1 –** Read through this section.

**Question 6.1 –** Which table stores the evidence of process execution in Windows OS?

**Answer 6.1 –** userassist

**Question 6.2 –** One of the users seems to have executed a program to remove traces from the disk; what is the name of that program?

**Answer 6.2 –** DiskWipe.exe

**Explanation 6.2 –** `select * from userassist;`

**Question 6.3 –** Create a search query to identify the VPN installed on this host. What is name of the software?

**Answer 6.3 –** ProtonVPN

**Explanation 6.3 –** `select name,version,install_location,install_date from programs where name LIKE '%vpn%';`

**Question 6.4 –** How many services are running on this host?

**Answer 6.4 –** 214

**Explanation 6.4 –** `select count(*) from services;`

**Question 6.5 –** A table **autoexec** contains the list of executables that are automatically executed on the target machine. There seems to be a batch file that runs automatically. What is the name of that batch file (with the extension .bat)?

**Answer 6.5 –** batstartup.bat

**Explanation 6.5 –** `select * from autoexec where path LIKE '%.bat';`

**Question 6.6 –** What is the full path of the batch file found in the above question? (Last in the List)

**Answer 6.6 –** C:\\Users\\James\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\Startup\\batstartup.bat