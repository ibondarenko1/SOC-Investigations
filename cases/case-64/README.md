# [CASE] SSH Brute-Force Detection via journalctl

### Case ID (slug-friendly)

linux-bruteforce-2026-04-19

### Case Title

SSH Brute-Force Pattern Detection on Lab Host via systemd journal

### Environment

SierraLab IT-115 Linux SOC lab — Ubuntu host, journal disk size 354.4 MB at start of exercise. Lab is a learning sandbox; all attack traffic was generated against the lab on purpose, all responding services were lab-only.

### Executive Summary

The journal of a lab Ubuntu host was inspected for evidence of repeated authentication failures consistent with an SSH brute-force attempt. `journalctl` filters on `_SYSTEMD_UNIT=ssh.service` and `priority=warning..err` surfaced a clean burst of `Invalid user` / `Failed password` events from a single source. The detection pattern matches **MITRE T1110.001 — Brute Force: Password Guessing**, with no successful login during the captured window (verdict: probe contained, no credential compromise).

### Timeline (Key Timestamps, lab time)

- T+0 — Lab attacker container began SSH login attempts against the Ubuntu host.
- T+0–2m — Burst of `Invalid user <name>` entries written to `/var/log/auth.log` and visible via `journalctl -u ssh -p err..warning`.
- T+5m — Failed-attempt rate dropped (attacker container rotated targets).
- T+30m — Journal rotation trim (size cap reached, oldest archive purged) — relevant for retention discussion in writeup.
- T+45m — Investigation closed: failed-only, no `Accepted password` / `Accepted publickey` from the attacker IP.

### Artifacts / IOCs (lab-scoped)

- Target host: lab Ubuntu (sierralabseconion environment)
- Journal size at investigation start: `354.4M`
- Source pattern: single IP, repeated `sshd[<pid>]: Invalid user <name> from <ip> port <p>`
- Outcome: zero `Accepted password` events for the attacker IP

### Technical Analysis

1. **Filter the journal narrowly.** `journalctl -u ssh.service --since "1 hour ago" --no-pager` is the cheap version; in this case the service unit was `ssh.service` (Debian/Ubuntu naming) — on RHEL-family it would be `sshd.service`. Knowing this distinction up front is part of the lab's value.
2. **Promote signal over noise.** Adding `-p warning..err` removes `info`-level connection accept/close events and leaves the security-relevant subset. For a quick triage:
   ```
   journalctl -u ssh.service -p warning..err --since today --no-pager | head -100
   ```
3. **Confirm the brute-force shape.** A single source repeatedly trying many usernames in seconds is the textbook T1110.001 fingerprint. Two extra checks before declaring it benign:
   - Did any `Accepted password` ever appear from that IP?  (No.)
   - Was there any session with `pam_unix(sshd:session): session opened`? (No.)
4. **Retention sanity check.** Journal had been rotating during the window. Verified `journalctl --disk-usage` (the 354.4M figure) and noted that on a host without persistent journal storage some early failed attempts can drop out of the volatile journal. In production this is why Security Onion / Wazuh / journald-remote forwarders matter — losing the first burst is losing the IOC.
5. **Hand-off shape.** Output of the filtered query was saved as `auth_failures.log` and attached to the SOC case; in production the same evidence path would be `evidence/02_journal_excerpt.txt` so the case folder is self-contained.

### Mitigation / Response Actions

- **Detection rule reminder:** any rule that fires on `>= N failed SSH logins from same IP within T minutes` would have caught this immediately. Default `fail2ban` `bantime=10m, maxretry=5` would have blocked the attacker IP after 5 attempts.
- **Network response:** in a real environment, the host firewall (`ufw deny from <ip>`) plus a temporary edge ACL would be the standard containment.
- **Hardening:** disable password auth (`PasswordAuthentication no` in `/etc/ssh/sshd_config`), enforce keys + MFA at the bastion. Document this even on lab hosts so the muscle memory matches production.

### MITRE ATT&CK Mapping

- **T1110.001** — Brute Force: Password Guessing
- **T1078** — Valid Accounts (would apply if any of the failed usernames had matched a real account; in this lab none did)

### Lessons Learned

- `journalctl -u ssh.service -p warning..err` is the right starting filter — broader filters drown the real signal.
- Always confirm a brute-force is *unsuccessful* before closing — the absence of `Accepted password` is the defining negative evidence.
- Persistent journal (`/var/log/journal/`) matters for IR; volatile journals lose evidence on reboot or rotation.
- The same pattern shape (single source, many usernames, rapid rate) repeats in real-world internet-facing hosts — building this muscle memory in lab is the point.

### Tooling

- `journalctl` (systemd journal)
- `/var/log/auth.log` (Debian/Ubuntu auth source)
- `awk` / `cut` / `sort | uniq -c` for IP frequency rollup
- `fail2ban` (referenced for mitigation, not used in lab)
