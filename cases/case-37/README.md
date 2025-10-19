# [CASE] Phishing Email with Malicious Attachment (aaronluo@cmail.carleton.ca)

### Case ID (slug-friendly)

phish-2021-03-21

### Case Title

Malicious Email Blocked - COVID19 Vaccine Phishing

### Executive Summary

A phishing email was detected and blocked by the mail security gateway.
The message originated from aaronluo@cmail.carleton.ca and contained a password-protected malicious attachment (password: infected).
No user interaction occurred as the message was successfully blocked before delivery.

### Timeline (Key Timestamps)

2021-03-21 12:26 PM: Alert triggered — phishing email detected.

2021-03-21 12:26 PM: SIEM flagged suspicious attachment and blocked delivery.

2021-03-21 12:30 PM: Analyst confirmed malicious indicators.

2021-03-21 12:45 PM: Case documented and closed as True Positive.

### Artifacts / Indicators of Compromise (IOCs)

Sender: aaronluo@cmail.carleton.ca

Domain: cmail.carleton.ca

IP: 189.162.189.159

MD5: 72c81cf21909a48eb9cceb9e04b865d (COVID19 Vaccine)

MD5: 6c710ea05ee2fd01ec10d45b4f0d86b6 (Invoice)

MD5: 5a3de19f198269947bb509152678b7d2 (UPS Status)

### Technical Analysis

The email contained a password-protected ZIP file designed to evade antivirus scanning.

Each attachment was analyzed in a sandbox and confirmed to contain malware.

The sender attempted to lure recipients using urgent or emotional topics (COVID-19, invoices, package delivery).

SIEM correlation showed multiple attempts from the same address targeting different users.

### Mitigation / Response Actions

Blocked sender and domain at mail gateway.

Verified no successful delivery occurred.

Logged IOCs in threat intelligence system.

No further remediation required.

### Recommendations / Next Steps

Conduct phishing awareness training for users.

Add new IOCs to detection rules.

Continue monitoring for related campaigns using same domain or IP.

### AI Prompt & Response (AI Support Summary)

Prompt:
“Analyze phishing email from aaronluo@cmail.carleton.ca with password-protected attachment.”

AI Response:
Identified pattern of malicious attachments disguised as legitimate messages (COVID-19, invoice, UPS delivery).
The sender’s activity and password-protected archives are consistent with known phishing malware campaigns.
Confirmed as a True Positive phishing attempt.

### Case Owner

Ievgen Bondarenko
