# [CASE] Cobalt Strike / Meterpreter Remote Access on Workstation Alex-HP

### Case ID (slug-friendly)

cs-172-16-17-55-2021-03-15

### Case Title

Confirmed Cobalt Strike Compromise on Endpoint

### Executive Summary

Endpoint Alex-HP (172.16.17.55) was confirmed compromised by a Cobalt Strike / Meterpreter payload. The host established outbound C2 communication and executed attacker commands, including downloading a secondary malicious payload and creating a persistence user account. Host requires isolation and full remediation.


### Timeline (Key Timestamps)

2020-12-21 13:00 — PowerShell reverse shell executed (TCPClient).
2020-12-21 13:17 — certutil used to download services.exe from 221.181.185.200:8080.
2020-12-21 13:18 — Attacker created persistence account: net user alexx H4rd2Cr4ck! /add.
2021-03-15 14:15 — Outbound C2 connection to 120.79.181.138 observed.


### Artifacts / Indicators of Compromise (IOCs)

IP: 120.79.181.138 (C2)
IP: 221.181.185.200 (Malware hosting)
URL: http://221.181.185.200:8080/services.exe
File: cobaltstrike_shellcode.exe
MD5: 24d99ba5654cdf31141c66fd9417b7e0
File: C:\Users\Public\svchosts.exe (malicious persistence binary)
Host: 172.16.17.55 (Alex-HP)


### Technical Analysis

- Cobalt Strike payload executed on host.
- PowerShell TCP reverse shell established for remote control.
- certutil used to download additional payload (services.exe) from attacker server.
- Persistence account created by attacker: "alexx".
- Malicious binary svchosts.exe placed in C:\Users\Public\ to mimic system process.
- Outbound network traffic confirmed to known C2 infrastructure.


### Mitigation / Response Actions

- Isolated affected endpoint from the network.
- Blocked C2 IPs 120.79.181.138 and 221.181.185.200 at firewall.
- Removed attacker persistence account (net user alexx /delete).
- Collected malicious binaries for evidence and sandbox analysis.
- Recommended full host reimage and credential reset.


### Recommendations / Next Steps

- Conduct environment-wide IOC sweep for C2 IPs and svchosts.exe copy.
- Reset credentials used on or from this host.
- Review AD logs for possible lateral movement.
- Add detections for certutil misuse, suspicious PowerShell, and svchosts.exe path anomalies.


### AI Prompt & Response (AI Support Summary)

Prompt:
"Analyze Meterpreter/Cobalt Strike activity observed on endpoint."

AI Response:
Identified Cobalt Strike payload execution, certutil-based payload retrieval, attacker account creation, and outbound C2 communication. Confirmed remote control and persistence behavior.


### Case Owner

Ievgen Bondarenko
