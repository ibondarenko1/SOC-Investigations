# [CASE] Suspicious Phishing Email From Vendor

### Case ID (slug-friendly)

phish-2025-09-28

### Case Title

Suspicious Phishing Email From Vendor

### Executive Summary

User reported receiving a suspicious email appearing to come from an external vendor. Email contained a malicious attachment designed to harvest credentials. Potential impact includes unauthorized access to user accounts.

### Timeline (Key Timestamps)

09:12 – User reports suspicious email to IT.

09:18 – SOC receives ticket and begins triage.

09:25 – Malicious attachment detonated in sandbox.

09:32 – Indicators confirmed malicious.

09:40 – Email blocked tenant-wide.

09:51 – User password reset and MFA revalidated.

### Artifacts / Indicators of Compromise (IOCs)

Sender: invoices@vendor-support.co

IP: 203.0.113.45

URL: http://malicious-download.example/

Domain: badsite.biz

SHA-256: abcd3f1290aa34d19f1e2f0ab…

Attachment: invoice_request.pdf.exe

### Technical Analysis

Email spoofed using look-alike domain mimicking known vendor.

Sandbox analysis shows the executable attempts outbound connection to malicious C2 server.

EDR logs show no execution on endpoint (blocked by security policy).

SIEM query confirms no lateral movement or additional recipients targeted.

No suspicious authentication attempts detected post-incident.

### Mitigation / Response Actions

Blocked sender domain in email security gateway.

Isolated user workstation (EDR automated policy).

Forced password reset for reporting user.

Reviewed mail logs and confirmed only one user received message.

Updated phishing detection rule to include new IOC set.

Uploaded malware hash to blocklists (EDR + Firewall).

### Recommendations / Next Steps

Conduct user phishing-awareness refresher training.

Perform environment-wide IOC hunt for related C2 traffic.

Review vendor communication policies to prevent spoofing.

Enhance email filtering rules for executable-in-PDF attachments.

### AI Prompt & Response (AI Support Summary)

Prompt Used:

"Analyze malicious attachment and identify behavior."

AI Response Summary:

The attachment is a disguised executable that downloads additional payloads via Invoke-WebRequest. Behavior aligns with MITRE T1059 – Command and Scripting Interpreter and T1105 – Ingress Tool Transfer. The script attempts to contact the remote domain badsite.biz to retrieve a second-stage credential harvester. Recommended immediate containment and user credential reset.

### Case Owner

Ievgen Bondarenko
