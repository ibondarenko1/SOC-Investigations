# [CASE] Failed Exploitation Attempt – Suspicious Autodiscover PowerShell Request (SOC175)

### Case ID (slug-friendly)

soc175-2025-11-18

### Case Title

Failed Exploitation Attempt on Exchange – Suspicious Autodiscover Request Containing PowerShell Keyword

### Executive Summary

A suspicious autodiscover request containing the keyword “powershell” triggered alert SOC175 (Possible CVE-2022-41082 exploitation) against Exchange Server 2. 
The request originated from an external IP address and was blocked by IIS before execution. No malicious activity or indicators of compromise were identified on the endpoint.


### Timeline (Key Timestamps)

2025-09-30 07:19 — SOC175 alert triggered on Exchange Server 2.
2025-09-30 07:20 — Analyst reviewed HTTP request and rule context.
2025-09-30 07:25 — Endpoint processes, PowerShell history, and logs examined. No malicious execution observed.
2025-09-30 07:32 — Network connections analyzed; no additional traffic from offending IP.
2025-09-30 07:40 — Case classified as False Positive (unsuccessful exploitation attempt).


### Artifacts / Indicators of Compromise (IOCs)

URL:
    /autodiscover/autodiscover.json?@evil.com/owa/&Email=autodiscover/autodiscover.json%3f@evil.com&Protocol=XYZ&FooProtocol=powershell
Comment:
    Suspicious autodiscover request containing “powershell” keyword (triggered SOC175).

IP Address:
    58.237.200.6
Comment:
    Source IP of attempted exploitation request.

Hostname:
    Exchange Server 2 (172.16.20.8)
Comment:
    Target of the HTTP request; no compromise observed.

Hashes Verified:
    E9CABAAACF0E50A55DF49698C0800D4B (legitimate Chrome binary)
    aba0a9709e6c11bc0b6ee21de36743e3
    FC2EA5BD5307D2CFA5AAA38E0C0DDCE9
    7353f60b1739074eb17c5f4dddefe239
    357b03e0b8d0c30713f2c41ce60583c5
Comment:
    All hashes correspond to legitimate processes; no malware present.


### Technical Analysis

• The alert SOC175 indicated a possible exploitation attempt of CVE-2022-41082 (ProxyNotShell) via a crafted autodiscover request.
• HTTP method was GET, while the real exploit chain requires POST + PowerShell RCE.
• IIS logs show the request was blocked before reaching Exchange or triggering backend execution.
• Endpoint process analysis revealed only legitimate processes: Chrome, Adobe Reader, ccsvchst.exe, notepad.exe, and benign PowerShell commands.
• PowerShell history showed no encoded payloads, downloads, or malicious scripting.
• Network analysis identified no follow-up connections from the same external IP address.
• No webshell behavior, process injection, or suspicious DLL loads were detected.
• Browser history and system activity showed normal administrative usage.
• Overall result: attempted but unsuccessful exploit; no compromise detected.


### Mitigation / Response Actions

• Confirmed the request was blocked by IIS before execution.
• Validated endpoint integrity via process history, PowerShell logs, and network review.
• Verified no lateral movement, persistence, or malicious execution occurred.
• Added offending URL and IP to monitoring for future correlation.
• Documented investigation and closed alert as False Positive (unsuccessful exploitation attempt).


### Recommendations / Next Steps

• Continue monitoring for repeated autodiscover exploitation attempts.
• Ensure all Exchange security patches are up to date (CVE-2022-41040 / CVE-2022-41082).
• Review external firewall rules for unnecessary exposure of autodiscover endpoints.
• Implement additional rate limiting or WAF rules for suspicious autodiscover patterns.


### AI Prompt & Response (AI Support Summary)

**AI Prompt:**
“Provide technical analysis for a suspicious autodiscover request containing the keyword ‘powershell’ and determine whether CVE-2022-41082 exploitation occurred.”

**AI Response:**
The request resembles part of the ProxyNotShell exploitation chain, which attempts PowerShell RCE via Exchange autodiscover. However, the method used (GET) is insufficient for exploitation, and no backend PowerShell execution occurred. Endpoint telemetry shows no indicators of compromise, no malicious processes, and no further traffic from the source IP. The event reflects an attempted—but unsuccessful—exploit.


### Case Owner

Ievgen Bondarenko
