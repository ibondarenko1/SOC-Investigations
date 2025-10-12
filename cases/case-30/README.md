# [CASE] Malicious Python Script Creating Scheduled Task

### Case ID (slug-friendly)

malware-2025-10-11

### Case Title

Malicious Python Script Creating Persistence Task

### Executive Summary

A suspicious Python script (Sorted-Algorithm.py) was executed on host Helena (172.16.17.36). The file created a scheduled task to maintain persistence. No outbound C2 communication detected. Classified as True Positive.

### Timeline (Key Timestamps)

2021-05-14 03:22 PM — Alert triggered: “SOC144 - New scheduled task created”

2021-05-14 03:23 PM — Command executed: SCHTASKS /CREATE /SC DAILY /TN DailyRoutine /TR C:\Windows\Temp\x86_x64_se...

2021-05-14 03:25 PM — Analyst verified malicious persistence creation via Terminal History

2021-05-14 03:35 PM — Malware hash and behavior confirmed

### Artifacts / Indicators of Compromise (IOCs)

MD5: 65d880c7f474720dafb84c1e93c51e11

File: Sorted-Algorithm.py

Source IP: 172.16.17.36

Hostname: Helena

Process: python.exe, created new scheduled task

MITRE ATT&CK: T1053.005 – Scheduled Task/Job: Scheduled Task

### Technical Analysis

Review of EDR logs shows the user executed a Python script manually.

The script triggered a persistence mechanism by creating a daily scheduled task.

Network logs show no evidence of C2 or external data exfiltration.

Endpoint remained online and accessible; antivirus did not quarantine the file.

Sandbox analysis confirmed the file exhibits persistence behavior but no immediate payload execution.

### Mitigation / Response Actions

Marked the file as malicious.

Recommended full antivirus scan and deletion of the scheduled task.

Verified no lateral movement or C2 activity.

Updated detection rules for similar scheduled task creation events.

Documented incident in SOC tracking system.

### Recommendations / Next Steps

Review scheduled tasks on all endpoints in the same network segment.

Conduct user awareness training on executing unknown scripts.

Tune SIEM correlation rules for suspicious use of SCHTASKS.

Periodically verify antivirus protection is active on all hosts.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze alert SOC144 — new scheduled task created by suspicious Python script.”

AI Response:
The alert indicates possible persistence creation (MITRE ATT&CK T1053).
The script Sorted-Algorithm.py created a daily scheduled task in Windows Task Scheduler.
No outbound C2 detected, suggesting pre-persistence staging activity.
Recommended to quarantine the file and review user’s PowerShell and Python execution history.

### Case Owner

Ievgen Bondarenko
