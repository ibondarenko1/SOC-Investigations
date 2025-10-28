# [CASE] Multiple Suspicious Access Attempts to /productscreen.html Detected Across Web Servers

### Case ID (slug-friendly)

webscan-2025-10-27

### Case Title

Suspicious Multiple Access Attempts to /productscreen.html

### Executive Summary

During routine web-log analysis in Splunk, multiple client IPs were observed requesting the resource /productscreen.html across three web servers (www1–www3).
The total of 65 unique IP addresses indicates a distributed scanning or enumeration activity possibly linked to reconnaissance before exploitation.


### Timeline (Key Timestamps)

- Email headers show spoofed vendor domain (vendor-support[.]biz)
- Attachment analyzed in sandbox – dropped executable connecting to 203.0.113.45
- EDR flagged "Invoke-WebRequest" download attempt
- SIEM search confirmed similar activity across two other endpoints


### Artifacts / Indicators of Compromise (IOCs)

- Targeted resource: /productscreen.html
- Total unique client IPs: 65
- Example IP addresses:
    • 203.0.113.45
    • 198.51.100.23
    • 192.0.2.56
    • 203.0.113.99
- User-Agent patterns:
    • curl/7.*
    • python-requests/*
    • Mozilla/5.* (mixed browser signatures)
- HTTP methods: GET
- Response codes: 200, 404
- Source servers: www1, www2, www3
- Timestamp range: 2022-09-08 00:00 → 2022-09-09 00:00 UTC
- Detection source: Splunk query  
  `sourcetype=access_combined_wcookie uri_path="/productscreen.html" | stats dc(clientip)`
- MITRE ATT&CK: T1595 – Active Scanning


### Technical Analysis

- Queried Splunk: sourcetype=access_combined_wcookie uri_path="/productscreen.html"
  → stats dc(clientip)=65
- Logs from www1–www3 merged under access_combined_wcookie (≈36 k events)
- Pattern analysis shows repeated GET requests from single IPs within seconds
- No successful login or sensitive-file access detected
- Behavior consistent with automated web-scanning (HTTP 200/404 mix)


### Mitigation / Response Actions

- Added temporary WAF rule blocking repeated requests to /productscreen.html
- Updated rate-limit policy for public endpoints
- Logged offending IPs to threat-intel watchlist
- Reviewed web-server access permissions and sanitized exposed paths
- Confirmed no compromise of backend systems


### Recommendations / Next Steps

- Correlate these IPs with other logs (mail, VPN, firewall) to detect reuse
- Implement anomaly alerts for URI access spikes in Splunk
- Periodically audit public web endpoints for unnecessary exposure
- Review geolocation distribution of inbound traffic


### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze Splunk web logs showing repeated requests to /productscreen.html and determine incident type.”

AI Response:
The pattern represents reconnaissance or automated scanning behavior targeting a specific endpoint.
No exploitation evidence found. Classified as Information Gathering (MITRE T1595).
Recommended defensive actions: rate-limiting, WAF tuning, IOC correlation.

### Case Owner

Ievgen Bondarenko
