# [CASE] Suspicious mshta.exe Execution on Host Roberto

### Case ID (slug-friendly)

lolbin-2025-10-07

### Case Title

Suspicious mshta.exe Execution

### Executive summary

Suspicious execution of mshta.exe launched a malicious .hta file (Ps1.hta) which triggered PowerShell activity and external communication. Indicates LOLBIN abuse for code execution.

### Timeline (key timestamps)

2025-03-05 10:29 — mshta.exe executed Ps1.hta  
2025-03-05 10:30 — PowerShell launched with obfuscated script  
2025-03-05 10:31 — External connection to 193.142.58.23 established

### Artifacts / IOCs

Host: Roberto (172.16.17.38)
File: C:\Users\Roberto\Desktop\Ps1.hta
MD5: 6685c433705f558c5535789234db0e5a
External IP: 193.142.58.23
Binary: C:\Windows\System32\mshta.exe

### Technical analysis

mshta.exe (LOLBIN) executed an .hta file containing obfuscated PowerShell commands.
PowerShell then reached out to external IP 193.142.58.23, possibly for C2 communication.
MITRE: T1218.005 (Mshta), T1059.001 (PowerShell), T1071.001 (C2 over HTTP).

### Actions taken / Mitigation

Isolated host 172.16.17.38

Blocked IP 193.142.58.23

Collected and quarantined Ps1.hta file

Checked PowerShell logs and browser artifacts

Updated IOC blocklist

### Recommendations / Next steps

Hunt for similar mshta.exe → PowerShell executions

Review recent email attachments on affected host

Add AppLocker rule to restrict mshta.exe

Enable full PowerShell logging in environment

### Case owner

Ievgen Bondarenko
