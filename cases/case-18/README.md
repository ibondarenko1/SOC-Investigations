# [CASE] Utilman.exe Winlogon Exploit Attempt on host Henry

### Case ID (slug-friendly)

lolbin-2023-06-21

### Case Title

Utilman.exe exploitation attempt to create unauthorized admin account

### Executive summary

Attempted local account creation via Utilman/Winlogon exploit on host Henry (172.16.17.149). Attacker replaced utilman.exe with cmd.exe and executed commands to create a local admin 'superman'. Host was contained in sandbox.

### Timeline (key timestamps)

2023-06-21 10:00:05 — suspicious downloads from 103.172.79.74
2023-06-21 10:07:05 — rename utilman.exe -> utilman.old
2023-06-21 10:07:12 — copy cmd.exe -> utilman.exe
2023-06-21 11:02:12 — net user superman onepunch123 /add
2023-06-21 11:03:14 — net localgroup administrators superman /add
Containment: Host marked "Host Contained" in EDR UI at <вставь timestamp из UI>.

### Artifacts / IOCs

file_hash: ded8fd7f36417f66eb6ada10e0c0d7c0022986e9
ip: 103.172.79.74
example_urls:
  http://103.172.79.74/henry.mpsl
  http://103.172.79.74/henry.x86
account: superman
commands:
  rename utilman.exe utilman.old
  copy cmd.exe utilman.exe
  net user superman onepunch123 /add
  net localgroup administrators superman /add

### Technical analysis

EDR telemetry shows downloads from 103.172.79.74 followed by file operations in C:\Windows\System32 replacing utilman.exe, then execution of account-creation commands from Winlogon context. Process parentage and hash indicate malicious activity. Device action reported as ALLOWED.

### Actions taken / Mitigation

- Host contained in sandbox (timestamp: <вставь>).
- Saved EDR export: henry_edr_export_<timestamp>.zip (attach to issue).
- Terminal/process/network logs saved: terminal.txt, processes.txt, network.txt (attach to issue).
- Verified/removed local user 'superman' (save output; attach).
- IOC list created and attached (ioc.txt).
- No production actions performed (sandbox only).

### Recommendations / Next steps

1. Hunt for hash and commands across environment (if later moving to prod).
2. Block 103.172.79.74 on perimeter (sandbox ticket created).
3. Add detections for utilman replacement + account creation from Winlogon.
4. Consider AppLocker/WDAC to prevent System32 modifications.

### Case owner

Ievgen Bondarenko
