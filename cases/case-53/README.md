# [CASE] False Positive – LS Command Detected in URL Query Parameter

### Case ID (slug-friendly)

web-ls-url-fp-2025-02-27

### Case Title

False Positive - LS Command Detected in URL

### Executive Summary

An automated detection triggered on a suspected "ls" command within an HTTP request. 
Investigation determined the activity to be benign, caused by the substring "ls" in the legitimate search parameter "?s=skills" while browsing letsdefend.io. 
No evidence of compromise or malicious behavior was found.


### Timeline (Key Timestamps)

2025-02-27 00:36 — HTTP request containing "?s=skills" detected.
2025-02-27 00:40 — Browser history reviewed.
2025-02-27 00:42 — Terminal and process logs reviewed.
2025-02-27 00:45 — No malicious traffic confirmed.
2025-02-27 00:48 — Alert classified as False Positive and closed.


### Artifacts / Indicators of Compromise (IOCs)

Source Host: 172.16.17.46 (EliotPRD)
Destination: 188.114.96.15 (Cloudflare → letsdefend.io)
URL: https://letsdefend.io/blog/?s=skills
User-Agent: Mozilla/5.0 (Linux Ubuntu)
Command History: `date` (benign)


### Technical Analysis

The rule SOC167 triggered upon detecting the substring "ls" in the HTTP request URL parameter "?s=skills". 
Browser history confirmed that the user was viewing legitimate educational blog pages hosted on letsdefend.io. 
Terminal history was reviewed, showing only the execution of the `date` command, with no evidence of shell usage, enumeration attempts, or injected commands. 
Network telemetry showed repeated requests to 188.114.96.15, associated with Cloudflare-hosted letsdefend.io, and no suspicious outbound connections. 
No abnormal processes were identified on the host.


### Mitigation / Response Actions

- Completed full review of browser, process, terminal, and network logs.
- Confirmed no malicious command execution or attack behavior.
- Documented root cause and closed alert as False Positive.


### Recommendations / Next Steps

- Improve detection rule to avoid substring-only matches.
  Example refinement: detect "ls" only when surrounded by shell syntax (`;`, `|`, `&&`, `$()`, `%0A`, etc.).
- No further response actions required.


### AI Prompt & Response (AI Support Summary)

**Prompt:** 
"Help determine whether 'ls' detected in URL request indicates malicious behavior."

**AI Response:** 
The substring "ls" appears within the search query text "?s=skills" on a legitimate domain. No indicators of command injection or exploitation patterns are present. This activity is consistent with normal browsing behavior and should be classified as a False Positive.


### Case Owner

Ievgen Bondarenko
