# [CASE] Phishing URL Accessed from EmilyComp

### Case ID (slug-friendly)

phish-2021-03-22

### Case Title

Phishing URL Accessed by User Ellie (EmilyComp)

### Executive Summary

User ellie on host EmilyComp (172.16.17.49) accessed a confirmed phishing URL (mogagrocol.ru) on March 22, 2021.
The domain was verified as malicious through VirusTotal and URLScan.
The request was allowed, indicating possible user interaction with a phishing page.

### Timeline (Key Timestamps)

2021-03-22 21:23 — SOC141 alert triggered: Phishing URL detected
2021-03-22 21:23 — Source: 172.16.17.49 (EmilyComp)
2021-03-22 21:23 — User: ellie accessed mogagrocol.ru
2021-03-22 21:25 — Analyst confirmed URL as malicious


### Artifacts / Indicators of Compromise (IOCs)

IP: 91.189.114.8
Source IP: 172.16.17.49
URL: http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php
User: ellie@letsdefend.io
Domain: mogagrocol.ru


### Technical Analysis

Review of proxy and endpoint logs confirms access to the phishing domain.

Browser and terminal history show user activity before and after the event.

URL analysis via VirusTotal/URLScan confirms phishing behavior (fake login form under compromised WordPress plugin path).

No evidence of payload download or further compromise at the time of review.


### Mitigation / Response Actions

Marked alert as True Positive in LetsDefend.

Blocked the domain mogagrocol.ru on proxy/firewall.

Notified user ellie and conducted phishing awareness refresher.

Verified endpoint (EmilyComp) with antivirus scan — no active infection found.


### Recommendations / Next Steps

Hunt for similar URLs or IPs (91.189.114.*) across network logs.

Update web-filter and proxy signatures.

Conduct internal phishing simulation and awareness training.

Review firewall egress rules to block outbound traffic to suspicious .ru domains.

### AI Prompt & Response (AI Support Summary)

Prompt:

“Summarize investigation of phishing URL alert SOC141 from LetsDefend and generate GitHub SOC Case.”

AI Response:

The phishing URL (mogagrocol.ru) was accessed by ellie from EmilyComp.
Logs and reputation checks confirmed it as malicious.
The event was categorized as True Positive, with containment and awareness measures applied.

### Case Owner

Ievgen Bondarenko
