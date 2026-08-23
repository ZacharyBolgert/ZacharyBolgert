## Hello, I'm Zachary Bolgert
Cybersecurity & Digital Forensics gradate (Cum Laude) from Stevenson University, based in Culpeper, VA. Focused on incident response, vulnerability management, and digital forensics; currently seeking an entry-level cybersecurity role.  

## Certifications 
-CompTIA Security + (SYO-701)

-CDFAE Digital Forensics Examiner - DoD Cyber Crime Center (DC3) / Stevenson University 

-CDFAE Digital Media Collector - DoD Cyber Crime Center (DC3) / Stevenson University 

## Featured Projects
## Digital Forensic Case Study - AfricanFalls (CyberDefenders)

This project documents a digital forensics investigation of the "AfricanFalls" case from CyberDefenders — a laptop logical forensic image belonging to a suspect accused of illegal activity. The investigation follows a formal forensic workflow using FTK Imager to verify evidence integrity, recover artifacts, and reconstruct the suspect's digital activity, including browsing history, deleted files, stored credentials, and network reconnaissance behavior.

Challenge source:
- https://cyberdefenders.org/blueteam-ctf-challenges/africanfalls/
## Tools Used 
- VirtualBox (Windows 11 VM environment)
- FTK Imager
- DB Browser for SQLite
- DCode (version 5.7)
- Timeline Explorer (version 2026.5.0)
- PECmd

## Case Information 

## Field            |      Detail 

Case Number         | 001 

Examiner            | Zachary Bolgert

Date of Examination | 8/22/2026

Evidence Source     | CyberDefenders — AfricanFalls (public blue team CTF challenge)

Evidence Description | Laptop logical forensic image, suspect "John Doe"

## Chain of Custody / Evidence Integrity
Source: https://cyberdefenders.org/blueteam-ctf-challenges/africanfalls/

Acquisition method: downloaded, added as data source in FTK Imager 

Hash value (MD5/SHA1): 
- MD5: 9471e69c95d8909ae60ddff30d50ffa1
- SHA1: 167aa08db25dfeeb876b0176ddc329a3d9f2803a
<img width="787" height="259" alt="AfricanFalls Hash Values" src="https://github.com/user-attachments/assets/90adb232-0e3d-4e38-9f91-0dd695af7e13" />
Integrity confirmed: Yes, I verified the logical forensic image (DiskDrigger.ad1) using FTK Imager   

## Methodology
Added Evidence Item using FTK Imager, selected source evidence type (Image File)

Added logical forensics image as data source

Verified logical forensic image using verify drive/image

Investigated using the following views/tools: (FTK Imager for browsing/export, DB Browser for SQLite, DCode, Timeline Explorer, PECmd)

<img width="380" height="309" alt="Screenshot 2026-08-23 124838" src="https://github.com/user-attachments/assets/eb0fb386-ba42-46f7-a077-c7f0a2d50fce" />

## Findings
1. Browsing History & Search Activity
- What was found: Brave keyword_search_terms table showing searches for steganography, secure file deletion, and encrypted messaging apps.
- Significance: Indicates deliberate attempts to hide data and cover digital tracks.
<img width="726" height="401" alt="SQLite Keyword Search Term " src="https://github.com/user-attachments/assets/04c0947e-c8a6-400f-bc65-cf98681dbbd6" />

- What was found: Chrome keyword_search_terms table showing searches for network attack tools (nmap, ettercap, bettercap, ARP spoofing, Wireshark), password/credential cracking (rockyou, password cracking lists, cain & abel), Tor, and IP-hiding methods.
- Significance: Shows research and preparation for network attacks and anonymized/untraceable access.
<img width="747" height="844" alt="SQLite" src="https://github.com/user-attachments/assets/88c07aea-7788-4db0-ad8d-ee12fb163341" />

