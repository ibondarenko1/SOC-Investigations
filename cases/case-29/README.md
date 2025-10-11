# [CASE] SOC145 - Ransomware Detected on MarkPRD

### Case ID (slug-friendly)

ransom-2021-05-23

### Case Title

Ransomware infection detected on endpoint MarkPRD (172.16.17.88)

### Executive Summary

Critical ransomware activity detected on host MarkPRD. The malicious file ab.exe (hash 0b486fe0503524cfe4726a4022fa6a68) was allowed to run, triggering outbound C2 communication. Immediate containment and remediation were required to prevent further spread.


### Timeline (Key Timestamps)

2021-05-23 19:32 — Alert SOC145 triggered: “Ransomware Detected”
2021-05-23 19:35 — File ab.exe executed on host MarkPRD
2021-05-23 19:37 — Outgoing connection to C2 observed
2021-05-23 19:40 — Host containment initiated by Security Analyst


### Artifacts / Indicators of Compromise (IOCs)

- MD5: 0b486fe0503524cfe4726a4022fa6a68
- File: ab.exe
- IP: 172.16.17.88 (source host)
- Hostname: MarkPRD
- C2 connection: Unknown remote address (outgoing traffic confirmed)


### Technical Analysis

The file ab.exe was executed and identified as ransomware during endpoint monitoring. EDR logs show the process svchost.exe with a suspicious hash, likely injected by the ransomware. The host initiated outbound communication consistent with C2 activity. Malware analysis via VirusTotal confirmed multiple detections (Ransomware family). The device action was “Allowed,” meaning no automatic quarantine occurred.


### Mitigation / Response Actions

- Isolated affected host (MarkPRD)
- Disabled user account MarkGuna
- Removed ab.exe and associated persistence artifacts
- Conducted full malware scan on network segment
- Restored clean image from backup


### Recommendations / Next Steps

- Update EDR policy to automatically quarantine ransomware detections
- Review firewall outbound connection rules
- Conduct ransomware awareness training for users
- Perform IOC sweep across the environment


### AI Prompt & Response (AI Support Summary)

**Prompt:**
"Analyze ransomware alert SOC145 from LetsDefend with host logs and process data."

**AI Response:**
The executable ab.exe (MD5: 0b486fe0503524cfe4726a4022fa6a68) was confirmed malicious.
The process attempted outbound C2 communication after execution. The infection originated from a user download or phishing email. Recommended containment and policy update.
This behavior aligns with MITRE ATT&CK techniques:
- T1059: Command and Scripting Interpreter
- T1071: Application Layer Protocol (C2 Communication)
- T1486: Data Encrypted for Impact


### Case Owner

Ievgen Bondarenko
