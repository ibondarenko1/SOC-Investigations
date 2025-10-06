# [CASE] FakeGPT Malicious Chrome Extension

### Case ID (slug-friendly)

soc202-fakegpt-2025-10-05

### Case Title

FakeGPT Malicious Chrome Extension

### Executive summary

User "Samuel" installed a malicious Chrome extension impersonating ChatGPT (FakeGPT). The extension attempted to exfiltrate data and communicate with external IPs. Malware was quarantined and user account was secured.

### Timeline (key timestamps)

2023-05-29 13:01 — FakeGPT extension installed
2023-05-29 13:02 — Network connections to 52.76.101.124, 18.140.6.45, 172.217.17.142
2023-05-29 13:10 — User accessed chat.openai.com
2023-05-29 13:11 — Antivirus detected and quarantined malicious extension

### Artifacts / IOCs

- File: hacfaophiklaeolhnmckojjjbnapppen.crx
- File path: C:\Users\LetsDefend\Download\hacfaophiklaeolhnmckojjjbnapppen.crx
- File hash: 742f19abe5e618a0d517861f4709df5329a5f137053a227bfb4eb8e152a4669
- IPs: 52.76.101.124, 18.140.6.45, 172.217.17.142
- Domain: chat.openai.com (legitimate), hacfaophiklaeolhnmckojjjbnapppen (malicious)


### Technical analysis

- Detected rule: SOC202 - FakeGPT Malicious Chrome Extension
- Hostname: Samuel (172.16.17.173)
- OS: Windows 10, domain LetsDefend
- Several Chrome and Windows processes observed (chrome.exe, svchost.exe, explorer.exe)
- Network connections initiated to suspicious IPs after installation
- Extension mimicked ChatGPT but redirected data externally
- Antivirus flagged and quarantined malicious CRX file


### Actions taken / Mitigation

- Blocked malicious IP addresses
- Quarantined infected Chrome extension
- Verified antivirus logs (malware cleaned)
- Instructed user to remove unauthorized browser extensions
- Reset browser sync and user credentials


### Recommendations / Next steps

- Review browser extension policies
- Educate users on verifying legitimate Chrome extensions
- Monitor outbound network connections for suspicious behavior
- Hunt for similar CRX files using file hash
- Add IOC indicators to SIEM threat database


### Case owner

Ievgen Bondarenko
