# [CASE] SOC102 - Suspicious URL Detected (False Positive)

### Case ID (slug-friendly)

soc102-2025-02-22

### Case Title

Suspicious URL Access Detected (False Positive)

### Executive Summary

A proxy alert was triggered due to a URL containing the keyword "phishing" in its path. Investigation confirmed the site (threatpost.com) is a legitimate cybersecurity news publication. No malicious content, downloads, or suspicious system behavior were observed. Incident classified as False Positive.


### Timeline (Key Timestamps)

2025-02-22 08:36 PM — User accessed URL via Chrome browser.
2025-02-22 08:37 PM — Proxy rule SOC102 triggered for suspicious URL pattern.
2025-02-22 08:45 PM — Analyst initiated investigation.
2025-02-22 09:00 PM — URL reputation verified via VirusTotal and URLScan.
2025-02-22 09:05 PM — Process, browser, and network activity reviewed; no threats detected.
2025-02-22 09:10 PM — Incident classified as False Positive and closed.


### Artifacts / Indicators of Compromise (IOCs)

URL: https://threatpost.com/malformed-url-prefix-phishing-attacks-spike-6000/164132/
Domain: threatpost.com (Legitimate, Clean)
Destination IP: 35.173.160.135 (CDN / Akamai)


### Technical Analysis

- Reviewed proxy logs and confirmed URL access from host 172.16.17.150 (user: Chan).
- Browser activity: chrome.exe, no suspicious child processes spawned.
- Verified Outlook.exe and vmware-usbarbitrator.exe binaries referenced in session; both returned 0/72 clean results on VirusTotal.
- No malicious scripts, redirects, payloads, or downloads identified.
- Host network traffic did not show connections to known malicious infrastructure.
- No persistence, credential theft, or command execution indicators found.


### Mitigation / Response Actions

- Verified URL reputation across third-party intelligence services.
- Confirmed no malware execution or file downloads occurred.
- No remediation required.


### Recommendations / Next Steps

- Continue monitoring for repeated high-risk keyword URL alerts to reduce alert fatigue.
- Consider tuning SOC102 rule to avoid false positives for known cybersecurity news domains.
- No further user action required.


### AI Prompt & Response (AI Support Summary)

**Prompt:** "Assist in determining whether the accessed URL is malicious."

**AI Response:** The URL belongs to threatpost.com, which is a reputable cybersecurity news website. No malicious indicators found on VirusTotal, URLScan, or HybridAnalysis. No follow-up malicious behavior was observed on the host. Classify as False Positive.


### Case Owner

Ievgen Bondarenko
