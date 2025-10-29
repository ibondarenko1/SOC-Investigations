# [CASE] Exchange Server Compromise via Mailbox Forwarding & Persistence Account

### Case ID (slug-friendly)

exchange-compromise-mail-forwarding-2021-03-07

### Case Title

exchange-compromise-mail-forwarding-2021-03-07

### Executive Summary

Mailbox of user katharine@letsdefend.io was compromised. Attacker configured email forwarding to external address (katharine.isabell@yandex.ru) and accessed the Exchange Server (172.16.20.3). A backdoor user account (backupUser) was created on the server to establish persistence. Plaintext credentials were found in forwarded messages, indicating data exfiltration and high risk of lateral movement. Incident confirmed as True Positive.


### Timeline (Key Timestamps)

2020-09-22 — User received phishing email with malicious attachment.
2021-03-07 17:31 — Mailbox forwarding rule created to katharine.isabell@yandex.ru.
2021-03-07 — Exchange Server terminal history shows:
                 net user backupUser /add
                 net localgroup backupGroup backupUser /add
2021-03-07 — Evidence of plaintext credentials in forwarded messages.
2021-03-07 — External communication to IP 185.125.190.18 observed.


### Artifacts / Indicators of Compromise (IOCs)

E-mail Sender: katharine.isabell@yandex.ru (malicious exfiltration address)
E-mail Domain: yandex.ru
IP: 185.125.190.18 (attacker external host)
IP: 172.16.20.3 (compromised Exchange Server)
User Account: backupUser (unauthorized account created)
Group: backupGroup (used for privilege persistence)
Credentials Extracted (plaintext): root, admin, john, bill (multiple)


### Technical Analysis

The attacker accessed the mailbox and created a forwarding rule to exfiltrate data externally. Exchange Server terminal logs confirm execution of account creation and privilege escalation commands:
    net user backupUser /add
    net localgroup backupGroup backupUser /add

Network logs show outbound communication to external IP 185.125.190.18, indicating possible C2 activity. Forwarded messages contained plaintext account credentials, indicating credential theft and potential lateral movement. The server must be treated as compromised.


### Mitigation / Response Actions

- Removed malicious mailbox forwarding rule.
- Contained Exchange Server (172.16.20.3).
- Removed unauthorized backdoor account (backupUser) and group (backupGroup).
- Blocked external IP 185.125.190.18 and domain yandex.ru at firewall and mail gateway.
- Reset passwords for impacted users, enforced MFA.
- Conducted credential sweep to prevent lateral movement.


### Recommendations / Next Steps

- Perform full forensic analysis of Exchange Server to confirm scope.
- Rebuild or restore Exchange Server from known-good image if integrity cannot be assured.
- Review and tighten external forwarding and mailbox rule policies.
- Enforce phishing and credential security awareness training for users.


### AI Prompt & Response (AI Support Summary)

Prompt: Identify cause and impact of Exchange compromise.

AI Summary:
Incident confirmed as credential compromise leading to mailbox forwarding and persistence via backdoor account. Exfiltration and lateral movement risks detected. Immediate containment and password resets performed.


### Case Owner

Ievgen Bondarenko
