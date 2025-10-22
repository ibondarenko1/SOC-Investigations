# [CASE] SSH Scan Activity – Authorized Red Team Exercise

### Case ID (slug-friendly)

soc147-sshscan-2025-10-21

### Case Title

Authorized Network Scan from Internal Red Team Host

### Executive Summary

An alert was triggered by the SOC147 rule — SSH Scan Activity.
Investigation determined that the scanning originated from an internal penetration testing machine (PentestMachine, 172.16.20.5).
The activity was verified as part of an authorized Red Team exercise. No compromise or malicious intent detected

### Timeline (Key Timestamps)

2021-06-13 16:23 — Nmap scan initiated from 172.16.20.5

2021-06-13 16:23 — Outbound SSH scan traffic to 172.16.20.1 – 172.16.20.6

2023-07-28 12:00 — Email received from redteam@letsdefend.io
 notifying scheduled scanning

2025-10-21 — Case reviewed and confirmed as authorized Red Team activity

### Artifacts / Indicators of Compromise (IOCs)

IP Address: 172.16.20.5 — Source (PentestMachine)

IP Range: 172.16.20.1 – 172.16.20.6 — Scanned hosts

MD5 Hash: 3361bf0051cc657ba90b46be53fe5b36 — Legitimate Nmap binary

E-mail Sender: redteam@letsdefend.io
 — Red Team communication

E-mail Domain: letsdefend.io — Official internal domain

### Technical Analysis

The PentestMachine executed the command:

nmap -sV -sP 172.16.20.0/24


Multiple outbound SSH connection attempts were observed in network logs.

File hash verification confirmed the binary as a legitimate version of Nmap.

No signs of malware infection, persistence, or data exfiltration.

Email review confirmed that Red Team activity was pre-approved and authorized.

### Mitigation / Response Actions

Verified Red Team authorization via email correspondence.

Ensured containment of PentestMachine during verification process.

Updated SOC documentation to whitelist 172.16.20.5 during future Red Team exercises.

No further response required.

### Recommendations / Next Steps

Maintain a central calendar for Red Team activity scheduling to avoid future false positives.

Implement tagging in SIEM for known internal testing hosts.

Conduct periodic review of SOC alert correlation rules to minimize noise.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze SSH Scan Activity alert (SOC147) and determine if it represents a real threat or Red Team activity.”

AI Response:
The scan originated from 172.16.20.5 (PentestMachine).
Command nmap -sV -sP 172.16.20.0/24 indicates authorized reconnaissance.
Emails from redteam@letsdefend.io
 confirm scheduled testing.
No malware, C2 communication, or compromise indicators found.
Classified as False Positive (Authorized Red Team exercise).

### Case Owner

Ievgen Bondarenko
