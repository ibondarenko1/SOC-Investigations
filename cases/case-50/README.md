# [CASE] XSS Attempt Against WebServer1002

### Case ID (slug-friendly)

xss-2025-02-26

### Case Title

XSS Injection Attempt Against Internal Web Server

### Executive Summary

An external IP (112.85.42.13) attempted to inject JavaScript code via a search query parameter against WebServer1002 (172.16.17.17). The request contained an XSS payload (<script>alert(1)</script>). The attack was unsuccessful, and no compromise of the server or internal hosts was observed.

### Timeline (Key Timestamps)

Timeline (Key Timestamps)

- Feb 26, 2022 06:56 PM — SIEM alert triggered (SOC166: XSS attempt).
- Feb 26, 2022 07:02 PM — Malicious URL reviewed, XSS payload confirmed.
- Feb 26, 2022 07:08 PM — WebServer1002 EDR checked, no malicious activity found.
- Feb 26, 2022 07:15 PM — Classified as True Positive (attack unsuccessful).
- Feb 26, 2022 07:20 PM — Source IP blocked and hardening recommendations issued.


### Artifacts / Indicators of Compromise (IOCs)

Source IP: 112.85.42.13
Destination: 172.16.17.17 (WebServer1002)
URL: https://172.16.17.17/search/?q=<script>alert(1)</script>
Rule: SOC166 - Javascript Code Detected in Requested URL
HTTP Method: GET
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:40.0) Gecko/20100101 Firefox/40.1


### Technical Analysis

The attacker attempted to perform Cross-Site Scripting (XSS) by injecting JavaScript into the q parameter of the search page.

Reviewing EDR telemetry for WebServer1002 showed:

No unauthorized processes or scheduled tasks.

No outbound callbacks.

No signs of execution of malicious JavaScript on client systems.

The attempt appears to be reconnaissance / scanning, likely automated.

Conclusion:
The attack is classified as True Positive, but unsuccessful. No system compromise detected.

### Mitigation / Response Actions

✔ Added 112.85.42.13 to perimeter temporary blocklist
✔ Confirmed no malicious execution or persistence on WebServer1002
✔ Verified no lateral movement or suspicious client activity
✔ Recommended enabling server-side input sanitization for search parameters
✔ Recommended enabling CSP (Content-Security-Policy) and X-XSS-Protection headers


### Recommendations / Next Steps

Conduct quick review of web application input validation controls.

Ensure front-end and server-side sanitization is consistently applied.

Monitor for repeated scanning from similar IP ranges.

Consider adding WAF rule to block <script> injection attempts.

### AI Prompt & Response (AI Support Summary)

Prompt Used:
"Investigate XSS payload detected in HTTP GET request. Determine whether attack was successful and whether escalation is required."

AI Response:
Confirmed this was a malicious XSS injection attempt. No server compromise was detected. Attack was unsuccessful. No Tier 2 escalation required. Recommended web hardening (CSP, input sanitization) and temporary blocklist action.

### Case Owner

Ievgen Bondarenko
