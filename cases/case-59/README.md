# [CASE] IDOR Exploitation Against Internal Web Application

### Case ID (slug-friendly)

web-idor-2025-11-26

### Case Title

Successful IDOR Exploitation on Internal WebServer1005

### Executive Summary

An external attacker exploited an Insecure Direct Object Reference (IDOR) vulnerability on the endpoint /get_user_info/ hosted on WebServer1005. By manipulating the id parameter, the attacker accessed multiple user records. HTTP 200 responses and varying response sizes indicated successful unauthorized data retrieval. Tier 2 escalation required due to confirmed data exposure.

### Timeline (Key Timestamps)

2025-11-26 10:46 AM – SOC169 alert triggered (Possible IDOR Attack Detected).

2025-11-26 10:48 AM – Repeated sequential GET/POST requests observed against /get_user_info/.

2025-11-26 10:49 AM – Response sizes differ per request → indicates access to different user records.

2025-11-26 10:55 AM – Analyst validates attack as malicious and successful.

2025-11-26 11:00 AM – Tier 2 escalation initiated.

### Artifacts / Indicators of Compromise (IOCs)

IP Address (Attacker):
134.209.118.137
External IP performing sequential IDOR requests.

URL Address (Target Endpoint):
https://172.16.17.15/get_user_info/
Endpoint vulnerable to IDOR; used to enumerate user data.

### Technical Analysis

Attack Vector

IDOR (Insecure Direct Object Reference)

Attack Behavior

Attacker sent multiple requests with incrementing IDs:
?id=1, ?id=2, ?id=3, etc.

HTTP status code: 200 OK for all requests.

Response sizes differ, confirming access to different user data.

Host Investigation (WebServer1005)

Processes: all legitimate (Chrome, Outlook, svchost, services, explorer, etc.)

Terminal History: only normal admin Docker commands.

Network Activity: no malware callbacks; only connection to documentation sites (Docker, Namecheap).

Browser History: typical administrative activity.

Severity Justification

Confirmed unauthorized access to internal sensitive data.

Attack executed from external network → high risk.

No privilege escalation detected, but exposed PII/user data.

### Mitigation / Response Actions

Immediate Actions

Initiated Tier 2 escalation.

Flagged attacker IP for blocking at WAF/Firewall.

Logged event for audit and compliance tracking.

Notified Web Development team of critical IDOR vulnerability.

Remediation Requirements

Implement proper authorization checks on /get_user_info/.

Disable direct object references; replace with indirect IDs or tokens.

Deploy input validation and RBAC on API endpoints.

Add rate-limiting for external client requests.

Containment

No malware detected on internal server.

No privilege escalation beyond data access.

Data exposure confirmed → escalation mandatory.

### Recommendations / Next Steps

Perform full API security review across all endpoints.

Conduct application penetration test focusing on authentication/authorization failures.

Implement WAF rules for parameter tampering and enumeration patterns.

Train development team on secure coding practices (OWASP Top 10).

Monitor for follow-up activity from attacker IP ranges.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze the SOC169 IDOR alert and determine whether the attack was successful. Provide IOCs and remediation.”

AI Response:
AI identified sequential ID manipulation with 200 OK responses and variable response sizes. This indicates successful IDOR exploitation and unauthorized access to multiple user records. Recommended blocking attacker IP, fixing authorization logic, and escalating to Tier 2.

### Case Owner

Ievgen Bondarenko
