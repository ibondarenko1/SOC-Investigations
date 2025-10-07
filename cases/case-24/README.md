# [CASE] CVE-2023-29357 Exploitation Attempt on SharePoint Server

### Case ID (slug-friendly)

cve-2023-29357-sharepoint-2025-10-06

### Case Title

Attempted Exploitation of CVE-2023-29357 on MS-SharePointServer

### Executive summary

Alert triggered for possible exploitation attempt of CVE-2023-29357 (Microsoft SharePoint Server Elevation of Privilege).  
The attack originated from an external IP and targeted the internal SharePoint server.  
Investigation confirmed that the attempt was unsuccessful — no signs of compromise or privilege escalation were detected.


### Timeline (key timestamps)

- Source IP: 39.91.166.222
- Destination IP: 172.16.17.233
- URL: /_api/web/siteusers
- User-Agent: python-requests/2.28.1
- Hostname: MS-SharePointServer


### Artifacts / IOCs

- Source IP: 39.91.166.222
- Destination IP: 172.16.17.233
- URL: /_api/web/siteusers
- User-Agent: python-requests/2.28.1
- Hostname: MS-SharePointServer


### Technical analysis

SOC alert SOC227 identified a possible exploitation attempt of CVE-2023-29357 (privilege escalation vulnerability).  
Review of process logs on MS-SharePointServer showed only legitimate Windows processes (smss.exe, winlogon.exe, userinit.exe, svchost.exe) with no anomalies.  
No suspicious PowerShell, CMD activity, or persistence mechanisms were observed.  
Network analysis showed inbound HTTP GET requests from 39.91.166.222 attempting to query SharePoint user enumeration endpoint.  
No outbound or C2 traffic detected.


### Actions taken / Mitigation

- Blocked source IP on firewall.
- Verified system integrity and logins on MS-SharePointServer.
- No Tier 2 escalation required (attack unsuccessful).
- Logged incident for monitoring.


### Recommendations / Next steps

- Continue monitoring external scanning attempts.
- Patch SharePoint Server to latest version mitigating CVE-2023-29357.
- Review and tighten access control for exposed SharePoint endpoints.


### Case owner

Ievgen Bondarenko
