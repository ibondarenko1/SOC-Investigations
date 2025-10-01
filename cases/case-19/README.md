# [CASE] VoIP Phishing Call Analysis

### Case ID (slug-friendly)

 001-VoIP

### Case Title

 VoIP Phishing Call Analysis

### Executive summary

A phishing attempt was conducted via a spoofed VoIP call imitating a bank. The attacker attempted to extract sensitive information from the victim (James).

### Timeline (key timestamps)

2024-05-03 20:36:12 UTC — Fake call initiated (INVITE from “Bank”)

2024-05-03 20:36:44 UTC — Call answered by James

2024-05-03 20:38:12 UTC — Call terminated (BYE/200 OK)

### Artifacts / IOCs

Source IP: 192.168.245.128 (Bank – Asterisk PBX)

Destination IP: 192.168.245.130 (James)

James’s phone (SIP URI): sip:7001@192.168.245.130:59836

Bank’s spoofed SIP ID: "Bank" <sip:01326947697@192.168.245.128>

Codec: g711U

Packets (RTP): 13,563

### Technical analysis

RTP stream analysis confirmed ~95 seconds of two-way audio communication.

SIP INVITE messages showed caller identity spoofed as "Bank".

Call metadata exposed James’s SIP number and established session parameters.

Asterisk PBX (20.7.0) identified as call server (attacker infrastructure).

### Actions taken / Mitigation

Identified spoofed SIP caller ID.

Verified bank’s phone number as fraudulent.

Flagged RTP communication as phishing social engineering attempt.

Case logged in SOC repository for reference and training.

### Recommendations / Next steps

Update SIP filters/rules to block spoofed “Bank” caller ID.

Enable SIP authentication enforcement on VoIP server.

Add detection rule in SIEM for INVITE packets from 192.168.245.128.

Educate users on phishing via VoIP and social engineering risks.

### Case owner

Ievgen Bondarenko
