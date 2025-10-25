# [CASE] Phishing email with malicious attachment — Vendor impersonation

### Case ID (slug-friendly)

phish-vendor-2025-10-24

### Case Title

Suspicious Phishing Email from Vendor (malicious attachment)

### Executive Summary

A user received a phishing email disguised as a legitimate vendor communication.
The email contained a malicious attachment which, once opened, executed a PowerShell script to download and run additional payloads.
The incident was detected through SMTP log analysis and confirmed by sandbox behavior.

### Timeline (Key Timestamps)

2025-10-24 09:10:23 — Phishing email received by user@corp.local.

2025-10-24 09:12:05 — User opened attachment secretrendezvous.docx.

2025-10-24 09:13:10 — EDR detected suspicious PowerShell activity (Invoke-WebRequest).

2025-10-24 09:14:22 — SIEM alert “suspicious-email-attachment” triggered.

2025-10-24 09:20:00 — User account disabled; endpoint isolated.

### Artifacts / Indicators of Compromise (IOCs)

IP: 203.0.113.45

URL: http://malicious.example/

Domain: badsite.biz

Sender: vendor-invoices@example.com

Attachment: secretrendezvous.docx

Attachment MD5: 9e423e11db88f01bbff81172839e1923

SHA256: abcdef1234567890… (replace with actual)

### Technical Analysis

SMTP headers show forged sender and relay chain.

Extracted attachment analyzed in sandbox — executed a macro initiating PowerShell download.

EDR logs confirm execution of powershell.exe with Invoke-WebRequest call.

Network telemetry revealed outbound connections to C2 IPs following attachment execution.

Sandbox confirmed persistence attempts and beaconing behavior (MITRE T1059, T1105).

### Mitigation / Response Actions

Isolated the affected endpoint from the corporate network.

Blocked sender and malicious domain at the mail gateway and proxy.

Reset compromised user credentials and forced logout of active sessions.

Added IOCs to SIEM/EDR/NGFW blocklists.

Conducted a full environment scan for lateral movement.

Restored system from a clean backup if necessary.

### Recommendations / Next Steps

Perform IOC hunting across environment (attachment hash, sender domain, C2 IP).

Strengthen mail gateway policies (macro blocking, attachment scanning).

Deliver phishing-awareness refresh training to users.

Review and tighten firewall egress rules.

If data exfiltration suspected, escalate for full forensics and legal review.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze suspicious PowerShell command from SIEM alert.”

AI Response:
The command downloads and executes a remote script via Invoke-WebRequest.
This behavior aligns with MITRE ATT&CK T1059 (Command and Scripting Interpreter) and T1105 (Ingress Tool Transfer).
Recommended actions: isolate the endpoint, capture volatile evidence, analyze the downloaded script, block associated domains/IPs, and update detection rules.

### Case Owner

Ievgen Bondarenko
