# [CASE] Investigate Web Attack – bWAPP Compromise Attempt

### Case ID (slug-friendly)

webattack-2021-06-20

### Case Title

Web Reconnaissance → Brute-Force → Command Injection on bWAPP Lab

### Executive Summary

During log review of the lab host (192.168.199.5), malicious activity from 192.168.199.2 was detected.
The attacker performed automated web scanning using Nikto, enumerated directories, brute-forced application credentials, and finally exploited a Command Injection vulnerability in phpi.php to execute Windows commands and create a persistent local account.

### Timeline (Key Timestamps)

<html>
<body>
<!--StartFragment-->
Time (+0300) | Event
-- | --
12:36:24 | Nikto automated scan started (Mozilla/5.00 (Nikto/2.1.6)) — Reconnaissance
12:46:24 – 12:50:10 | Multiple POSTs to /bWAPP/login.php — Brute-Force Login attempts
12:50:10 | Successful login (HTTP 302 → portal.php)
12:52:36 | Command Injection executed (whoami)
12:52:46 – 12:52:56 | Enumeration commands (net user, net share)
12:53:13 | Persistence command executed — net user hacker Asd123!! /add

<!--EndFragment-->
</body>
</html>

### Artifacts / Indicators of Compromise (IOCs)

Attacker IP: 192.168.199.2

Target Host: 192.168.199.5

User-Agent: Mozilla/5.00 (Nikto/2.1.6)

Malicious Requests:

/bWAPP/phpi.php?message=%22%22;%20system(%27whoami%27)

/bWAPP/phpi.php?message=%22%22;%20system(%27net%20user%20hacker%20Asd123!!%20/add%27)

Persistence Payload (confirmed pattern):
%27net%20user%20hacker%20Asd123!!%20/add%27

### Technical Analysis

Reconnaissance: Nikto scan performed directory and file probing on /bWAPP/.

Directory Brute-Force: Series of HTTP 404 responses for random extensions (.exe, .java, .show, etc.).

Brute Force Login: Hundreds of POST requests to login.php; success indicated by HTTP 302.

Command Injection: Attacker abused phpi.php?message= parameter with system() calls.

Persistence: Created user hacker with password Asd123!! via Windows net user command.

Impact: Full command execution and account creation on target Windows system.

### Mitigation / Response Actions

Blocked source IP 192.168.199.2 at firewall.

Disabled bWAPP test instance and removed injected user account.

Reviewed server for additional persistence artifacts and malware.

Updated web application firewall rules to detect system( and cmd= patterns.

Hardened PHP configuration (disabled system, exec, popen).

### Recommendations / Next Steps

Patch and harden all web applications before public exposure.

Implement strong credential policy to resist brute force attacks.

Enable SIEM alerting for command injection and “net user /add” signatures.

Conduct developer training on input sanitization and secure coding.

### AI Prompt & Response (AI Support Summary)

Prompt: “Analyze the access.log and determine attack sequence and persistence payload.”
AI Response: Detected Nikto reconnaissance, directory enumeration, login brute force, command injection (whoami → net user hacker Asd123!! /add).
Identified payload: %27net%20user%20hacker%20Asd123!!%20/add%27.
Confirmed MITRE ATT&CK T1059 (Command and Scripting Interpreter) and T1136 (Create Account).

### Case Owner

Ievgen Bondarenko
