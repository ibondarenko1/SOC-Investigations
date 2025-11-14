# [CASE] SOC129 – Successful Local File Inclusion (LFI) Attempt

### Case ID (slug-friendly)

soc129-lfi-2025-11-14

### Case Title

Successful Local File Inclusion Attempt on Web Application

### Executive Summary

An external threat actor attempted to exploit a Local File Inclusion (LFI) vulnerability on the internal web server 172.16.20.4. The attacker issued a directory traversal payload targeting the /etc/passwd file. The request was detected and flagged by security monitoring. No further malicious activity or internal compromise was observed.


### Timeline (Key Timestamps)

2025-02-21 05:02 PM — LFI payload received by web server
2025-02-21 05:02 PM — SIEM triggered SOC129 alert
2025-11-14 05:44 AM — Analyst reviewed logs and investigated access
2025-11-14 05:55 AM — Case classified as False Positive according to training scenario


### Artifacts / Indicators of Compromise (IOCs)

- URL: http://172.16.20.4/srcCode/show.php?page=../../../../../../etc/passwd
- Source IP: 49.234.71.65
- Host: 172.16.20.4 (gitServer)


### Technical Analysis

- Reviewed SIEM alert SOC129 indicating a path traversal attempt.
- Observed malicious URL containing directory traversal payload to read /etc/passwd.
- Log Management review shows no internal hosts accessed this URL.
- No evidence of lateral movement, malware execution, or unauthorized file access.
- In the training environment, the event is categorized as a non-impacting probe without successful exploitation.
- Endpoint analysis indicates no correlation to workstation/server activity for this event.


### Mitigation / Response Actions

- Validated that the target system did not serve sensitive file contents internally.
- Confirmed no user accounts or internal systems interacted with the malicious URL.
- Documented IOCs for future detection tuning.
- Ensured application-level input validation requirements are present for production environments.


### Recommendations / Next Steps

- Perform periodic audits of web server input validation logic.
- Implement WAF rules to block directory traversal payloads.
- Continue monitoring for repeated attempts or similar IOCs.
- Review application logs for anomalies around authentication or file access.


### AI Prompt & Response (AI Support Summary)

**Prompt:**
"Analyze LFI attempt detected by SIEM under alert SOC129."

**AI Response:**
The URL contains an LFI directory traversal payload attempting to read /etc/passwd. 
Based on logged activity, no internal devices accessed the malicious URL and no successful exploitation 
of internal resources was observed. In the context of the training environment, this event can be 
classified as a non-impactful attempt (False Positive). No follow-up malicious activity was identified.


### Case Owner

Ievgen Bondarenko
