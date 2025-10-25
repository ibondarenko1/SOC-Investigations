# [CASE] Malicious Excel Macro Triggering PowerShell – Host Sofia

### Case ID (slug-friendly)

malware-2021-03-13

### Case Title

Suspicious XLSM File Executed on Endpoint Sofia (172.16.17.56)

### Executive Summary

User Sofia (172.16.17.56) downloaded a macro-enabled Excel file “ORDER SHEET & SPEC.xlsm” that triggered encoded PowerShell activity. 
The file was confirmed malicious via sandbox analysis and established C2 communication. 
The malware was not quarantined, requiring manual host isolation and remediation.


### Timeline (Key Timestamps)

2021-03-13 20:20 — SOC138 alert triggered: Detected Suspicious XLS File.
2021-03-13 20:21 — File downloaded: ORDER SHEET & SPEC.xlsm (7ccf88c0bbe3b29bf19d877c4596a8d4).
2021-03-13 20:22 — PowerShell -EncodedCommand observed on host Sofia.
2021-03-13 20:24 — Outbound C2 request to mztech.org.mz/teet/.
2021-03-13 20:25 — File confirmed malicious (VirusTotal/Hybrid Analysis).


### Artifacts / Indicators of Compromise (IOCs)

- URL: http://mztech.org.mz/teet/
- File Hash (MD5): 7ccf88c0bbe3b29bf19d877c4596a8d4
- File Name: ORDER SHEET & SPEC.xlsm
- IP Address: 172.16.17.56
- Email Sender: radiosputnik@ria.ru
- Domain: ria.ru


### Technical Analysis

- Sandbox and threat intel confirmed the XLSM file drops or executes a PowerShell payload.
- PowerShell launched with Base64-encoded commands indicative of obfuscation and remote command execution.
- C2 communication confirmed with mztech.org.mz/teet/.
- No AV quarantine action observed — Device Action: Allowed.
- Behavior consistent with macro-based malware infection chain (initial access + execution).


### Mitigation / Response Actions

1. Isolate host Sofia (172.16.17.56) from the network.
2. Perform full endpoint malware scan and memory analysis.
3. Block domain mztech.org.mz and associated IPs.
4. Add file hash to EDR and email gateway blocklists.
5. Reset credentials of affected user (Sofia2020).
6. Update AV signatures and verify all Office macro settings.
7. Conduct user awareness training on phishing and macro threats.


### Recommendations / Next Steps

- Hunt for similar IOCs across the environment (hashes, URLs, sender domain).
- Review PowerShell execution logs and identify any other hosts running encoded commands.
- Conduct phishing awareness training for end users, emphasizing malicious macro risks.
- Apply network-level blocks for domain mztech.org.mz and related indicators.
- Update EDR and email security policies to detect and block macro-enabled files.
- Review firewall egress policies to restrict unauthorized outbound HTTP/HTTPS connections.


### AI Prompt & Response (AI Support Summary)

**Prompt:**
"Analyze suspicious PowerShell command from SIEM alert associated with XLSM macro execution."

**AI Response:**
The encoded PowerShell command decodes to a script using Invoke-WebRequest to download and execute a remote payload.
This behavior is consistent with post-exploitation or initial infection activity, aligning with MITRE ATT&CK technique 
T1059 (Command and Scripting Interpreter) and T1105 (Ingress Tool Transfer).
AI analysis confirmed this as malicious macro-based infection behavior originating from a phishing attachment.


### Case Owner

Ievgen Bondarenko
