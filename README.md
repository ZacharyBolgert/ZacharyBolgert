## Hello, I'm Zachary Bolgert
Cybersecurity & Digital Forensics graduate (Cum Laude) from Stevenson University. Focused on incident response, vulnerability management, and digital forensics; currently seeking an entry-level cybersecurity role.  

## Certifications 
-CompTIA Security + (SY0-701)

-CDFAE Digital Forensics Examiner - DoD Cyber Crime Center (DC3) / Stevenson University 

-CDFAE Digital Media Collector - DoD Cyber Crime Center (DC3) / Stevenson University 

# Featured Projects
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

## Wazuh + Sysmon + Atomic Red Team Detection Lab

## Overview

A home lab built to practice endpoint detection engineering. I deployed a Wazuh SIEM manager, instrumented a Windows 11 endpoint with Sysmon for detailed telemetry, and enrolled it as a monitored agent. The next phase simulates real attacker techniques with Atomic Red Team and measures detection coverage against the MITRE ATT&CK framework.

## Architecture

Two VMs on an isolated internal network in VirtualBox:

| VM | Role | Software |
|---|---|---|
| Wazuh Manager | SIEM — indexer, manager, and dashboard (all-in-one install) | Ubuntu Server, Wazuh |
| Windows 11 Endpoint | Monitored agent, future attack simulation target | Windows 11, Sysmon, Wazuh agent |

