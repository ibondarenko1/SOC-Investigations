# [CASE] SOC101 – Phishing Mail Detected (LetsDefend Simulation)

### Case ID (slug-friendly)

soc101-phish-2021-04-04

### Case Title

Phishing Email Containing Malicious URL Delivered to User

### Executive Summary

A phishing email was detected by rule SOC101 with the subject "Its a Must have for your Phone". 
The email was sent from lethuyan852@gmail.com to mark@letsdefend.io on April 4, 2021, and contained a malicious URL (http://huuangaybantiep.xyz) promoting a fake product. 
The link was confirmed malicious via sandbox analysis. The email was delivered, but there is no evidence of user interaction.


### Timeline (Key Timestamps)

2021-04-04 23:00 — Email detected by SOC101 rule (Phishing Mail Detected)
2021-04-04 23:02 — Security analyst reviewed message header and content
2021-04-04 23:05 — Sandbox analysis confirmed malicious URL (http://huuangaybantiep.xyz)
2021-04-04 23:10 — Verified that no user clicked or accessed the URL
2021-04-04 23:15 — Incident classified as True Positive and alert closed


### Artifacts / Indicators of Compromise (IOCs)

- URL: http://huuangaybantiep.xyz
- Sender: lethuyan852@gmail.com
- IP: 146.56.195.192 (SMTP source)
- Subject: Its a Must have for your Phone
- Domain: huuangaybantiep.xyz (malicious phishing domain)


### Technical Analysis

- The email was sent through a Gmail account using SMTP server at IP 146.56.195.192.
- Message contained a plain-text phishing link (http://huuangaybantiep.xyz).
- Sandbox and reputation checks (VirusTotal, URLHaus) confirmed the URL as malicious.
- Log Management review confirmed no network activity or HTTP requests toward the domain.
- Device Action: Allowed — indicates email was successfully delivered.
- No attachments were present; the malicious vector was a URL link.


### Mitigation / Response Actions

- Blocked sender (lethuyan852@gmail.com) and domain (huuangaybantiep.xyz) at mail gateway.
- Added URL to proxy and firewall blocklist.
- Alerted user (mark@letsdefend.io) and conducted awareness reminder.
- Monitored logs for any attempted outbound connections to the domain.
- Verified no additional emails from same sender observed.


### Recommendations / Next Steps

- Enhance anti-phishing rule set to auto-quarantine messages with similar URL patterns.
- Conduct a short phishing awareness refresher for users.
- Continue monitoring for new campaigns using .xyz domains.
- Add domain and IP to internal threat intelligence database.


### AI Prompt & Response (AI Support Summary)

**Prompt:**
"Assist in analyzing a phishing email detected by SOC101 rule."

**AI Response:**
Identified key IOCs (URL, sender, SMTP IP). Confirmed phishing indicators (malicious link, social engineering lure). 
Determined that the email was delivered but not opened. 
Recommended classification as True Positive (Phishing Email – MITRE ATT&CK T1566.002).


### Case Owner

Ievgen Bondarenko
