#### NICE Framework

**NICE Framework Category:** Collect and Operate  
**NICE Specialty Area:** Cyber Operations  
**NICE Work Role:** Cyber Operator  
**NICE Task Description:** Exploit network devices, security devices, and/or terminals or environments using various methods or tools. (T0696)  

#### DoD Cyber Workforce Framework (DCWF)

**DCWF Element:** Cyber Effects  
**DCWF Work Role:** Access Network Operator  
**DCWF Task Description:** Exploit network devices, security devices, and/or terminals or environments using various methods or tools. (2408)

Challenge difficulty: 1.5/3 stars

OS: Linux
#### Scenario

Your mission in this CISA Threat Sandbox Challenge is to learn about CVE-2021-35464, a dangerous remote code execution (RCE) vulnerability, and then exercise that knowledge along with your offensive and defensive cyber skills. You will be provided with real-world, authoritative reference materials that cover details critical to understanding the offensive and defensive angles of this CVE. After learning about the CVE, you will be asked to complete two technical objectives, one red team (offensive) and one blue team (defensive), related to the CVE:  
  
Red Team (Offensive) Objective: Utilize CVE-2021-35464 to deploy command and control (C2) enabled malware on a system running a vulnerable ForgeRock OpenAM instance used by an information technology (IT) business (i.e., the red target system).  

Blue Team (Defensive) Objective: Implement a known mitigation method for CVE-2021-35464 to safeguard a server running a vulnerable OpenAM instance used by an information technology (IT) business (i.e., the blue target system).  

#### Meeting Briefing
![[Pasted image 20250510175109.png]]
![[Pasted image 20250510175131.png]]

`Doc Scurlock` Hello @playerone, welcome to the mission briefing for the CVE‐2021‐35464 "ForgeRock OpenAM Backstage Pass" Threat Sandbox. During this mission, you will be providing ethical hacking services, similar to penetration testing and security remediation, to a fictional technology company within the information technology (IT) critical infrastructure (CI) sector.

`Doc Scurlock` Your mission in this threat sandbox will be to familiarize yourself with CVE‐2021‐35464 from an offensive (i.e., red team) and a defensive (i.e., blue team) perspective and then use that knowledge along with your cybersecurity skills to exploit and implement a protective mitigation on the company's systems vulnerable to CVE‐2021‐35464.

`Doc Scurlock` Before we get to your specific objectives, let's cover some of the basic details of CVE‐2021‐35464...

`Doc Scurlock` CVE‐2021‐35464 is a dangerous remote code execution (RCE) vulnerability that scores a 9.8/10 (Critical) severity rating on the common vulnerability scoring system (CVSS). It affects specific versions of the software "ForgeRock OpenAM" (It additionally affects the paid-for version of this software, ForgeRock AM), an access management tool for authentication and authorization, which is part of ForgeRock's Open Identity Platform (ForgeRock has since merged with Ping Identity which may result in the renaming of these software products) and is most commonly used in the information technology critical infrastructure sector.

`Doc Scurlock` Following its discovery, CVE-2021-35464 saw exploitation in the wild by a diverse set of dangerous cyber threat actors. A vulnerability needs to be pretty bad to make it into a major cybersecurity advisory. CVE-2021-35464 made it into at least two major Cybersecurity Advisories (CSA), including the 2021 Top Routinely Exploited Vulnerabilities joint CSA and the Critical ForgeRock Access Management Vulnerability CISA Alert CSA. The joint CSA was put out by major cybersecurity government agencies from around the world, including those from within the USA, such as the Cybersecurity and Infrastructure Security Agency (CISA), the Federal Bureau of Investigation (FBI), and the National Security Agency (NSA). You can take a look at that CISA Alert CSA (i.e., Critical ForgeRock Access Management Vulnerability) here: https://www.cisa.gov/news-events/alerts/2021/07/12/critical-forgerock-access-management-vulnerability

