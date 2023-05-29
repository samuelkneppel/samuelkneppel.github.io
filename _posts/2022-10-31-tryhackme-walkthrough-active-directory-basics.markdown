---
layout: post
title:  "TryHackMe Walkthrough - Active Directory Basics"
date:   2022-10-31 01:00:00 -0400
categories: active-directory ad microsoft tryhackme walkthrough windows
---
![](\content\2022-10-31-tryhackme-walkthrough-active-directory-basics\2022-10-31-tryhackme-walkthrough-active-directory-basics.png)

#### **Introduction**

The purpose of this article is to document my journey through the TryHackMe platform. This article will contain answers to the questions provided along with the thought process as to how I obtained them. I will also include any additional notes along the way.

This [room](https://tryhackme.com/room/winadbasics) is an introduction to Active Directory and the different technologies associated with it.

#### **Task 1: Introduction**

**Task 1.1 –** Read through this section.

**Question 1.1 –** Click the **Submit** button to progress to the next task.

#### **Task 2: Windows Domains**

**Task 2.1 –** Click **Start Machine** to start the machine.

**Task 2.2 –** Read through this section. All the answers to the following questions can be found within this section.

**Task 2.3 –** RDP into the machine via it’s IP address and login using the credentials `Administrator:Password321`. Alternatively, you can use the build-in AttackBox if you would prefer.

Question 2.1 – In a Windows domain, credentials are stored in a centralized repository called…

**Answer 2.1 –** Active Directory

**Question 2.2 –** The server in charge of running the Active Directory services is called…

**Answer 2.2 –** Domain Controller

#### **Task 3: Active Directory**

**Task 3.1 –** Read through this section and complete all of the tasks outlined. All the answers to the following questions can be found within this section.

**Question 3.1 –** Which group normally administrates all computers and resources in a domain?

**Answer 3.1 –** Domain Admins

**Question 3.2 –** What would be the name of the machine account associated with a machine named TOM-PC?

**Answer 3.2 –** TOM-PC$

**Question 3.3 –** Suppose our company creates a new department for Quality Assurance. What type of containers should we use to group all Quality Assurance users so that policies can be applied consistently to them?

**Answer 3.3 –** Organizational Units (OUs)

#### **Task 4: Managing Users in AD**

**Task 4.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 4.1 –** What was the flag found on Sophie’s desktop?

**Answer 4.1 –** THM{thanks\_for\_contacting\_support}

**Question 4.2 –** The process of granting privileges to a user over some OU or other AD Object is called…

**Answer 4.2 –** delegation

#### **Task 5: Managing Computers in AD**

**Task 5.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 5.1** – After organizing the available computers, how many ended up in the Workstations OU?

**Answer 5.1 –** 7

**Question 5.2 –** Is it recommendable to create separate OUs for Servers and Workstations? (yay/nay)

**Answer 5.2 –** yay

#### **Task 6: Group Policies**

**Task 6.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 6.1 –** What is the name of the network share used to distribute GPOs to domain machines?

**Answer 6.1 –** sysvol

**Question 6.2 –** Can a GPO be used to apply settings to users and computers? (yay/nay)

**Answer 6.2 –** yay

#### **Task 7: Authentication Methods**

**Task 7.1 –** Read through this section. All of the answers to the following questions can be found within this section.

**Question 7.1 –**  Will a current version of Windows use NetNTLM as the preferred authentication protocol by default? (yay/nay)

**Answer 7.1 –** nay

**Question 7.2 –** When referring to Kerberos, what type of ticket allows us to request further tickets known as TGS?

**Answer 7.2 –** Ticket Granting Ticket

**Question 7.3 –** When using NetNTLM, is a user’s password transmitted over the network at any point? (yay/nay)

**Answer 7.3 –** nay

#### **Task 8: Trees, Forests, and Trusts**

**Task 8.1 –** Read through this section. All of the answers to the following questions can be found within this section.

**Question 8.1 –**  What is a group of Windows domains that share the same namespace called?

**Answer 8.1 –** Tree

**Question 8.2 –** What should be configured between two domains for a user in Domain A to access a resource in Domain B?

**Answer 8.2 –** A Trust Relationship

#### **Task 9: Conclusion**

**Task 9.1 –** Read through this section.

**Question 9.1 –** Click the **Completed** button to complete this room.

#### **My Conclusion**

At this point, I have gained a solid foundational knowledge of Active Directory and the different technologies associated with it.

**Reference:** [TryHackMe - Active Directory Basics](https://tryhackme.com/room/winadbasics)