# [CASE] VPN Brute Force Incident - Mane Account

### Case ID (slug-friendly)

brute-2025-10-05

### Case Title

Brute Force Attack on VPN (Event ID 162)

### Executive summary

A brute force attack was detected on the VPN service. Multiple failed login attempts were observed from the same external IP address (37.19.221.229), followed by a successful login for the user mane@letsdefend.io
.
The attack originated from an external source and successfully compromised the VPN login credentials.

### Timeline (key timestamps)


2023-06-21 01:51 PM | Alert triggered: "Possible Brute Force Detected on VPN"
2023-06-21 01:52 PM | Source IP 37.19.221.229 identified as external
2023-06-21 01:53 PM | Multiple failed logins followed by successful login detected
2023-06-21 02:10 PM | Analyst confirmed True Positive
2023-06-21 02:20 PM | Host isolation initiated and password reset enforced

<!--EndFragment-->
</body>
</html>

### Artifacts / IOCs

<html>
<body>
<!--StartFragment-->
IP Address | 37.19.221.229 | Source IP of attacker
-- | -- | --


<!--EndFragment-->
</body>
</html>

### Technical analysis

Rule Triggered: SOC210 – Possible Brute Force Detected on VPN

Event ID: 162

Source IP: 37.19.221.229 (External)

Destination IP: 33.33.33.33

Username: mane

Email: mane@letsdefend.io

System: Windows 10 client in domain LetsDefend

Logs Checked: VPN and authentication audit logs (Event ID 4624 & 4625)

Result: Multiple failed attempts (4625) followed by successful login (4624) from the same IP.

Evidence: VPN logs, host process activity (no malicious binaries found).

Conclusion: Successful brute force login confirmed.

### Actions taken / Mitigation

Blocked malicious source IP 37.19.221.229 at the firewall and VPN gateway.

Reset password for the affected user account mane@letsdefend.io
.

Isolated host (172.16.17.210) from the corporate network to prevent lateral movement.

Reviewed VPN logs to confirm no other accounts were compromised.

Implemented account lockout policy to limit repeated login attempts.

Verified EDR logs for suspicious activity — no persistence or malware found.

Informed management and updated incident case documentation in SOC platform.

### Recommendations / Next steps

Blocked source IP 37.19.221.229 on VPN and firewall to stop further login attempts.

Reset credentials for the compromised user account mane@letsdefend.io
.

Enabled Multi-Factor Authentication (MFA) for all VPN users to prevent similar brute force attacks.

Isolated the affected host (172.16.17.210) from the network to prevent possible lateral movement.

Reviewed VPN and authentication logs to ensure no other accounts were accessed from the same source IP.

Verified that no malware or persistence mechanisms were present on the host via EDR review.

Reported incident summary to SOC lead and updated case documentation in GitHub.

### Case owner

Ievgen Bondarenko
