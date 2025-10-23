# [CASE] Malicious File Download Attempt – NicolasPRD

### Case ID (slug-friendly)

soc137-2025-03-14

### Case Title

Malicious DOCM File and PowerShell Execution on Endpoint NicolasPRD

### Executive Summary

An alert (SOC137) was triggered for host NicolasPRD (172.16.17.37) after a user attempted to open a malicious Microsoft Word document containing macros.
The attachment attempted to execute a PowerShell command to download and run a remote payload via rundll32.exe.
The antivirus successfully blocked and quarantined the file before execution. No C2 communication was detected.

### Timeline (Key Timestamps)

2021-03-07 16:12 – Suspicious PowerShell process created via WMIC

2021-03-07 16:14 – Execution of rundll32.exe from user AppData folder

2021-03-07 16:16 – 16:18 – Attacker browsed directories and read notes.txt

2021-03-14 19:15 – Alert SOC137: Malicious File/Script Download Attempt triggered and blocked

2021-03-14 19:20 – File quarantined, no outbound C2 traffic detected

### Artifacts / Indicators of Compromise (IOCs)

<html>
<body>
<!--StartFragment--><html><head></head><body>
Type | Value | Comment
-- | -- | --
MD5 Hash | f2d0c66b801244c059f636d08a474079 | Malicious DOCM file INVOICE PACKAGE LINK TO DOWNLOAD.docm
IP Address | 172.16.17.37 | Source endpoint (internal)
Domain | letsdefend.local | Endpoint domain context
File Path | C:\Users\Nicolas\AppData\Local\... | Location of attempted DLL execution

</body></html><!--EndFragment-->
</body>
</html>

### Technical Analysis

PowerShell executed with flags -ExecutionPolicy Bypass -Hidden -IEX, typical for malicious script execution.

The script attempted to load a DLL using rundll32.exe from AppData.

Antivirus blocked the file, marking it as infected (password-protected).

No C2 activity detected in Log Management or Network Action tabs.

Browser history shows only legitimate traffic (Google, StackOverflow, BBC, CNN).

Behavior aligns with a macro-based downloader using PowerShell as a stager.

### Mitigation / Response Actions

Verified that antivirus quarantined the malicious file.

Isolated the endpoint and reviewed PowerShell operational logs.

Performed full system scan and confirmed no active malware remains.

Reset password for user Nicolas.

Added detection rule for PowerShell Bypass + IEX executions.

### Recommendations / Next Steps

Monitor NicolasPRD for 48 hours for any recurring activity.

Hunt for the same hash or PowerShell pattern across the environment.

Conduct phishing-awareness training for end-users.

Review and restrict execution of macros and PowerShell in user context.

### AI Prompt & Response (AI Support Summary)

Prompt:

“Analyze SOC137 alert showing PowerShell command execution and malicious DOCM download.”

AI Response:

The PowerShell command attempted to download a remote script using Invoke-Expression and execute it via rundll32.exe.
The behavior corresponds to MITRE ATT&CK T1059 – Command and Scripting Interpreter (PowerShell).
Antivirus blocked the payload, preventing C2 connection.
Recommended containment and account password reset.

### Case Owner

Ievgen Bondarenko
