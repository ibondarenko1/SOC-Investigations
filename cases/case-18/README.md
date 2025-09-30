# Utilman.exe Winlogon Exploit Attempt (Henry)

**Case ID:** utilman-2025-09-30  
**Host:** Henry (172.16.17.149)  
**Opened by:** Ievgen Bondarenko  
**Status:** Closed (sandbox)

---

## Executive summary
Attempted privilege escalation via replacement/abuse of `Utilman.exe` (LOLBIN). The actor attempted to create a local administrator account (`superman`) by replacing/using accessibility binary and executing `net user` commands. Containment was performed in the sandbox; no persistent adversary account remains.

---

## Timeline (key timestamps)
- 2023-06-21 10:00 — Suspicious network downloads observed from `103.172.79.74`.  
- 2023-06-21 10:07 — `utilman.exe` rename/copy operations observed (file modification in `C:\Windows\System32`).  
- 2023-06-21 11:02 — Command observed: `net user superman onepunch123 /add`.  
- 2023-06-21 11:03 — Command observed: `net localgroup administrators superman /add`.  
- 2023-06-21 11:05 — Host contained in sandbox and investigation initiated.  
- 2023-06-21 12:30 — Persistence registry entries identified and removed (Autoruns).  
- 2023-06-21 XX:XX — Case closed (sandbox) — evidence collected.

*(Use exact timestamps from exports where required.)*

---

## Artifacts / IOCs
- **Infected host:** `Henry` — `172.16.17.149`  
- **Download / C2 host:** `103.172.79.74` (multiple URLs: `http://103.172.79.74/henry.*`)  
- **Observed commands:** `rename utilman.exe utilman.old`, `copy cmd.exe utilman.exe`, `net user superman onepunch123 /add`, `net localgroup administrators superman /add`  
- **Suspect file hash (SHA256):** `ded8fd7f36417f66eb6ada10e0c0d7c0022986e9`  
- **Persistence location found:** `HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\AlternateShells` → `cmd.exe` (Autoruns)

---

## Technical analysis
EDR and endpoint telemetry show a sequence: external downloads → modification of accessibility binary in `C:\Windows\System32` → execution of commands with SYSTEM context via Winlogon/Utilman path. The `net user` commands were observed, but the account `superman` is **not present** at time of investigation. Autoruns revealed Winlogon alternate shell entry pointing to `cmd.exe` — confirmed persistence mechanism. Host was contained and persistence entries removed in sandbox.

**MITRE ATT&CK mapping:**  
- T1546.010 — Event Triggered Execution: Accessibility Features (Utilman/AlternateShell)

---

## Actions taken (sandbox)
- Host **contained** (EDR) — containment timestamp saved in evidence.  
- Collected and attached evidence: EDR export, terminal history, process list, autoruns export, screenshots.  
- Verified `superman` account does **not** exist (`net user superman` → not found).  
- Identified and removed persistence entries (Autoruns / registry).  
- Recorded IOC list and created sandbox block ticket for `103.172.79.74`.  
- Did **not** perform any production changes.

---

## Recommendations
1. Hunt for the same hash and commands across environment (if moving to prod).  
2. Block `103.172.79.74` in test/prod perimeter when authorized.  
3. Harden detection for LOLBin abuse (Utilman, sethc, osk) and track Winlogon children.  
4. Implement AppLocker / WDAC or rules preventing untrusted writes to `C:\Windows\System32`.  
5. Add SIEM rules for `rename utilman.exe` / `copy cmd.exe utilman.exe` and for `net localgroup administrators` executed from Winlogon context.

---

## Evidence (attached)
- `henry_edr_export_<timestamp>.zip`  
- `terminal.txt` (terminal history)  
- `processes.txt` (process tree export)  
- `autoruns.txt` (Autoruns export before/after)  
- `utilman_hash.txt` (SHA256)  
- Screenshots: `endpoint_info.png`, `process_tree.png`, `autoruns.png`, `terminal_history.png`  

---

## Closure note
**Closure date:** `9.30.2025`  
**Owner:** Ievgen Bondarenko

All mandatory sandbox artifacts were collected and attached. Containment confirmed and persistence removed in sandbox. No new local admin account found. Case closed as **True Positive (sandbox)**.
