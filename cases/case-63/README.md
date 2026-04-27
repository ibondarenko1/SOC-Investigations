# [CASE] Security Onion PCAP Triage — Lab Job 1001

### Case ID (slug-friendly)

so-pcap-2026-04-18

### Case Title

Security Onion PCAP Triage — Suspicious External Scan Captured in Lab Job 1001

### Environment

SierraLab IT-115 — Security Onion 2.4 sensor (Ubuntu, kali@172.16.16.4) monitoring an internal lab network. Investigation performed against a sensor-side capture, no production data involved.

### Executive Summary

A scheduled Security Onion PCAP capture job (`job 1001`, status `Completed`) was opened for triage during a Linux/SOC lab exercise. The capture contained outbound probing traffic from a lab host toward an external block. Traffic was benign-by-design (lab-controlled), but the workflow exercises the full SOC pipeline: pivot from alert → SO Hunt → PCAP retrieval → flow reconstruction → IOC extraction → write-up.

Recorded SO investigation reference: `hfiuo50BiRBAe-Xkx2dG`.

### Timeline (Key Timestamps, lab time)

- T+0 — PCAP job 1001 reaches `Completed` state in the SO Cases queue.
- T+2m — Case opened in SOC dashboard, severity `medium`, channel `network`.
- T+5m — Hunt query pivot from src IP → top destination ports / connection counts.
- T+10m — PCAP downloaded to analyst host, opened in Wireshark + NetworkMiner.
- T+18m — TCP scan pattern confirmed (SYN bursts across consecutive ports, no ACK from peer).
- T+25m — Case marked `closed-resolved-lab`, no production rule triggered.

### Artifacts / IOCs (lab-scoped)

- SO case ref: `hfiuo50BiRBAe-Xkx2dG`
- PCAP job: `1001` (Completed)
- Sensor host: `kali@172.16.16.4`
- Source IP (lab): `172.16.16.0/24` host
- Capture size: ~ a handful of MB (single window)

No external indicators worth threat-intel publication — this is a controlled lab environment.

### Technical Analysis

1. **Alert pivot.** The PCAP triage workflow in Security Onion starts from a case row, not a raw alert. Job 1001 was selected from the *Cases* dashboard because it was the most recent `Completed` capture. The case ID was preserved and quoted into the writeup so the trail is reproducible later.
2. **Hunt pivot.** Before downloading the PCAP, a Hunt query (`src_ip:172.16.16.4`) was used to confirm there was actual traffic on the wire and that the time window matched the case scope. This is the cheap pre-filter — if Hunt is empty, the PCAP is empty, and you save the download cost.
3. **PCAP download.** Pulled via the SO `so-pcap` interface, opened in:
   - **Wireshark** for stream-level inspection.
   - **NetworkMiner** for parsed assets / file-extraction view.
4. **Pattern.** Outbound probe pattern was characteristic of an `nmap`-style SYN sweep: single source, fanning out across destination ports, no completed handshakes. In a real environment this would map to **MITRE ATT&CK T1046 — Network Service Discovery** and would warrant containment of the source. In lab context it confirmed the capture pipeline end-to-end.
5. **Pipeline verification.** The exercise validated that:
   - PCAP retention is working (`job 1001` was actually present and complete).
   - Sensor-to-analyst handoff works without manual SCP gymnastics.
   - Case linkage from job → narrative → IOC table is reproducible.

### Mitigation / Response Actions

- Confirmed lab-controlled origin; no isolation needed.
- Closed SO case with verdict `lab-validated`.
- Recorded reproducible workflow (case ref + job ID) so the same triage can be re-run for grading / future exercises.

### MITRE ATT&CK Mapping

- **T1046** — Network Service Discovery (matched pattern, lab simulation)

### Lessons Learned

- *Hunt before you PCAP.* Saves time + bandwidth on noisy days.
- *Quote the SO case ref in the writeup.* Without `hfiuo50BiRBAe-Xkx2dG`, this report wouldn't be linkable back to the source-of-truth dashboard.
- *Track PCAP job status*, not just alert IDs — the case dashboard is where lab work is graded, and `Completed` ≠ "you've actually looked at it".

### Tooling

- Security Onion 2.4 (Hunt, Cases, so-pcap)
- Wireshark / tshark
- NetworkMiner
