# [CASE] FTP Brute-Force + Confirmed Server Compromise

### Case ID (slug-friendly)

ftp-bruteforce-2025-01-29

### Case Title

FTP Brute Force Attack and Server Compromise

### Executive Summary

External IP 42.192.84.19 attempted multiple FTP brute-force logins against PublicServer (172.16.20.4). 
Investigation confirmed that the server was already compromised and contained malicious persistence (/root/shell.sh).


### Timeline (Key Timestamps)

2021-03-07 17:09 UTC — External IP 42.192.84.19 attempts FTP login to PublicServer (172.16.20.4) on port 21.
2021-03-07 17:09 UTC — Multiple credential guesses observed (admin/admin, admin/password, admin/123456, admin/root) — all rejected.
2021-03-07 17:12 UTC — Analyst review confirms host exhibits signs of prior compromise (unauthorized python3 process and /root/shell.sh).
2021-03-07 17:18 UTC — Additional lateral movement indicators detected on NodeServer and Roberto endpoints.
2021-03-07 17:25 UTC — PublicServer, NodeServer, Rosa, Roberto endpoints placed into network containment.
2021-03-07 17:30 UTC — IOC 42.192.84.19 added to firewall blocklist.


### Artifacts / Indicators of Compromise (IOCs)

IP: 42.192.84.19 (Brute-force source)
File: /root/shell.sh (malicious persistence script)
Process: python3 (unauthorized execution on PublicServer)


### Technical Analysis

- Observed multiple FTP login attempts from 42.192.84.19 targeting PublicServer.
- All login attempts were rejected, but system review revealed unauthorized shell script and running python3 process.
- This indicates the attacker achieved access prior to the brute-force attempts.
- Additional suspicious tools and remote access traces observed on internal hosts (NodeServer, Roberto, Rosa).


### Mitigation / Response Actions

- Contained affected hosts (network isolation).
- Blocked IOC IP 42.192.84.19 on firewall.
- Initiated forensic evidence collection (logs, processes, files).
- Recommended reimage of PublicServer due to confirmed root-level compromise.
- Password and credential rotation recommended for all affected systems.


### Recommendations / Next Steps

- Perform memory and disk forensic imaging before any system cleanup or reboot.
- Reimage PublicServer after evidence collection.
- Hunt for similar IOCs across internal network and SIEM logs.
- Implement brute-force detection and lockout rules on exposed services.


### AI Prompt & Response (AI Support Summary)

**Prompt:** "Summarize incident and recommend remediation."
**AI Response:** Identified FTP brute-force from external IP and confirmed prior compromise with persistence. Recommended host containment, IOC blocking, forensic imaging, reimage, and credential rotation.


### Case Owner

Ievgen Bondarenko
