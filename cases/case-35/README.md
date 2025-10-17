# [CASE] Emotet Malware Infection via Malicious Document

### Case ID (slug-friendly)

emotet-2025-10-16

### Case Title

Emotet Malware Infection Detected on Endpoint RichardPRD

### Executive Summary

A suspicious Microsoft Word document (Iword.doc) was detected downloading a malicious executable (network.exe) from an external URL. 
The file was identified as Emotet malware. Endpoint protection successfully cleaned the infection, and the C2 connection was confirmed.


### Timeline (Key Timestamps)

2025-10-16 09:06 — Alert triggered: Emotet Malware Detected (Event ID 85)
2025-10-16 09:07 — File Iword.doc identified on host RichardPRD
2025-10-16 09:08 — File network.exe downloaded from http://andaluciabeach.net/image/network.exe
2025-10-16 09:09 — C2 connection observed to 5.135.143.133
2025-10-16 09:10 — Endpoint protection cleaned the malicious file
2025-10-16 09:12 — Analyst confirmed True Positive and closed alert


### Artifacts / Indicators of Compromise (IOCs)

- File MD5: 349d13ca99ab03869548d75b99e5a1d0
- URL: http://andaluciabeach.net/image/network.exe
- C2 IP: 5.135.143.133
- Host: RichardPRD
- Internal IP: 172.16.17.45


### Technical Analysis

- The Word document (Iword.doc) triggered a download of network.exe from an external domain.
- The executable exhibited Emotet-like network behavior and communicated with 5.135.143.133.
- Sandbox analysis confirmed Emotet signature.
- Endpoint logs showed the infection was cleaned successfully by the AV engine.


### Mitigation / Response Actions

- Verified that malware was quarantined by endpoint protection.
- Blocked malicious URL and IP at the firewall.
- Checked network logs for lateral movement (no evidence found).
- Recommended email security awareness refresher for the user.


### Recommendations / Next Steps

- Perform retrospective search for similar Emotet indicators.
- Implement YARA or Sigma rule to detect similar payloads.
- Review inbound email filters for malicious attachments.
- Report indicators to threat intelligence sharing platform.


### AI Prompt & Response (AI Support Summary)

**Prompt:**
"Summarize the Emotet infection case and generate a complete SOC investigation report."

**AI Response:**
The investigation confirmed a True Positive Emotet infection. The infection originated from a malicious Word document that downloaded an executable via an external HTTP link. C2 communication was observed and blocked. The malware was cleaned by the endpoint protection. Relevant IOCs were extracted and submitted for blocking.


### Case Owner

Ievgen Bondarenko
