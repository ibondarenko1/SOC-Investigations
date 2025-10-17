# [CASE] WinRAR Download from Official Website – False Positive

### Case ID (slug-friendly)

soc119-2025-10-16

### Case Title

WinRAR Download from Official Website – False Positive

### Executive Summary

The alert SOC119 triggered for a detected malicious executable download from https://www.win-rar.com. 
After analysis, the domain and file were verified as legitimate (official WinRAR installer). 
No malicious activity or C2 communication observed. The event is classified as a False Positive.


### Timeline (Key Timestamps)

2025-10-16 10:02 — Alert SOC119 triggered: Malicious Executable File Detected  
2025-10-16 10:15 — URL analyzed via VirusTotal and HybridAnalysis  
2025-10-16 10:25 — No malicious indicators found; confirmed legitimate source  
2025-10-16 10:30 — Alert closed as False Positive


### Artifacts / Indicators of Compromise (IOCs)

- URL: https://www.win-rar.com/postdownload.html?&L=0&Version=32bit
- Source IP: 172.16.17.5
- Destination IP: 51.195.68.163
- Domain: win-rar.com


### Technical Analysis

- Analyzed URL in VirusTotal, URLScan, and HybridAnalysis – no malicious indicators detected.
- Host “SusieHost” shows normal user activity, no suspicious processes or persistence.
- Proxy logs confirm legitimate download behavior from the official vendor domain.
- No outbound C2 or follow-up infection detected in SIEM or endpoint telemetry.


### Mitigation / Response Actions

- Verified domain reputation and digital signature of installer.
- No further containment required.
- Updated detection rule notes to reduce false positives for known safe vendor domains.


### Recommendations / Next Steps

- Whitelist known safe software vendor domains in proxy detection rules.
- Review similar detections for correlation with legitimate software updates.
- Continue monitoring network traffic for unknown outbound connections.


### AI Prompt & Response (AI Support Summary)

**Prompt:**
“Analyze alert SOC119 – Proxy Malicious Executable File Detected from win-rar.com. Verify if it’s legitimate.”

**AI Response:**
The download was verified as legitimate. The domain win-rar.com is the official vendor for WinRAR. 
VirusTotal and HybridAnalysis confirm no malicious indicators. 
Classification: False Positive.


### Case Owner

Ievgen Bondarenko