- What was found: Brave urls table showing YouTube tutorials and site visits on hacking passwords with Kali Linux, ethical hacking, WiFi network attacks, OSINT phone lookups, steganography (including QuickStego software and JPHS), Shodan searches for vulnerable devices, and encrypted/anonymous messaging apps.
- Significance: Confirms active research and tool-seeking beyond search terms alone — shows the suspect visited tutorial content and software download pages, indicating intent to acquire and use these tools, not just casual searching.
<img width="721" height="715" alt="SQLite Urls" src="https://github.com/user-attachments/assets/de723d79-8331-4a09-8981-2fe84be97f7c" />

- What was found: Chrome urls table showing downloads of Cain & Abel password cracking tool, Tor Browser download and install, IP address hiding guides, and password wordlists from SecLists on GitHub (rockyou, common credentials, 10-million password lists).
- Significance: Shows the suspect actually downloaded password-cracking tools and wordlists, and installed Tor for anonymity — moving beyond research into active tool acquisition for cracking credentials and hiding identity.
<img width="742" height="738" alt="SQL URls table" src="https://github.com/user-attachments/assets/7759013e-65b5-4260-85bf-d861314e8913" />


2. Deleted Files / Recovered Data
- What was found: Recycle Bin metadata ($I/$R file pair) revealing a deleted file originally located at C:\Users\John Doe\Downloads\10-million-password-list-top-100.txt, deleted 4/29/2021.
- Significance: Shows the suspect downloaded a password cracking wordlist and later deleted it — an attempt to remove evidence of password cracking activity, though the file remained recoverable in the Recycle Bin.
<img width="988" height="592" alt="passwords" src="https://github.com/user-attachments/assets/3279302f-c26c-4f10-95e9-6c820486f54c" />

- What was found: Recovered content of the deleted $RW9BJ2Z.txt file from Recycle Bin, confirmed to be the actual "10-million-password-list-top-100.txt" wordlist — a list of common passwords (123456, password, qwerty, dragon, monkey, etc.).
- Significance: Directly confirms the deleted file was a real password cracking wordlist, not just a suspiciously-named file — full content recovery proves the suspect possessed and later attempted to hide password-cracking material.
<img width="1022" height="809" alt="image" src="https://github.com/user-attachments/assets/02c2116e-842e-41f1-b723-b825ebac86ca" />

3. Anonymous/Encrypted Communications
- What was found: Browser history showing searches for ProtonMail (encrypted email service) and login/inbox activity for a ProtonMail account (dreammaker82@protonmail.com).
- Significance: Shows the suspect set up and actively used an encrypted, harder-to-trace email account — consistent with the broader pattern of seeking anonymous communication channels alongside the earlier "secure messaging app" searches, further supporting intent to conceal identity and communications.
<img width="573" height="266" alt="email" src="https://github.com/user-attachments/assets/2bff9499-42f4-49bf-86ed-7a61aeb7bc13" />


4. Network Activity / FTP Client Configuration
- What was found: FileZilla recentservers.xml configuration file showing a saved FTP connection to host 192.168.1.20 on port 21, using username "kali."
- Significance: Confirms FileZilla (FTP client) was installed and actively configured to connect to a host on the local network using the username "kali" — suggesting a connection to a Kali Linux machine, potentially for transferring files off the system or coordinating with attack tooling. This is a strong piece of evidence tying the suspect's activity to broader network compromise/exfiltration behavior, not just isolated research.
<img width="1016" height="717" alt="recent servers" src="https://github.com/user-attachments/assets/3fef0270-808c-4cc6-8141-54351e4fa799" />

5. Timeline Reconstruction / Timestamp Analysis
- What was found: Chromium timestamp (13264194013047881) from the browser history decoded via DCode, confirming the exact UTC date/time the "10-million-password-list-top-1000000.txt" file was downloaded.
- Significance: Establishes a precise, verified timestamp for this download — ties directly to the earlier password wordlist finding and strengthens the timeline by showing exactly when the suspect acquired that file.
<img width="1024" height="951" alt="Time stamp" src="https://github.com/user-attachments/assets/6f4bc80c-a5b1-49bd-8a68-7f1cbf257142" />

