# [CASE] Follina Exploitation via Malicious Document on JonasPRD

### Case ID (slug-friendly)

follina-2022-06-02

### Case Title

Malicious Office Document Exploited MSDT (Follina) and Reached C2

### Executive summary

A malicious Word document (05-2022-0438.doc) was executed on host JonasPRD (172.16.17.39). 
The file exploited MSDT (Follina vulnerability CVE-2022-30190) and spawned powershell.exe. 
Outbound connections to known malicious C2 infrastructure (qstride.com, 67.68.210.95, thuening.de) were observed. 
AV allowed execution, no automatic quarantine occurred. Incident confirmed as True Positive.

### Timeline (key timestamps)

2022-06-02 15:13 - User admin logged into host JonasPRD
2022-06-02 15:22 - Malicious document 05-2022-0438.doc opened, msdt.exe executed
2022-06-02 15:22 - powershell.exe spawned from msdt.exe
2022-06-02 15:22 - Outbound HTTP request to qstride.com/img/0/
2022-06-02 15:23 - Outbound connection to 67.68.210.95 (C2) established
2022-06-02 15:24 - Command executed: taskkill /f /im msdt.exe (manual containment)
2022-06-02 15:25 - Temp folder cleanup command observed
2022-06-02 19:48 - Further outbound to 157.240.238.14 (suspicious)

### Artifacts / IOCs

Files & Hashes

05-2022-0438.doc (MD5: 52945af1def85b171870b31fa4782e52)

Parent process MD5: 21b3a9b03027779dc3070481a468b211

Parent process MD5: bac591433cdada740aab065885fd408bc

Processes

msdt.exe (exploited by Office)

powershell.exe (spawned by msdt.exe)

rasser.exe (observed in logs)

Network (C2 Indicators)

http://qstride.com/img/0/

http://67.68.210.95/HX8tpawYAxLaiFMTGa1/...

http://thuening.de/cgi-bin/uo9wm/

IPs: 198.100.45.154, 67.68.210.95, 81.169.145.105, 49.233.160.217

E-mail

Sender: info@nexoiberica.com

Domain: nexoiberica.com

### Technical analysis

Sandbox/EDR/SIEM analysis confirmed malicious activity:
- Malicious document (05-2022-0438.doc, MD5: 52945af1def85b171870b31fa4782e52) executed msdt.exe (Follina exploit, CVE-2022-30190).
- msdt.exe spawned powershell.exe and rasser.exe, observed making outbound HTTP/POST requests.
- C2 communication established with qstride.com, 67.68.210.95, thuening.de, 198.100.45.154, and 81.169.145.105.
- AV logs indicated “Permitted” action (no quarantine).
- Terminal History: manual `taskkill /f /im msdt.exe` and cleanup commands in %temp%.
- Browser/Network logs confirmed suspicious activity following document execution.

### Actions taken / Mitigation

- Isolated host JonasPRD (172.16.17.39) from the network.
- Blocked identified C2 domains/IPs (qstride.com, 67.68.210.95, thuening.de, etc.) at the firewall/proxy.
- Removed malicious document and related processes.
- Collected artifacts (files, hashes, logs, memory dump) for forensic investigation.
- Applied Microsoft security patches for MSDT/Office.
- Reset user admin credentials on JonasPRD.
- Updated EDR/AV signatures and enabled PowerShell ScriptBlock logging.
- Initiated IOC sweep across SIEM/Proxy/EDR for lateral movement detection.

### Recommendations / Next steps

Containment

Isolate host JonasPRD (172.16.17.39) from the corporate network.

Block identified C2 IPs/domains at firewall/proxy.

Eradication

Remove malicious .doc file and related processes.

Apply latest Microsoft patches addressing MSDT/Follina.

Enforce PowerShell restrictions (Constrained Language mode, ScriptBlock logging).

Recovery

Reimage or restore JonasPRD from a trusted backup if compromise confirmed.

Monitor for reoccurring suspicious traffic.

Hunt

Search SIEM/EDR/Proxy logs for same IOCs across all endpoints.

Verify if other hosts received or executed the malicious email/document.

Awareness

Notify end users about malicious attachments via phishing campaigns.

Provide training on recognizing suspicious emails.

### Case owner

Ievgen Bondarenko
