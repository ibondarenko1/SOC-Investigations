# [CASE] Suspicious WMI Activity and Confirmed C2 Communication

### Case ID (slug-friendly)

malware-2025-10-19

### Case Title

Suspicious WMI Activity and Confirmed C2 Communication

### Executive Summary

An internal host (Aldo – 172.16.17.51) exhibited abnormal outbound connections and reconnaissance activity.
Further analysis confirmed malicious execution via PowerShell, creation of a backdoor user account on the Exchange Server, and successful C2 communication with external IPs.
Incident classified as True Positive with High severity.

### Timeline (Key Timestamps)

2025-10-18 09:43 — Suspicious outbound traffic detected from host Aldo.
2025-10-18 10:02 — User Aldo executed “ipconfig”, “nslookup 172.16.20.3”, and “net user”.
2025-10-18 10:15 — Outbound connections observed to 74.6.143.25 and 13.35.254.24.
2025-10-18 11:00 — Malware analysis confirmed file as malicious; C2 addresses identified.
2025-10-18 11:20 — Exchange Server (172.16.20.3) showed creation of unauthorized account “backupUser”.
2025-10-18 12:10 — C2 communication confirmed in Log Management.
2025-10-18 12:30 — No quarantine action detected; escalation to containment initiated.


### Artifacts / Indicators of Compromise (IOCs)

IP: 74.6.143.25, 13.35.254.24, 172.67.202.151

URL: https://cracking.org/, https://cracking.org/forums/cracking-tools.16/

E-mail Sender: 2constheatcomshirl@seznam.cz, security@letsdefend.io

MD5: a2cb77c5d58f7ae7cb3936222d5, 1fd76c47135226bb1369827e1fd6afd3

Hostname: Aldo, ExchangeServer, PentestMachine

### Technical Analysis

Detected suspicious WMI and PowerShell execution from host Aldo (172.16.17.51).

Endpoint logs showed connections to external IPs linked to malware C2 infrastructure.

Malware downloaded from cracking.org — classified as malicious by VirusTotal & HybridAnalysis.

No AV quarantine; persistence achieved via creation of local admin “backupUser” on Exchange Server.

MITRE Mapping:

T1018 – Remote System Discovery

T1047 – WMI Execution

T1136 – Create Account

T1059 – Command & Scripting Interpreter

### Mitigation / Response Actions

Isolated affected hosts (Aldo, Exchange Server).

Disabled user accounts: aldo, backupUser.

Blocked IPs and URLs via firewall and EDR rules.

Conducted full malware removal and credential resets.

Implemented PowerShell logging and WMI restrictions.

### Recommendations / Next Steps

Review internal segmentation and privilege access.

Deploy improved phishing detection and sandbox scanning.

Perform IOC sweep across endpoints for lateral movement traces.

Conduct security awareness training for employees.

Validate EDR coverage and response playbooks.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze suspicious WMI activity and identify potential C2 communication.”

AI Response:
The detected PowerShell and WMI processes indicate remote execution and possible lateral movement.
Outbound connections to multiple external IPs correspond with known C2 infrastructure.
This activity aligns with MITRE techniques T1047 (WMI Execution) and T1059 (Command and Scripting Interpreter).
Recommend containment, account review, and blocking external IPs.

### Case Owner

Ievgen Bondarenko
