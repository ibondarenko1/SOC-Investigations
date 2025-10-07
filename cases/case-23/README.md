# [CASE] Command Injection and Ransomware Activity (GoldenEye)

### Case ID (slug-friendly)

cmdinj-2025-10-06

### Case Title

External Command Injection on WebServer1004 leading to GoldenEye ransomware execution

### Executive summary

External actor exploited a command injection vulnerability on internal host WebServer1004 (172.16.17.16), executing “whoami” and later initiating PowerShell commands on Julia and Arnold. Investigation confirmed malicious payload downloads (GoldenEye ransomware) and execution attempts within the network.

### Timeline (key timestamps)

2025-10-06 07:29 – External connection from 61.177.172.87 to WebServer1004 exploiting RCE via /index.php?cmd=whoami  
2025-10-06 07:30 – Successful execution of injected command  
2025-10-06 13:30 – Arnold host accessed malicious S3 link containing “Vulnerability_Script.zip”  
2025-10-06 14:45 – PowerShell script disables Windows Defender and downloads ransomware payload  
2025-10-06 15:00 – Investigation confirmed lateral movement to Julia host  
2025-10-06 15:30 – Case escalated to Tier 2 for containment

### Artifacts / IOCs

- External IP: 61.177.172.87  
- Internal IP: 172.16.17.16 (WebServer1004)  
- Internal hosts: Julia (172.16.17.161), Arnold (172.16.17.164)  
- URL: https://files-ld.s3.us-east-2.amazonaws.com/434860b2-db11-4fb1-8f71-c5d1d6e14663-Vulnerability_Script.zip  
- File: Ransomware.GoldenEye.zip  
- Process: powershell.exe -command “Set-MpPreference -DisableRealtimeMonitoring”  
- Hash: (placeholder for MD5/SHA256 once available)

### Technical analysis

The investigation revealed command injection (RCE) from external IP 61.177.172.87 targeting WebServer1004 (Ubuntu 20.04). The attacker executed a “whoami” command successfully, confirming remote code execution.  
Subsequent analysis of Windows endpoints showed PowerShell activity that disabled Defender and attempted to download ransomware from S3-hosted URLs.  
Indicators match known GoldenEye ransomware behavior.  
No legitimate test indicators (e.g., Verodin, AttackIQ) were found — the incident was not part of a planned simulation.

### Actions taken / Mitigation

- Blocked external IP 61.177.172.87 at the perimeter firewall  
- Isolated affected hosts (WebServer1004, Arnold, Julia)  
- Removed downloaded malicious ZIP files  
- Triggered Tier 2 escalation for forensic investigation  
- Collected system and PowerShell logs for evidence preservation

### Recommendations / Next steps

- Perform full disk analysis of WebServer1004, Arnold, and Julia for persistence or lateral movement  
- Reset local credentials potentially exposed during compromise  
- Deploy additional WAF rules for command injection prevention  
- Update detection rules in SIEM for PowerShell + S3 downloads  
- Conduct ransomware recovery tabletop exercise

### Case owner

Ievgen Bondarenko
