# [CASE] SOC119 - Proxy: Malicious Executable File Detected

### Case ID (slug-friendly)

soc119-2025-10-20

### Case Title

Malicious Executable Download from PentestMachine

### Executive Summary

An alert was triggered by the proxy for a suspicious executable download from GitHub. The source host (PentestMachine – Kali Linux) was confirmed as part of an authorized internal penetration test. The activity involved downloading the BloodHound tool used for legitimate security assessments.

### Timeline (Key Timestamps)

2025-10-20 09:14 — Proxy detected download of executable from GitHub

2025-10-20 09:16 — Analyst validated source IP (172.16.20.5) from PentestMachine

2025-10-20 09:18 — File hash and URL analyzed via VirusTotal (benign result)

2025-10-20 09:22 — Alert confirmed as authorized pentest activity

2025-10-20 09:25 — Case closed as false positive

### Artifacts / Indicators of Compromise (IOCs)

Source IP: 172.16.20.5

Destination IP: 140.82.121.4

URL: https://github.com/BloodHoundAD/BloodHound/releases

Domain: github.com

Filename: BloodHound.zip

### Technical Analysis

Proxy logs confirmed download request from PentestMachine (Kali).

The file hash was verified in VirusTotal — no detections reported.

Log Management showed user kali initiated the request.

The BloodHound tool is legitimate software used for Active Directory analysis.

No suspicious outbound or lateral network activity observed post-download.

### Mitigation / Response Actions

Verified activity with internal pentest schedule.

Added GitHub BloodHound release URL to internal allowlist for pentest machines.

No remediation required.

### Recommendations / Next Steps

Continue monitoring for unauthorized BloodHound usage from non-pentest assets.

Maintain updated pentest activity whitelist in proxy rules.

Conduct regular review of authorized tool usage logs.

### AI Prompt & Response (AI Support Summary)

Prompt: “Summarize and classify the SOC119 - Proxy Malicious Executable File Detected alert in LetsDefend.”
AI Output Summary: The alert is linked to a legitimate pentesting tool download (BloodHound) from an authorized host (Kali). No malicious behavior detected. Classified as False Positive – Authorized Pentest Activity.

### Case Owner

Ievgen Bondarenko
