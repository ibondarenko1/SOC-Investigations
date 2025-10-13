# [CASE] SQL Injection Attempt Detected on SQL Server

### Case ID (slug-friendly)

soc142-sqlinjection-2025-10-13

### Case Title

SQL Injection Attempt on Internal SQL Server (SOC142)

### Executive Summary

Alert SOC142 (Multiple HTTP 500 Responses) was triggered when external IP 101.32.223.119 attempted a SQL injection against internal SQLServer (172.16.20.6). 
The malicious payload was observed in the request URL and confirmed as a True Positive attack. The request was allowed and not blocked by proxy.


### Timeline (Key Timestamps)

2021-04-18 13:00 — Alert SOC142 triggered (Multiple HTTP 500 Responses)
2021-04-18 13:05 — Source IP 101.32.223.119 accessed SQLServer 172.16.20.6 via malicious URL
2021-04-18 13:44 — SQLServer (sqlAdmin) active session confirmed
2021-04-18 13:50 — Incident analyzed and confirmed as SQL Injection (True Positive)


### Artifacts / Indicators of Compromise (IOCs)

- Source IP: 101.32.223.119
- Destination IP: 172.16.20.6
- URL: https://172.16.20.6/userNumber=1 AND (SELECT * FROM Users)=1
- User Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 Chrome/79.0.3945.88
- Device Action: Allowed
- Hostname: SQLServer
- MD5 Hash: a2cb77c5d2dd585f7ae7cb3936222d5 (Python3 process from attacker host)


### Technical Analysis

- Proxy logs confirm multiple HTTP 500 responses from SQLServer during injection attempts.
- The injected URL contained a valid SQL query structure consistent with SQLi pattern.
- Elastic/Kibana data and endpoint telemetry verified that source 101.32.223.119 initiated the traffic.
- No command execution or data exfiltration observed post-attack.
- Processes such as python3 and nmap observed on PentestMachine indicate attacker reconnaissance.


### Mitigation / Response Actions

- Blocked source IP 101.32.223.119 at firewall perimeter.
- Reviewed SQLServer logs for suspicious queries and integrity.
- Added WAF rule to block SQLi payloads.
- Updated detection rule in SIEM to auto-classify similar patterns.
- Notified security and DB admin teams for further audit.


### Recommendations / Next Steps

- Conduct review of all exposed web applications for SQLi vulnerabilities.
- Perform vulnerability scan and patch database servers.
- Apply principle of least privilege to SQL accounts.
- Continue monitoring for repeated connection attempts from 101.32.223.0/24.


### AI Prompt & Response (AI Support Summary)

**Prompt:** "Assist in analyzing SOC142 (Multiple HTTP 500 Responses) for SQL Injection detection."
**AI Response:** 
The URL accessed by external IP 101.32.223.119 contained an SQL Injection payload targeting internal SQLServer 172.16.20.6. 
The attack is confirmed as True Positive. 
Recommended blocking attacker IP, enabling WAF filtering, and reviewing logs for further exploitation attempts.


### Case Owner

Ievgen Bondarenko