6. Program Execution Evidence
- What was found: PECmd/Prefetch analysis shows TORBROWSER-INSTALL-WIN64-10.0.exe was executed on 2021-04-29 18:22:32 UTC — confirming the Tor Browser installer was run on the system.
- Significance: Supports the earlier browser history findings (Tor searches and download) with proof the installer was actually executed, not just downloaded. Confirms progression from research → download → installation.
<img width="1022" height="604" alt="Tor" src="https://github.com/user-attachments/assets/7a5c89ed-867d-4944-8d66-ff2fb5ab5c73" />
<img width="1029" height="845" alt="Prefetch " src="https://github.com/user-attachments/assets/caa32fe4-3ba0-486c-b484-825185ef2fb4" />

7. Command Execution History / Network Reconnaissance
- What was found: ConsoleHost_history.txt (PowerShell command history) revealing actual commands executed, including bettercap (network attack tool, run with --no-spoofing, -caplet http-ui), nmap scans against local subnet ranges (10.0.2.1-254) and the domain dfir.science, and multiple sdelete commands targeting specific files/folders including .\accountNum and .\accountNum.zip.
- Significance: Provides direct, command-level proof — not just search history — that the suspect actively ran network scanning and attack tools (nmap, bettercap) against the local network, and used secure deletion (sdelete) specifically on a file/folder named "accountNum," suggesting an attempt to permanently destroy financial or account-related evidence.
<img width="1016" height="883" alt="Command line" src="https://github.com/user-attachments/assets/0ed30b1d-c327-4800-9753-63f0670a4d56" />

## Conclusion
- This investigation of the AfricanFalls disk image reveals a clear and escalating pattern of malicious intent. The suspect progressed from researching network attack tools, password cracking methods, and anti-forensic techniques, to actively downloading and installing this software (Cain & Abel, Tor Browser, password wordlists), to executing real attacks and reconnaissance against the local network (nmap, bettercap). Evidence of FTP configuration to a Kali Linux host suggests coordinated exfiltration or attack activity, while the targeted deletion of a file specifically named "accountNum" indicates an attempt to destroy evidence related to financial account compromise. Combined with the suspect's use of encrypted communications (ProtonMail) and anonymization tools (Tor), the evidence supports the conclusion that John Doe engaged in deliberate, premeditated illegal network activity and took active steps to conceal it. All artifacts were recoverable despite deletion attempts, demonstrating the value of forensic recovery techniques even against anti-forensic behavior.
## Skills Demonstrated
- Forensic image acquisition and integrity verification (FTK Imager, hash validation)
- SQLite database analysis for browser artifact recovery (DB Browser for SQLite)
- Deleted file recovery and Recycle Bin metadata analysis
- Timestamp decoding and timeline reconstruction (DCode, Timeline Explorer)
- Program execution analysis via Prefetch parsing (PECmd)
- PowerShell command history analysis
- Network artifact analysis and correlation across multiple evidence sources
- Formal chain-of-custody and forensic report documentation



## Home SOC Detection Lab

Multi-VM lab (Security Onion, Kali Linux, Metasploitable2) simulating a network attack and detecting it via Suricata/Zeek/Kibana, with a Teir-1-style incident triage writeup. (Currently in progress)  

## Tools & Skills 
Forensics: Autopsy, FTK Imager

Security Monitoring: Security Onion, Suricata, Zeek, Kibana

Networking: Wireshark, GNS3, TCP/IP, packet analysis

Systems: Windows, Kali Linux =, Ubuntu Linux, VirtualBox 

## Connect
- <a href="www.linkedin.com/in/zachary-bolgert-77338837b">LinkedIn</a>
- Email: ZacharyBolgert1@gmail.com