**Software:**
- Wazuh (all-in-one install via the official install script)
- Sysmon, using the SwiftOnSecurity configuration ([SwiftOnSecurity's sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config))
- Atomic Red Team (to be used for attack simulation)

---

## Build Steps

### 1. Deployed the Wazuh manager
Installed Ubuntu Server and ran the official Wazuh all-in-one installer. Hit an early snag where the install script wasn't actually present in the working directory — the first download attempts pointed at the wrong URL (`wazuh.com` instead of the actual package host, `packages.wazuh.com/4.12/wazuh-install.sh`), which silently saved an error page instead of the script. Fixed by pulling the script from the correct URL and confirming it landed with `ls -la` before running the install.
<img width="1919" height="946" alt="image" src="https://github.com/user-attachments/assets/e97b478a-80a9-4e87-b97d-233547f34f18" />

### 2. Installed Sysmon on the Windows 11 endpoint
Installed Sysmon using the SwiftOnSecurity configuration to get detailed process-creation, network-connection, and registry telemetry beyond default Windows event logging.
<img width="966" height="449" alt="image" src="https://github.com/user-attachments/assets/1cbbb8af-6e5c-4ff3-8591-7d7135eb20f4" />

### 3. Enrolled the Windows VM as a Wazuh agent
Deployed the Wazuh agent from the manager's dashboard (pre-configured with the manager address and registration key) and confirmed the agent shows Active in the Wazuh dashboard, with Sysmon events flowing into Security Events.
<img width="1919" height="325" alt="image" src="https://github.com/user-attachments/assets/782a50d7-1197-424e-9a64-67b0c747501b" />

<img width="954" height="821" alt="image" src="https://github.com/user-attachments/assets/2ab76f46-ccdd-4e64-9d7d-2389375012c0" />

### 4. Attack simulation 
Installed Atomic Red Team on the Windows endpoint, resolving two setup issues along the way: a PowerShell execution-policy block that prevented a required module from loading, and a Windows Defender exclusion needed for the atomic test files (Defender flags them as suspicious by design, since they mimic real attacker behavior). Ran T1059.001-17 (PowerShell Command Execution) as the first simulated technique.
<img width="946" height="192" alt="image" src="https://github.com/user-attachments/assets/e8bdf56b-7250-441f-8117-4e6ca0ee327c" />


### 5. Detection tuning
Confirmed detection without writing any custom rules — Wazuh's default ruleset caught the PowerShell activity out of the box, including a level-12 alert for a PowerShell process spawning a base64-encoded command. Some events in the same window (rule 92203, "Executable file created by powershell") were Atomic Red Team installing its own test files rather than the technique itself — worth distinguishing actual technique signal from setup noise.
<img width="1919" height="871" alt="image" src="https://github.com/user-attachments/assets/a1930fad-9499-4488-9429-6d7c4eec9a7d" />

### 6. Simulated credential dumping (T1003.001)
Attempted T1003.001-2 (Dump LSASS.exe Memory using comsvcs.dll), a living-off-the-land technique that uses a built-in Windows DLL rather than an external tool. The attempt failed with "Access is denied" before the dump could occur. Checked Windows Security's Protection History and found no entry referencing this attempt, ruling out real-time Defender interception — the block is more likely explained by Windows' built-in LSASS Protected Process Light (PPL) hardening, which restricts memory access to lsass.exe even from an Administrator-level process. This is a stronger result than a clean detection: it shows OS-level hardening stopping credential-access activity before it produced any telemetry for Wazuh to catch.
<img width="709" height="266" alt="image" src="https://github.com/user-attachments/assets/0cd9d652-009a-4e9d-82a6-7d016b06d0dc" />

### 7. Simulated persistence (T1547.001)
Ran T1547.001-1 (Reg Key Run), which adds a registry Run key entry via `reg.exe` — the classic persistence technique for surviving reboots. Detected immediately and accurately by Wazuh's default ruleset: one rule specifically identified the registry modification via `reg.exe` for next-logon execution, and a second, higher-severity rule flagged the value's Base64-like pattern. Cleaned up the added registry key afterward using Atomic Red Team's built-in cleanup command.
<img width="1919" height="955" alt="image" src="https://github.com/user-attachments/assets/fb0228ba-99ee-444b-8412-ef68d6857869" />

## Detection Results

| ATT&CK Technique | Detected? | Rule ID | Notes |
|---|---|---|---|
| T1059.001 | Yes (default rule, no tuning needed) | 92057 | "Powershell.exe spawned a powershell process which executed a base64 encoded command" — level 12 alert |
| T1003.001 | Blocked pre-execution | N/A | "Access is denied" attempting to dump LSASS via comsvcs.dll — no corresponding Defender Protection History entry, indicating the block came from Windows' LSASS PPL hardening rather than antivirus |
| T1547.001 | Yes (default rule, no tuning needed) | 92302, 92041 | Registry Run key persistence via reg.exe — caught by both a technique-specific rule and a higher-severity Base64-pattern rule (level 10) |

## AI-Assisted Alert Triage for Wazuh

## Overview

An experiment testing whether a small, locally-run LLM can meaningfully assist with SOC alert triage — pulling real alerts from a Wazuh SIEM and asking a local model to summarize and prioritize them. Built as a follow-up to my [Wazuh Detection Lab](#wazuh--sysmon--atomic-red-team-detection-lab), using its real alert data as input. The result: the model was inconsistent and prone to fabricating threat context, which turned out to be the more useful finding than a clean success would have been.

## Architecture

Runs entirely on the same Ubuntu VM as the Wazuh manager — no new infrastructure needed:

| Component | Role | Software |
|---|---|---|
| Wazuh Indexer | Source of alert data, queried via REST API | OpenSearch (bundled with Wazuh) |
| Ollama | Local LLM runtime, no cloud API, no cost | Ollama, running `llama3.2:1b` |
| Python script | Pulls alerts, sends to local LLM, prints summary + priority | Python 3.14, `requests`, `ollama` libraries |

Chose a fully local model over a cloud API (OpenAI/Claude/etc.) deliberately: no signup, no billing, no API key management, and it fits a security project better to keep alert data on-machine rather than sending it to a third party.

---

## Build Steps

### 1. Set up a Python virtual environment
Ubuntu 26.04's system Python blocks direct `pip install` for safety (PEP 668, "externally-managed-environment"). Used a virtual environment instead of overriding it:
```bash
sudo apt install python3-pip python3.14-venv -y
python3 -m venv ~/wazuh-ai-triage/venv
source ~/wazuh-ai-triage/venv/bin/activate
pip install requests ollama
```

### 2. Confirmed direct access to Wazuh's alert data
Wazuh's alerts live in its indexer (OpenSearch), not the manager's REST API. Verified access with a raw query before writing any Python:
```bash
curl -k -u admin:'<password>' "https://localhost:9200/wazuh-alerts-*/_search?pretty&size=1"
```
Returned a full alert as JSON, confirming the data path.

### 3. Installed Ollama and pulled a local model
```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.2:1b
```
Chose a small (~1.3GB) model deliberately — the task (summarizing a short alert description) doesn't need frontier-level reasoning, and a small model keeps the whole thing running comfortably on a lab VM with no GPU.

### 4. Wrote the triage script
`triage.py` pulls the most recent alerts from the indexer, sends each one to the local model with a prompt asking for a plain-English summary and a LOW/MEDIUM/HIGH priority rating, and prints the result:

```python
import requests
import ollama

requests.packages.urllib3.disable_warnings()

WAZUH_URL = "https://localhost:9200/wazuh-alerts-*/_search"
WAZUH_USER = "admin"
WAZUH_PASS = "<password>"

def get_recent_alerts(count=5):
    query = {
        "size": count,
        "sort": [{"@timestamp": {"order": "desc"}}]
    }
    response = requests.get(
        WAZUH_URL,
        auth=(WAZUH_USER, WAZUH_PASS),
        json=query,
        verify=False
    )
    return response.json()["hits"]["hits"]

if __name__ == "__main__":
    alerts = get_recent_alerts()
    for alert in alerts:
        rule = alert["_source"]["rule"]
        description = rule["description"]
        level = rule["level"]

        prompt = f"Summarize this security alert in one plain-English sentence, and rate it as LOW, MEDIUM, or HIGH priority: '{description}' (severity level {level})"

        response = ollama.generate(model="llama3.2:1b", prompt=prompt)

        print(f"\n--- Original Alert (Level {level}) ---")
        print(description)
        print("--- AI Summary ---")
        print(response["response"])
```

<img width="1291" height="816" alt="image" src="https://github.com/user-attachments/assets/425c4147-b8a3-4cdb-905a-4945b7ac8efa" />
<img width="1267" height="219" alt="image" src="https://github.com/user-attachments/assets/9ff98636-99c2-42f2-ba35-aa6c59e1cd80" />


### 5. Ran the script against real alerts — and found a problem
Ran the script against genuine alerts pulled live from the indexer. The model was inconsistent and prone to fabricating threat context. Three identical **"PAM: Login session closed"** alerts, run back to back, were rated LOW, HIGH, and — most notably — one response claimed the session was "closed due to suspicious activity," a detail invented by the model that doesn't appear anywhere in the actual alert data.

Example output (same alert type, two different ratings):
```
--- Original Alert (Level 3) ---
PAM: Login session closed.
--- AI Summary ---
I would rate this security alert as LOW priority. The message is related to a
user's login session, which is a low-risk issue and not typically considered
a critical security vulnerability.

--- Original Alert (Level 3) ---
PAM: Login session closed.
--- AI Summary ---
As for the priority rating, I would rate it as HIGH. Here's why: The alert is
related to a potential security vulnerability that could be exploited by an
attacker to gain unauthorized access to the system or data...
```
<img width="1288" height="802" alt="image" src="https://github.com/user-attachments/assets/0a97e616-cee4-4d0d-a5fc-0843519ce67c" />
<img width="1283" height="394" alt="image" src="https://github.com/user-attachments/assets/a9f9110c-9ad2-4cd4-9a8f-b278642ab002" />

## Conclusion

This project set out to test whether a small, locally-run LLM could meaningfully assist with SOC alert triage, using real alert data from my own Wazuh lab. The honest answer is no — not without more work. The model was inconsistent (rating identical alerts differently across runs) and, more seriously, fabricated threat context that wasn't present in the source data. That's a genuinely useful result: it demonstrates the kind of critical evaluation a security practitioner needs to apply to AI tooling before trusting it in a real workflow, rather than assuming AI-generated output is reliable by default.

## Vulnerability Management Lab: Scan, Prioritize, Remediate, Rescan

## Overview

A home lab built to practice the vulnerability management lifecycle. I scan an intentionally vulnerable Linux target and a Windows 11 endpoint with Nessus Essentials, rank the findings by real-world risk instead of severity alone (CVSS + EPSS + CISA's Known Exploited Vulnerabilities catalog), fix or mitigate the top findings, and rescan to prove the result. It complements my Wazuh detection lab: that project covered catching attacker activity, this one covers finding and closing the weaknesses attackers use.

<!-- TODO: once finished, add one sentence with the headline result, e.g. "Fixing N findings cut the credentialed Metasploitable scan from X to Y." -->

## Architecture

Three VMs on an isolated host-only network in VirtualBox, with no route to the internet, so the vulnerable machine is never exposed:

| VM | Role | Software |
|---|---|---|
| Kali Linux (10.10.10.10) | Scanner | Kali 2026.2, Nessus Essentials, nmap |
| Metasploitable 2 (10.10.10.20) | Intentionally vulnerable Linux target | Metasploitable 2 |
| Windows 11 (10.10.10.30) | Windows target for credentialed scanning | Windows 11 |

**Software:**
- Nessus Essentials (vulnerability scanner)
- nmap (connectivity checks)
- Python 3, standard library only (triage script)
- CISA KEV catalog and FIRST.org EPSS API (prioritization data)
- VirtualBox for the lab

**How findings are ranked:**

| Tier | Rule |
|---|---|
| P1 - Known exploited | Any CVE on the finding is in the CISA KEV catalog |
| P2 - High exploit likelihood | EPSS of 0.30 or higher |
| P3 - High severity | Scanner rates it Critical or High |
| P4 - Routine | Everything else |

The 0.30 EPSS cutoff is a judgment call rather than a standard. Findings with no CVE (default credentials, cleartext services) can't be ranked by KEV or EPSS, so they fall back to scanner severity.

---

## Build Steps

### 1. Built the isolated lab network
Put all three VMs on one VirtualBox host-only network with static 10.10.10.0/24 addresses. Kali keeps a second NAT adapter so Nessus can download plugins, while Metasploitable has no internet-facing adapter at all.

<img width="949" height="515" alt="image" src="https://github.com/user-attachments/assets/876d2f7f-00b6-4ddd-a7e5-2b16e89ab933" />
<img width="913" height="426" alt="image" src="https://github.com/user-attachments/assets/e4b8864f-6fb0-46c5-841d-c70975bcd665" />
<img width="744" height="218" alt="image" src="https://github.com/user-attachments/assets/ff34f99f-5f7e-4bc2-9b17-765b7e2d355f" />


### 2. Fixed connectivity to the Windows VM
Hit two snags getting the scanner to see Windows. The first test (`nmap -Pn -p 445 10.10.10.30`) reported 0 hosts up, because I had attached the Windows adapter to a VirtualBox Internal Network while Kali was on the Host-only network. VirtualBox only connects adapters that share a network, so the two machines couldn't see each other even though the IP settings were correct. Moving Windows onto the same host-only network fixed discovery, and `nmap -sn` listed all three hosts.

The next check showed port 445 as `filtered`. That meant Kali could reach the host but Windows Defender Firewall was dropping SMB. I set the network profile to Private and added a narrow inbound rule that allows port 445 only from the scanner, instead of enabling the whole File and Printer Sharing group:

```powershell
Set-NetIPInterface -InterfaceAlias "Ethernet" -Dhcp Disabled
New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 10.10.10.30 -PrefixLength 24
Set-NetConnectionProfile -InterfaceAlias "Ethernet" -NetworkCategory Private
New-NetFirewallRule -DisplayName "Lab SMB from Kali" -Direction Inbound -Protocol TCP -LocalPort 445 -RemoteAddress 10.10.10.10 -Action Allow
```

<img width="639" height="421" alt="image" src="https://github.com/user-attachments/assets/efc8e77c-345f-4c57-8fed-574558e3145c" />
<img width="695" height="213" alt="image" src="https://github.com/user-attachments/assets/368f9e09-4927-430d-90d1-f9330a57d30f" />
<img width="650" height="210" alt="image" src="https://github.com/user-attachments/assets/ed860034-5d65-4ce9-a971-44c168e535e6" />


### 3. Took baseline snapshots
Took a `clean-baseline` snapshot of each VM before running any scans or changing anything, so the lab can be reset for the rescan.

### 4. Installed Nessus Essentials on the Kali scanner 
Downloaded the Nessus installer from tenable and installed it on the kali VM. Nessus Essentials is free under a 30-day license limited to 5 IP addresses, which is enough for this two-target lab. I used the Ubuntu .deb build, since kali is Debian-based, and it installed without errors. After installing, I started the service and opened the setup page in Firefox at 'https://localhost:8834':

```powershell
cd ~/Downloads
sudo dpkg -i Nessus-*.deb
sudo systemctl start nessusd
```
Firefox showed a certificate warning because Nessus uses a self-signed certificate, which is expected for a scanner running locally on my own VM. 

<img width="948" height="533" alt="image" src="https://github.com/user-attachments/assets/547e1a11-16b5-4078-af07-a78bc35728a4" />
<img width="1782" height="832" alt="image" src="https://github.com/user-attachments/assets/47014470-77d6-4dd6-b0a5-b67889ae0b4e" />

### 5. Prioritized findings with a Python script
Wrote `kev_triage.py` to read a Nessus CSV export, pull the CISA KEV catalog and EPSS scores, and sort the findings into the priority tiers above. It also has a `compare` mode that diffs a before and after export. The script uses only the standard library, so it runs anywhere with Python 3.

```bash
python3 kev_triage.py triage scans/ms2-cred-before.csv -o ms2-prioritized-before.csv
python3 kev_triage.py compare scans/ms2-cred-before.csv scans/ms2-cred-after.csv
```

<details>
<summary>View kev_triage.py</summary>

```python
#!/usr/bin/env python3
"""kev_triage.py - risk-based triage of a Nessus CSV export.

Usage:
  python kev_triage.py triage  scan.csv  -o prioritized.csv
  python kev_triage.py compare before.csv after.csv

Offline testing: add --kev-file kev.csv and --no-epss
"""
import argparse, csv, json, os, re, sys, urllib.request

KEV_URL = ("https://www.cisa.gov/sites/default/files/csv/"
           "known_exploited_vulnerabilities.csv")
EPSS_API = "https://api.first.org/data/v1/epss?cve="
CVE_RE = re.compile(r"CVE-\d{4}-\d{4,}", re.I)
RISK_RANK = {"Critical": 4, "High": 3, "Medium": 2, "Low": 1, "None": 0}


def load_kev(path=None):
    """Return the set of CVE IDs in CISA's KEV catalog."""
    if path and os.path.exists(path):
        text = open(path, encoding="utf-8-sig").read()
    else:
        with urllib.request.urlopen(KEV_URL, timeout=30) as r:
            text = r.read().decode("utf-8-sig")
    return {row["cveID"].upper() for row in csv.DictReader(text.splitlines())}


def load_epss(cves):
    """Return {CVE: EPSS probability} using the free FIRST.org API."""
    scores, cves = {}, sorted(cves)
    for i in range(0, len(cves), 50):
        url = EPSS_API + ",".join(cves[i:i + 50])
        with urllib.request.urlopen(url, timeout=30) as r:
            for item in json.load(r).get("data", []):
                scores[item["cve"].upper()] = float(item["epss"])
    return scores


def read_findings(path):
    rows = []
    with open(path, newline="", encoding="utf-8-sig") as f:
        for row in csv.DictReader(f):
            if row.get("Risk", "None") in ("None", ""):
                continue  # skip informational plugins
            row["_cves"] = sorted({c.upper() for c in CVE_RE.findall(row.get("CVE", ""))})
            rows.append(row)
    return rows


def tier(in_kev, epss, risk):
    if in_kev:
        return "P1 - Known exploited (KEV)"
    if epss >= 0.30:
        return "P2 - High exploit likelihood"
    if risk in ("Critical", "High"):
        return "P3 - High severity"
    return "P4 - Routine"


def triage(args):
    findings = read_findings(args.scan)
    kev = load_kev(args.kev_file)
    all_cves = {c for f in findings for c in f["_cves"]}
    epss = {} if args.no_epss else load_epss(all_cves)
    out = []
    for f in findings:
        in_kev = any(c in kev for c in f["_cves"])
        top_epss = max([epss.get(c, 0.0) for c in f["_cves"]] or [0.0])
        out.append({
            "Priority": tier(in_kev, top_epss, f.get("Risk", "")),
            "Host": f.get("Host", ""), "Port": f.get("Port", ""),
            "Plugin ID": f.get("Plugin ID", ""), "Name": f.get("Name", ""),
            "Risk": f.get("Risk", ""), "CVEs": " ".join(f["_cves"]) or "No CVE",
            "In KEV": "YES" if in_kev else "no", "EPSS": round(top_epss, 4),
            "Solution": f.get("Solution", "")[:200],
        })
    out.sort(key=lambda r: (r["Priority"], -r["EPSS"], -RISK_RANK.get(r["Risk"], 0)))
    with open(args.output, "w", newline="", encoding="utf-8") as fh:
        w = csv.DictWriter(fh, fieldnames=list(out[0].keys()))
        w.writeheader()
        w.writerows(out)
    counts = {}
    for r in out:
        counts[r["Priority"]] = counts.get(r["Priority"], 0) + 1
    print(f"{len(out)} findings written to {args.output}")
    for k in sorted(counts):
        print(f"  {k}: {counts[k]}")


def key(row):
    return (row.get("Host", ""), row.get("Port", ""), row.get("Plugin ID", ""))


def compare(args):
    before = {key(r): r for r in read_findings(args.before)}
    after = {key(r): r for r in read_findings(args.after)}
    fixed = [before[k] for k in before if k not in after]
    still = [before[k] for k in before if k in after]
    new = [after[k] for k in after if k not in before]
    print(f"Before: {len(before)} | After: {len(after)}")
    print(f"Fixed: {len(fixed)} | Still open: {len(still)} | New: {len(new)}")
    if before:
        print(f"Reduction: {100 * len(fixed) / len(before):.1f}%")
    for label, rows in (("FIXED", fixed), ("NEW", new)):
        print(f"\n{label}:")
        for r in rows:
            print(f"  [{r.get('Risk')}] {r.get('Host')}:{r.get('Port')} {r.get('Name')}")


if __name__ == "__main__":
    p = argparse.ArgumentParser(description=__doc__)
    sub = p.add_subparsers(dest="cmd", required=True)
    t = sub.add_parser("triage")
    t.add_argument("scan")
    t.add_argument("-o", "--output", default="prioritized.csv")
    t.add_argument("--kev-file")
    t.add_argument("--no-epss", action="store_true")
    t.set_defaults(fn=triage)
    c = sub.add_parser("compare")
    c.add_argument("before")
    c.add_argument("after")
    c.set_defaults(fn=compare)
    a = p.parse_args()
    a.fn(a)
```

</details>

<!-- TODO: add 1-2 sentences on what the ranking showed, e.g. how many findings were P1 (KEV), and whether the order differed from plain CVSS ranking -->
<!-- paste screenshot: terminal output of the triage script -->

### 6. Remediated the top findings
<!-- TODO: rewrite with what you actually did. Pick 5-8 findings. Suggested framing: -->
Chose [N] findings from the top of the prioritized list, including at least one with no CVE. Metasploitable 2 is end-of-life and its package repositories no longer exist, so I couldn't patch it. Fixes were disabling services, changing credentials, and adding firewall rules, which is how legacy systems that can't be patched are handled in practice. Each fix is recorded below with the response type (remediate, mitigate, or accept).

<!-- paste screenshot: evidence a fix worked, e.g. netstat showing a port gone -->

### 7. Rescanned and compared
<!-- TODO: rewrite after the rescan. Suggested content: -->
Re-ran the same three scans with the same policies and compared them with the script's `compare` mode. [X] findings were fixed, [Y] remained, and [Z] were new. <!-- TODO: explain any new findings or fixed findings that still appeared, honestly, like the LSASS note in your detection lab -->

<!-- paste screenshot: compare script output -->

## Results

<!-- TODO: fill in with your real numbers -->

| Target | Scan | Critical | High | Medium | Low | Total |
|---|---|---|---|---|---|---|
| Metasploitable 2 | Unauthenticated, before | TBD | TBD | TBD | TBD | TBD |
| Metasploitable 2 | Credentialed, before | TBD | TBD | TBD | TBD | TBD |
| Metasploitable 2 | Credentialed, after | TBD | TBD | TBD | TBD | TBD |
| Windows 11 | Credentialed, before | TBD | TBD | TBD | TBD | TBD |
| Windows 11 | Credentialed, after | TBD | TBD | TBD | TBD | TBD |

**Remediation log:**

| Finding | Plugin ID | Priority | Response | Change made | Result |
|---|---|---|---|---|---|
| TBD | TBD | TBD | TBD | TBD | TBD |

## Conclusion

<!-- TODO: write after the lab is done, in the same honest style as your other conclusions. Cover: what the credentialed scan found that the unauthenticated scan missed; how many findings were known-exploited (KEV) and whether ranking by KEV/EPSS changed the order compared with CVSS alone; what you could not patch and how you handled it; anything that surprised you or didn't go as planned; what you would add in a real environment (asset criticality, change windows, recurring scheduled scans). -->

TBD

## Skills Demonstrated

<!-- TODO: keep only what you actually did -->
- Vulnerability scanning with Nessus (unauthenticated and credentialed)
- Risk-based prioritization using CVSS, EPSS, and CISA KEV
- Python automation for scan triage and before/after comparison
- Remediation planning (remediate, mitigate, accept) and verification by rescan
- Isolated lab design and network troubleshooting (VirtualBox, nmap)
- Windows firewall and network profile configuration (PowerShell)
- Documenting findings and remediation in a repeatable format
## Connect
- [LinkedIn](https://www.linkedin.com/in/zachary-bolgert-77338837b)
- Email: ZacharyBolgert1@gmail.com
