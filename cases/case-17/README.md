# Utilman.exe Winlogon Exploit Attempt (Henry)

**Case ID:** utilman-2025-09-29  
**Host:** Henry (172.16.17.149)  
**Opened by:** Ievgen Bondarenko  
**Status:** Closed (sandbox)

---

## Executive summary
Alert triggered on suspicious use of `Utilman.exe` (LOLBIN) attempting privilege escalation. Adversary tried to add a local administrator account. Investigation confirmed exploitation attempt, but no persistent local account remained. Host was contained, and persistence artifacts were reviewed.

---

## Timeline (key timestamps)
- 2023-06-21 11:02 — Alert triggered (`Utilman.exe exploit attempt`).  
- 2023-06-21 12:24 — Analyst investigated host Henry.  
- 2023-06-21 12:30 — Host contained, persistence entries reviewed.  
- Case closed as **True Positive**.

---

## Artifacts / IOCs
- **IP Address:** 172.16.17.149  
- **Process:** Utilman.exe  
- **Parent Process:** Winlogon.exe  
- **Suspicious Command:** `net user superman onepunch123 /add`  
- **Process Hash:** `ded8fd7f36417f66eb6ada10e0c0d7c0022986e9`  

---

## Technical analysis
- `Utilman.exe` executed as child of `Winlogon.exe`.  
- Suspicious command attempted to add a new local user (`superman`).  
- Verification: no such user was created.  
- Autoruns analysis showed persistence attempt via alternate shells.  

---

## Actions taken
- Host contained in sandbox.  
- Verified no new accounts exist.  
- Persistence entries reviewed and cleared.  
- Alert closed as **True Positive**.  

---

## Recommendations
1. Harden accessibility executables.  
2. Monitor LOLBin usage across hosts.  
3. Add detection for persistence via Winlogon AlternateShells.  

---

## Closure note
**Closure date:** 2025-09-29  
**Owner:** Ievgen Bondarenko  

True Positive — Utilman.exe LOLBin attempt to create local user. No user created, host contained, persistence mitigated.