`Doc Scurlock` CVE‐2021‐35464 was added to CISA's Known Exploited Vulnerabilities (KEV) Catalog, a maintained and authoritative source of vulnerabilities that have been confirmed to have been exploited in the wild, on November 3, 2021. You can review CISA's KEV Catalog here: https://www.cisa.gov/known-exploited-vulnerabilities-catalog

`Doc Scurlock` For those organizations that did not or could not protect their systems from this vulnerability, they saw parts of their most critical operational and security infrastructure, their access and identity management solution, exploited. Once exploited, threat actors deployed command and control (C2) enabled malware and other malicious tools that they likely used to extract valuable digital credentials, attack additional systems, and deploy ransomware.

`Doc Scurlock` Now that you have a basic understanding of the vulnerability and the stakes of compromise let's get onto the details of your mission...

`Doc Scurlock` Your first objective will be to act as the attacker (red team) and utilize CVE‐2021‐35464 to deploy a C2 listener on the vulnerable "Red Target" system, a clone of the system running the company's OpenAM instance.

`Doc Scurlock` To read up on the technical exploitation details of CVE‐2021‐35464, we suggest you review the following AttackerKB topic: https://attackerkb.com/topics/KnAX5kffui/pre-auth-rce-in-forgerock-access-manager-cve-2021-35464/rapid7-analysis

`Doc Scurlock` Once you've got a handle on how the vulnerability works in principle, you must use the provided "Security-Desk" machine to take advantage of CVE‐2021‐35464 and deploy a C2 listener on the vulnerable "Red Target" system. The "Red Target" system is running a vulnerable version and configuration of OpenAM on port 80.

`Doc Scurlock` For this part of the mission, the "Security-Desk" machine has been configured to include the following to enable your ability to complete the mission: Metasploit, the "cve_2021_35464_forgerock_openam" exploit module in Metasploit, and a "deploy_c2" executable file (available on the Desktop in the Resources folder) that will deploy a C2 listener when executed. While other software and utilities are available on the "Security-Desk" machine, they may or may not assist you in accomplishing this part of the mission.

`Doc Scurlock` Your second objective will be to act as the defender (blue team) and protect the vulnerable "Blue Target" system, another clone of the system running the company's OpenAM instance. You will protect this system's installation of OpenAM by employing the OpenAM maintainer's official mitigation method to prevent RCE via CVE‐2021‐35464. While it is almost always preferable to patch vulnerable software instead of using mitigation techniques, patches are not always available right after a vulnerability is made public. Additionally, patching can sometimes require costly downtime, which organizations often must schedule in advance, making mitigations valuable stopgap solutions.

`Doc Scurlock` You can find the mitigation method to prevent RCE via CVE‐2021‐35464 in the ForgeRock OpenAM maintainer's official security advisory for CVE‐2021‐35464 at the following link: https://backstage.forgerock.com/knowledge/kb/article/a47894244 While the maintainer provides two workaround (i.e., mitigation) options, during this mission you should use "Workaround Option 1" to disable the VersionServlet mapping.

`Doc Scurlock` To implement the necessary mitigation for this mission, you must use the provided "Security-Desk" machine to access the vulnerable "Blue Target" system and complete the steps needed to implement the RCE mitigation. The "Blue Target" system is running the vulnerable version of OpenAM, is running SSH on port 22, and you have a privileged user account on the system that can be accessed via SSH using the same credentials as you use to access the "Security-Desk" machine.

`Doc Scurlock` For this part of the mission, the "Security-Desk" machine has been configured to include the following to enable your ability to complete the mission: SSH. While other software and utilities are available on the "Security-Desk" machine, they may or may not assist you in accomplishing this part of the mission.

`Doc Scurlock` The part of the OpenAM installation on the "Blue Target" system that contains the XML file involved in the RCE mitigation is within the directory "/usr/local/tomcat/webapps/openam/WEB-INF/". The objective will be satisfied once the RCE mitigation is correctly implemented, which does not require restarting the "Blue Target" or any services associated with the OpenAM installation.

`Doc Scurlock` Good luck, and enjoy the mission! We look forward to your success.

