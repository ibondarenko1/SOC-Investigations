# [CASE] SQL Injection Probe Attempt Against WebServer1001

### Case ID (slug-friendly)

sqli-2025-02-25

### Case Title

SQL Injection Probe Detected Against Internal Web Server

### Executive Summary

The monitoring system detected a SQL Injection probe sent from external IP 167.99.169.17 to internal web server 172.16.17.18. The payload (" OR 1=1 --) indicates malicious intent, but the attempt was unsuccessful. No indicators of compromise or post-exploitation behavior were observed.

### Timeline (Key Timestamps)

2025-02-25 11:34 — Alert SOC165 triggered: Possible SQL Injection Payload.
2025-02-25 11:40 — Host WebServer1001 process, network, terminal logs reviewed.
2025-02-25 11:48 — No suspicious processes or persistence mechanisms identified.
2025-02-25 11:52 — Source IP and payload recorded as artifacts; WAF block recommended.
2025-02-25 11:55 — Case closed as True Positive (Unsuccessful Attack).


### Artifacts / Indicators of Compromise (IOCs)

IP Address (Source): 167.99.169.17
IP Address (Destination): 172.16.17.18 (WebServer1001)
URL Requested: https://172.16.17.18/search?q=%22%20OR%201%20%3D%201%20--
Decoded Payload: " OR 1=1 --
MD5: 9ef51c8ad595c5e2a123c06ad39fccd7 (wininit.exe - benign)
MD5: d8e577bf078c45954f4531885478d5a9 (services.exe - benign)
MD5: f586835082f632dc8d9404d83bc16316 (svchost.exe - benign)


### Technical Analysis

The payload used (" OR 1=1 --) is a standard SQL Injection probing signature.

The target service did not perform unintended SQL execution.

Review of host processes showed only expected system binaries.

Terminal history shows legitimate administrative activity (docker-compose build/up).

No evidence of lateral movement, privilege escalation, persistence, or data exfiltration.

Conclusion:
The attack was malicious but unsuccessful. No compromise.

### Mitigation / Response Actions

- Added malicious source IP and payload to artifacts for tracking.
- Recommended blocking or rate-limiting source IP at perimeter (FW/WAF).
- Recommended verifying application uses parameterized SQL queries.
- Verified no follow-up malicious activity within the environment.


### Recommendations / Next Steps

- Implement or tune existing WAF SQLi detection rules.
- Conduct lightweight code review of search endpoint input validation.
- Monitor environment for repeated SQLi probes from similar IP ranges.


### AI Prompt & Response (AI Support Summary)

Prompt:
"Analyze SQL Injection alert and determine if compromise occurred."

AI Response Summary:
External SQL Injection attempt detected. Payload confirms malicious intent, but there is no evidence of successful exploitation or host compromise. Recommend blocking source IP and verifying WAF protections. Case can be closed as True Positive (unsuccessful attack).

### Case Owner

Ievgen Bondarenko
