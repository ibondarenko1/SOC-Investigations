# [CASE] SOC143 - Password Stealer Detected via Phishing Email

### Case ID (slug-friendly)

soc143-2021-04-26

### Case Title

Password Stealer Delivered via Phishing Email (True Positive)

### Executive Summary

A phishing email was detected with a malicious ZIP attachment sent from a spoofed Microsoft address. The file was confirmed to contain password-stealer malware. The email was successfully delivered, and the infected host established outbound communication with an external C2 server.


### Timeline (Key Timestamps)

2021-04-26 23:03 — Alert triggered (SOC143: Password Stealer Detected)
2021-04-26 23:05 — Analyst reviewed email header and attachment
2021-04-26 23:10 — Attachment analyzed in sandbox, identified as password stealer
2021-04-26 23:15 — Network logs show outbound C2 connection (81.169.145.105)
2021-04-26 23:20 — Analyst classified as True Positive and closed alert


### Artifacts / Indicators of Compromise (IOCs)

- E-mail Sender: bill@microsoft.com
- E-mail Domain: letsdefend.io
- IP Address: 180.76.101.229 (SMTP origin)
- IP Address: 81.169.145.105 (C2 server)
- URL: http://thuening.de/cgi-bin/uo9wm/
- MD5 Hash: bd05664f01205fa9077f442468a8743a


### Technical Analysis

- The phishing email contained a password-protected ZIP archive labeled "infected".
- Sandbox analysis confirmed the attachment as a password stealer malware.
- Device Action = Allowed, confirming the email reached the user.
- Network logs revealed C2 communication attempts to 81.169.145.105 and thuening.de.
- MITRE ATT&CK techniques:
  - T1566.001 – Spearphishing Attachment
  - T1071.001 – Application Layer Protocol: Web Protocols
  - T1041 – Exfiltration Over C2 Channel


### Mitigation / Response Actions

- Blocked malicious IPs and domains (180.76.101.229, thuening.de, 81.169.145.105)
- Quarantined affected endpoint
- Updated email gateway filters to block password-protected ZIPs
- Informed users about phishing awareness
- Uploaded IOCs to threat intelligence feed


### Recommendations / Next Steps

- Perform full threat-hunting sweep for similar IOCs across environment
- Verify no lateral movement or credential theft occurred
- Conduct user awareness refresher training
- Strengthen attachment filtering policies


### AI Prompt & Response (AI Support Summary)

**Prompt:**
"Analyze LetsDefend SOC143 case and determine whether the password stealer alert is true or false positive. Provide reasoning and IOCs."

**AI Response:**
Analysis confirmed this was a real phishing incident with a malicious ZIP file containing password stealer malware. The attachment hash (bd05664f01205fa9077f442468a8743a) is listed as malicious on VirusTotal. 
Outbound connections to 81.169.145.105 (thuening.de) confirm the file execution and C2 activity. The case is True Positive.


### Case Owner

Ievgen Bondarenko