****end mission brief****
##### Information on CVE-2021-35464

[NIST National Vulnerability Database. CVE-2021-35464](https://nvd.nist.gov/vuln/detail/CVE-2021-35464). National Institute of Standards and Technology. Accessed May 10, 2025.

ForgeRock AM server before 7.0 has a Java deserialization vulnerability in the jato.pageSession parameter on multiple pages. The exploitation does not require authentication, and remote code execution can be triggered by sending a single crafted /ccversion/* request to the server. The vulnerability exists due to the usage of Sun ONE Application Framework (JATO) found in versions of Java 8 or earlier. This vulnerability scores a 9.8/10 (critical) on the Common Vulnerability Scoring System (CVSS).

###### What is deserialization/serialization?

Serialization is the process of converting data from an in-memory object into a format that can be transmitted (stream of bytes), written to a file (JSON, YAML), or stored in a DB (BLOBs). Deserialization reconstructs this processed data to convert the data back into a usable object or data structure in a program. 

###### Insecure deserialization vulnerability

In applications that deserialize user-input without proper validation an attacker can send a malicious serialized payload. If the application's classpath includes classes that can be chained together (gadgetchain), deserialization may invoke methods that lead to remote code execution, especially if reflection is used internally (i.e. vulnerable methods like InvokeTransformer from the Apache Commons Collection). 

#### Red Team exercise

My first action was to run a nmap scan against the target machine @ 172.16.100.90. I decided that since this is a test environment i'd go the fast and hard route. 

![[Pasted image 20250510194141.png]]

This confirmed that the target has Apache Tomcat 8.5.68 running on port 80. 

The challenge has provided that we are seeking to exploit CVE-2021-35464. As such, I opened the metasploit console and used the CVE search to find modules particular to this vulnerability. 

![[Pasted image 20250510194457.png]]

Any time I load a tool I check options to ensure that I have entered all required fields for the tool/module to function properly. The values that I need to set for this particular module are RHOST (remote host) 172.16.100.90, RPORT (remote port) 80, and LHOST (local host) 172.16.200.12. 

![[Pasted image 20250510194731.png]]

![[Pasted image 20250510195001.png]]

afterwards I do like to run "show options" once more for the sake of measuring twice and cutting once but i'll spare the screenshot

after the necessary fields have been confirmed we pass 'exploit' and like magic we have a meterpreter session. 

![[Pasted image 20250510195424.png]]

From here we can upload our deploy_c2 ELF binary and check that the upload was successful (i'll double check despite metasploit telling us it was)

![[Pasted image 20250510195943.png]]

Last step of this red team exercise is to pop into a shell from our meterpreter session and execute the deploy_c2 binary. passing pwd first would have been more efficient so next time i'll be saving myself a step there

![[Pasted image 20250510200954.png]]


#### Blue team exercise

For our blue team exercise we are tasked with implementing the vendor-provided mitigation on a vulnerable machine @ 172.16.100.100. 

To do so i've first ssh'd into the machine using the given credentials for a privileged account

![[Pasted image 20250510202131.png]]

Per the vendor, mitigation can be achieved by making an edit to comment out the VersionServlet/ccversion portion of _/path/to/tomcat/webapps/openam/WEB-INF/web.xml_

I edited the file with nano and commented it out with the proper '<!-- -->' for xml.

![[Pasted image 20250510212023.png]]

It seems like the characters are malformed given the Unicode long dash and ^M characters when opening in vim to denote a windows-style CRLF but apparently this is sufficient for this challenge. 

[ForgeRock Security Advisory: AM Remote Code Execution Vulnerability (CVE-2021-35464)](https://backstage.forgerock.com/knowledge/advisories/book/b21824339#a47894244). ForgeRock. Accessed May 10, 2025.



README.md format reference citation:
@misc{Ednas},
  title = {35SecurityBegins},
  year = {2022},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/Ednas/WriteUps/tree/main/NICEChallenge/35SecurityBegins}},
  }


