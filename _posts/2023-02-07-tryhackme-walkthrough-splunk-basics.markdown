---
layout: post
title:  "TryHackMe Walkthrough - Splunk: Basics"
date:   2023-02-07 01:00:00 -0400
categories: splunk tryhackme walkthrough
---

![](\content\2023-02-07-tryhackme-walkthrough-splunk-basics\2023-02-07-tryhackme-walkthrough-splunk-basics.png)

#### My Introduction

The purpose of this post is to document my journey through the TryHackMe platform. This article contains answers to the questions provided along with the commands I used to obtain the answers. I will also include any additional notes along the way.

This [room](https://tryhackme.com/room/splunk101) was created as an introduction to Splunk and its basics.

NOTE: only subscribers to TryHackMe are allowed to access this room. If you would like to subscribe to TryHackMe, sign up [here](https://tryhackme.com/why-subscribe).

#### Task 1: Introduction

**Task 1.1** **–** Read through this section.

**Question 1.1** **–** Continue with the next task.

**Answer 1.1** **–** Click the **Completed** button to progress to the next task.

#### Task 2: Connect with the Lab

**Task 2.1 –** Read through this section.

**Task 2.2 –** Connect to the VPN and navigate to http://MACHINE\_IP after you click **Start Machine**.

**Question 2.1 –** Connect with the lab.

**Answer 2.1 –** Click the **Completed** button to progress to the next task.

![](\content\2023-02-07-tryhackme-walkthrough-splunk-basics\2023-02-07-tryhackme-walkthrough-splunk-basics-task-2.png)

#### Task 3: Splunk Components

**Task 3.1 –** Read through this section and answer the following questions.

**Question 3.1 –** Which component is used to collect and send data over the Splunk instance?

Answer 3.1 – Forwarder

#### Task 4: Navigating Splunk

**Task 4.1 –** Read through this section and answer the following questions.

**Question 4.1 –** In the Add Data tab, which option is used to collect data from files and ports?

**Answer 4.1 –** Monitor

#### Task 5: Adding Data

**Task 5.1 –** Read through this section and answer the following questions.

**Question 5.1 –** Upload the data attached to this task and create an index “VPN\_Logs”. How many events are present in the log file?

**Answer 5.1 –** 2862

**Explanation 5.1 –** `source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json"`

**Question 5.2 –** How many log events by the user **Maleena** are captured?

**Answer 5.2 –** 60

**Explanation 5.2 –** `source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" UserName=Maleena`

**Question 5.3 –** What is the name associated with IP 107.14.182.38?

**Answer 5.4 –** Smith

**Explanation 5.4 –** `source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" Source_ip="107.14.182.38"`

**Question 5.5 –** What is the number of events that originated from all countries except France?

**Answer 5.5 –** 2814

**Explanation 5.5 –** `source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" Source_Country!=France`

**Question 5.6 –** How many VPN Events were observed by the IP 107.3.206.58?

**Answer 5.6 –** 14

**Explanation 5.6 –** `source="VPNlogs.json" host="VPN_Connections" index="vpn_logs" sourcetype="_json" Source_ip="107.3.206.58"`

![](\content\2023-02-07-tryhackme-walkthrough-splunk-basics\2023-02-07-tryhackme-walkthrough-splunk-basics-task-5.png)

#### Task 6 – Conclusion

**Task 6.1 –** Read through this section.

**Question 6.1 –** Join the next room.

**Answer 6.1** **–** Click the **Completed** button to complete this room.