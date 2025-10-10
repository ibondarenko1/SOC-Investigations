# [CASE] Phishing Email – Excel 4.0 Macro / PowerShell C2 Activity

### Case ID (slug-friendly)

phish-2025-10-09

### Case Title

Phishing Email with Malicious Excel Macro Attachment

### Executive Summary

User received a phishing email from an external vendor address containing a password-protected Excel attachment.
The attachment used legacy Excel 4.0 macros to launch PowerShell, which initiated outbound HTTP requests to external IPs, establishing potential C2 communication.

### Timeline (Key Timestamps)

2021-06-13 02:11 — Email received by user
2021-06-13 02:13 — SIEM alert triggered (SOC146 – Excel 4.0 Macros)
2020-08-29 22:28 — PowerShell GET request to http://qstride.com/img/0/
2020-08-29 22:32 — rasser.exe POST to http://67.68.210.95/
2020-08-29 23:09 — PowerShell GET request to http://thuening.de/cgi-bin/uo9wmr/


### Artifacts / Indicators of Compromise (IOCs)

IP: 198.100.45.154
IP: 67.68.210.95
IP: 81.169.145.105
URL: http://qstride.com/img/0/
URL: http://thuening.de/cgi-bin/uo9wmr/
File Hash: 11f44531fb088d1307d87b701e8eabff
Sender: trenton@tritowncomputers.com
Recipient: lars@letsdefend.io
Attachment Password: infected
Process: powershell.exe, rasser.exe


### Technical Analysis

Attachment analyzed via VirusTotal and AnyRun — malicious.

Excel 4.0 macro executed PowerShell (Invoke-WebRequest) to fetch additional payloads.

Secondary binary rasser.exe performed outbound POST to C2.

Connection logs confirmed C2 URLs accessed from the host.

Device action = Permitted → message delivered and executed.

MITRE ATT&CK:

T1566.001 – Phishing Attachment

T1059.001 – PowerShell

T1071.001 – Web Protocols

T1105 – Ingress Tool Transfer

### Mitigation / Response Actions

Quarantined malicious email and attachment.

Blocked domains and IPs on perimeter firewall.

Isolated affected endpoint for forensic analysis.

Reset credentials for impacted user accounts.

Implemented SIEM rule: detect PowerShell + HTTP POST from user hosts.

### Recommendations / Next Steps

Disable Excel 4.0 macros across all users.

Enhance outbound traffic filtering to restrict unknown IPs/domains.

Enable detailed PowerShell script logging (Event ID 4104).

Conduct phishing awareness refresher training.

### AI Prompt & Response (AI Support Summary)

“Analyze suspicious PowerShell network activity triggered by Excel attachment.”

AI Response:
The Excel macro file executed PowerShell to download external content via HTTP.
C2 URLs and payload confirmed malicious.
Behavior aligns with MITRE T1059 (Command and Scripting Interpreter) and T1071 (Web Protocols).
Recommended blocking outbound traffic and isolating infected host.

### Case Owner

Ievgen Bondarenko
