# [CASE] Event Log Cleared — Unauthorized Account Creation / Malicious Binary (Exchange Server)

### Case ID (slug-friendly)

soc-2025-11-13-064

### Case Title

Unauthorized Account Creation and Malicious Binary Detected on Exchange Server

### Executive Summary

A malicious actor gained unauthorized access to the Exchange Server and created a backdoor account. Evidence includes execution of credential-related commands, presence of a modified system binary (hh.exe), and clearing of Windows Event Logs. This confirms an active compromise requiring immediate containment.

### Timeline (Key Timestamps)

2020-10-10 10:29:01 — Terminal commands executed (net user, net localgroup).
2020-10-10 10:29:04 — New privileged user backupUser added.
2021-02-21 19:23 — EventID 64: Event Logs Cleared.
2025-11-13 — SOC investigation initiated and compromise confirmed.

### Artifacts / Indicators of Compromise (IOCs)

MD5: 1ceece8d02a8e9b19d3a1a65c7a2b249 (malicious hh.exe)

File: C:\Windows\hh.exe

Unauthorized account: backupUser

Host: Exchange Server (172.16.20.3)

(Если есть — добавляешь IP, URL, SHA256, службы, persistence.)

### Technical Analysis

The Exchange Server executed suspicious account-creation commands:

net user backupUser

net localgroup backupGroup backupUser /add

A modified Windows binary (hh.exe) was found with a non-legitimate MD5 hash.

Presence of unusual processes (chrome.exe, AcroRd32.exe, notepad.exe) on a server is indicative of interactive attacker activity.

Event Logs were cleared (EventID 64), indicating defense evasion.

No outbound C2 communication observed.

Malware was not quarantined by the endpoint.

### Mitigation / Response Actions

Confirmed malicious binary (via VT and behavioral analysis).

Marked incident as True Positive.

Containment recommended:

Isolate Exchange Server from the network.

Remove unauthorized user (backupUser).

Replace or restore corrupted system files.

Conduct AV/EDR full scan.

Reset credentials for all privileged accounts.

Rotate service account passwords.

### Recommendations / Next Steps

Perform full compromise assessment on the domain.

Review RDP logs and authentication history.

Hunt for similar IOCs across environment (hash, commands, new accounts).

Implement stricter PowerShell logging (Module + ScriptBlock).

Enable tamper-proof logging via SIEM.

Review firewall egress rules to block future C2 attempts.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze malicious activity involving unauthorized account creation and hash-mismatched hh.exe.”

AI Response:
Analysis confirms malicious activity consistent with MITRE techniques T1136 (Create Account), T1070 (Clear Logs), and T1059 (Command Execution). Presence of modified system binary and unauthorized user creation indicates active compromise requiring immediate containment.

### Case Owner

Ievgen Bondarenko
