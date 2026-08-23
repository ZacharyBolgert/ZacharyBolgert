## Hello, I'm Zachary Bolgert
Cybersecurity & Digital Forensics gradate (Cum Laude) from Stevenson University, based in Culpeper, VA. Focused on incident response, vulnerability management, and digital forensics; currently seeking an entry-level cybersecurity role.  

## Certifications 
-CompTIA Security + (SYO-701)

-CDFAE Digital Forensics Examiner - DoD Cyber Crime Center (DC3) / Stevenson University 

-CDFAE Digital Media Collector - DoD Cyber Crime Center (DC3) / Stevenson University 

## Featured Projects
## Digital Forensic Case Study - AfricanFalls (CyberDefenders)

This project documents a digital forensics investigation of the "AfricanFalls" case from CyberDefenders — a laptop disk image belonging to a suspect accused of illegal activity. The investigation follows a formal forensic workflow using Autopsy to verify evidence integrity, recover artifacts, and reconstruct the suspect's digital activity, including browsing history, deleted files, stored credentials, and network reconnaissance behavior.

Challenge source:
- https://cyberdefenders.org/blueteam-ctf-challenges/africanfalls/
## Tools Used 
- VirtualBox (Windows 11 VM environment)
- FTK Imager
- DB Browser for SQLite
- Autopsy

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

Investigated using the following views/tools: (e.g. tool bar, status bar, details)
<img width="380" height="309" alt="Screenshot 2026-08-23 124838" src="https://github.com/user-attachments/assets/eb0fb386-ba42-46f7-a077-c7f0a2d50fce" />

## Findings
1. Browsing History & Search Activity
- What was found: Brave keyword_search_terms table showing searches for steganography, secure file deletion, and encrypted messaging apps.
- Significance: Indicates deliberate attempts to hide data and cover digital tracks.
<img width="726" height="401" alt="SQLite Keyword Search Term " src="https://github.com/user-attachments/assets/04c0947e-c8a6-400f-bc65-cf98681dbbd6" />

- What was found: Chrome keyword_search_terms table showing searches for network attack tools (nmap, ettercap, bettercap, ARP spoofing, Wireshark), password/credential cracking (rockyou, password cracking lists, cain & abel), Tor, and IP-hiding methods.
- Significance: Shows research and preparation for network attacks and anonymized/untraceable access.
<img width="747" height="844" alt="SQLite" src="https://github.com/user-attachments/assets/88c07aea-7788-4db0-ad8d-ee12fb163341" />

2. Deleted Files / Recovered Data
What was found:
Significance:

3. Stored Credentials / Password Exposure
What was found:
Significance:

4. Network Reconnaissance / Scanning Activity
What was found (e.g. port scanning tools, Tor usage):
Significance:

**Timeline**
Date/Time	Event

**Conclusion**

**Skills Demonstrated**




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
