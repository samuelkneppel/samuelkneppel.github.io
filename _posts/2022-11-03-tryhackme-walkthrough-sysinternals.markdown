---
layout: post
title:  "TryHackMe Walkthrough - Sysinternals"
date:   2022-11-03 01:00:00 -0400
categories: microsoft sysinternals tryhackme walkthrough windows
---

![](\content\2022-11-03-tryhackme-walkthrough-sysinternals\2022-11-03-tryhackme-walkthrough-sysinternals.png)

#### Introduction

The purpose of this article is to document my journey through the TryHackMe platform. This article will contain answers to the questions provided along with the thought process as to how I obtained them. I will also include any additional notes along the way.

This [room](https://tryhackme.com/room/btsysinternalssg) was created in order to teach one how to use the Sysinternals tools to analyze Window systems or applications.

**NOTE:** Only subscribers to TryHackMe are allowed to access this room. If you would like to subscribe to TryHackMe, sign up [here](https://tryhackme.com/why-subscribe).

**ADDITIONAL:** Some commands you will be running require an Internet connection, which the virtual machine provided does not have. In those cases, you can either resort to using another Windows VM, another Windows device, or your personal Windows device, as long as the device you use has an Internet connection.

#### **Task 1: Introduction**

**Task 1.1 –** Read through this section. All the answers to the following questions can be found within this section.

**Task 1.2 –** Click **Start Machine** to start the machine.

**Task 1.3 –** RDP into the machine via it’s IP address and login using the credentials `administrator:letmein123!`. Alternatively, you can use the build-in AttackBox if you would prefer.

**Question 1.1 –** When did Microsoft acquire the Sysinternals tools?

**Answer 1.1 –** 2006

**Question 1.2 –** I deployed the attached virtual machine and I’m ready to move on…

**Answer 1.2 –** Click the **Submit** button to progress to the next task.

#### **Task 2: Install the Sysinternals Suite**

**Task 2.1 –** Read through this section. All the answers to the following questions can be found within this section.

**Question 2.1 –** What is the last tool listed within the Sysinternals Suite?

**Answer 2.1 –** ZoomIt

#### **Task 3: Using Sysinternals Live**

**Task 3.1 –** Read through this section. All the answers to the following questions can be found within this section.

**Question 3.1 –**  What service needs to be enabled on the local host to interact with live.sysinternals.com?

**Answer 3.1 –** webclient

#### **Task 4: File and Disk Utilities**

**Task 4.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 4.1 –** There is a txt file on the desktop named file.txt. Using one of the three discussed tools in this task, what is the text within the ADS?

**Answer 4.1 –** I am hiding in the stream.

#### **Task 5: Networking Utilities**

**Task 5.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 5.1 –**  Using WHOIS tools, what is the ISP/Organization for the remote address in the screenshots above?

**Answer 5.1 –** Microsoft Corporation

#### **Task 6: Process Utilities**

**Task 6.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 6.1 –**  Run Autoruns and inspect what are the new entries in the Image Hijacks tab compared to the screenshots above.

**Answer 6.1 –** Click the **Completed** button to progress to the next task.

**Question 6.2 –**  What entry was updated?

**Answer 6.2 –** `taskmgr.exe`

**Question 6.3 –** What is the updated value?

**Answer 6.3 –** `C:\TOOLS\SYSINT\PROCEXP.EXE`

#### **Task 7: Security Utilities**

**Task 7.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section.

**Question 7.1 –** You will check out the Sysmon room if you haven’t done so already…

**Answer 7.1 –** Click the **Completed** button to progress to the next task.

#### **Task 8: System Information**

**Task 8.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section.

**Question 8.1 –** Moving along…

**Answer 8.1 –** Click the **\*\*Completed** button to progress to the next task.

#### **Task 9: Miscellaneous**

**Task 9.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section as well as within the machine you are connected to.

**Question 9.1 –** Run the Strings tool on ZoomIt.exe. What is the full path to the .pdb file?

**Answer 9.1 –** \`C:\\agent\\\_work\\112\\s\\Win32\\Release\\ZoomIt.pdb\`

**Explanation 9.1 –** I had a little bit of extra help with this question. It looks like the current version of `ZoomIt.exe` available online as well as in the VM provided lists the `.pdb` file location as `D:\a\1\s\Win32\Release\ZoomIt.pdb`, not `C:\agent\_work\112\s\Win32\Release\ZoomIt.pdb`. I had to reference another write-up blog post online in order to find the answer the writer was looking for.

#### **Task 10: Conclusion**

**Task 10.1 –** Read through this section and complete the tasks outlined. All of the answers to the following questions can be found within this section.

**Question 10.1 –** I will definitely look into Sysinternals more in-depth and add this to my arsenal…

**Answer 10.1 –** Click the **Completed** button to complete this room.

#### **My Conclusion**

After completing this room, I have become much better acquainted with the Sysinternals suite of tools. Included below is a short list of the tools that were used during the course of completing this room as well as their official description from the Sysinternals website and example syntax.

*   **Sigcheck** – a command-line utility that shows file version number, timestamp information, and digital signature details, including certificate chains. It also includes an option to check a file’s status on VirusTotal, a site that performs automated file scanning against over 40 antivirus engines, and an option to upload a file for scanning
    *     Example syntax: `sigcheck -u -e C:\Windows\System32 -accepteula`
*   **Streams** – the NTFS file system provides applications the ability to create alternate data streams of information. By default, all data is stored in a file’s main unnamed data stream, but by using the syntax ‘file:stream’, you are able to read and write to alternates
    *    Example syntax: `streams C:\Users\Administrator\Desktop\SysinternalsSuite.zip -accepteula`
*   **SDelete** – a command line utility that takes a number of options. In any given use, it allows you to delete one or more files and/or directories, or to cleanse the free space on a logical disk
    *     Example syntax: `sdelete -p 3 -s C:\Users\Administrator\Directory -accepteula`
*   **TCPView** – TCPView is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. On Windows Server 2008, Vista, and XP, TCPView also reports the name of the process that owns the endpoint. TCPView provides a more informative and conveniently presented subset of the Netstat program that ships with Windows. The TCPView download includes Tcpvcon, a command-line version with the same functionality
*   **Whois** – Whois performs the registration record for the domain name or IP address that you specify
    *     Example syntax: `whois xxx.xxx.xxx.xxx -v -accepteula`
*   **Autoruns** –  shows you what programs are configured to run during system boot-up or login, and when you start various built-in Windows applications like Internet Explorer, Explorer and media players. These programs and drivers include ones in your startup folder, Run, RunOnce, and other Registry keys. Autoruns reports Explorer shell extensions, toolbars, browser helper objects, Winlogon notifications, auto-start services, and much more. Autoruns goes way beyond other auto-start utilities
*   **ProcDump** – a command-line utility whose primary purpose is monitoring an application for CPU spikes and generating crash dumps during a spike that an administrator or developer can use to determine the cause of the spike
    *     Example syntax: `procdump.exe notepad`
*   **Process Explorer** – consists of two sub-windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that Process Explorer is in: if it is in handle mode you’ll see the handles that the process selected in the top window has opened; if Process Explorer is in DLL mode you’ll see the DLLs and memory-mapped files that the process has loaded
*   **Process Monitor** – Process Monitor is an advanced monitoring tool for Windows that shows real-time file system, Registry and process/thread activity. It combines the features of two legacy Sysinternals utilities, Filemon and Regmon, and adds an extensive list of enhancements including rich and non-destructive filtering, comprehensive event properties such as session IDs and user names, reliable process information, full thread stacks with integrated symbol support for each operation, simultaneous logging to a file, and much more. Its uniquely powerful features will make Process Monitor a core utility in your system troubleshooting and malware hunting toolkit
*   **PsExec** – a light-weight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software. PsExec’s most powerful uses include launching interactive command-prompts on remote systems and remote-enabling tools like IpConfig that otherwise do not have the ability to show information about remote systems
    *     Example Syntax: `psexec -i \\remote-device cmd`
*   **Sysmon** – System Monitor (Sysmon) is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time. By collecting the events it generates using Windows Event Collection or SIEM agents and subsequently analyzing them, you can identify malicious or anomalous activity and understand how intruders and malware operate on your network
*   **WinObj** – a 32-bit Windows NT program that uses the native Windows NT API (provided by `NTDLL.DLL`) to access and display information on the NT Object Manager’s name space
*   **BgInfo** – automatically displays relevant information about a Windows computer on the desktop’s background, such as the computer name, IP address, service pack version, and more
*   **RegJump** – command-line applet that takes a registry path and makes Regedit open to that path. It accepts root keys in standard (e.g. `HKEY_LOCAL_MACHINE`) and abbreviated form (e.g. `HKLM`)
    *    Example syntax – `regjump HKLM\System\CurrentControlSet\Services\WebClient`
*   **Strings** – scans the file you pass it for UNICODE (or ASCII) strings of a default length of 3 or more UNICODE (or ASCII) characters. Note that it works under Windows 95 as well
    *     Example syntax – `strings.exe C:\Windows\System32\notepad.exe`

**Reference:** [TryHackMe Sysinternals](https://tryhackme.com/room/btsysinternalssg), [Sysinternals – Sysinternals - Microsoft Learn](https://learn.microsoft.com/en-us/sysinternals/)