# [CASE] Suspicious Request to Newly Registered Domain

### Case ID (slug-friendly)

soc133-2025-02-28

### Case Title

Suspicious Request to Newly Registered Domain (amesiana.com)

### Executive Summary

A user accessed a newly registered domain (amesiana.com). Reputation and sandbox analysis show no malicious behavior. The request appears user-initiated and no follow-on activity or compromise was detected. Domain was blocked to prevent future access.


### Timeline (Key Timestamps)

2021-02-28 19:57 — User accessed amesiana.com from Chrome browser
2021-02-28 20:00 — Alert SOC133 triggered in proxy logs
2021-02-28 20:05 — Domain analyzed using VirusTotal, URLScan, WHOIS
2021-02-28 20:10 — Endpoint processes/network history reviewed, no malicious activity
2021-02-28 20:12 — Domain blocked and user notified
2021-02-28 20:15 — Case closed (Benign Positive)


### Artifacts / Indicators of Compromise (IOCs)

URL: https://amesiana.com/
IP: 23.227.38.71
User Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64)
Hostname: KatharinePRD (Ubuntu 16.04.4)
Username: leo


### Technical Analysis

- The alert was triggered due to access to a newly registered domain based on proxy traffic rules.
- Browser history indicates the request originated from the user (leo) through Chrome.
- VirusTotal and URLScan analysis show no malware distribution, malicious scripts, or redirects.
- No suspicious processes, persistence, or file modifications were identified on the endpoint.
- No lateral movement or repeated beaconing was observed.
- Activity is consistent with user-initiated browsing curiosity rather than malicious execution.


### Mitigation / Response Actions

- Blocked the domain amesiana.com in outbound proxy
- Added IP 23.227.38.71 to internal deny list
- Reviewed endpoint activity (no compromise found)
- Notified user to avoid unknown newly registered websites


### Recommendations / Next Steps

- Continue monitoring for new or low-reputation domains accessed by internal users
- Reinforce user awareness on suspicious domain access
- Consider enabling automatic new-domain sandbox detonation


### AI Prompt & Response (AI Support Summary)

**Prompt:**
"Investigate SOC133 alert related to suspicious request to newly registered domain."

**AI Response:**
The browsing request originated from user activity and analysis shows no malicious payloads or suspicious scripts. No follow-on network or process activity detected. Domain classified as low reputation but not malicious. Recommend block and close as Benign Positive.


### Case Owner

Ievgen Bondarenko
