title: "[CASE] Utilman.exe Winlogon Exploit Attempt"
case_id: utilman-2025-09-30
case_title: Utilman.exe Winlogon Exploit Attempt
summary: "Attempted privilege escalation via Utilman.exe (LOLBin). Command executed but no new user created. Host isolated."
timeline: |
  2023-06-21 11:02 — Alert triggered (Utilman.exe exploit attempt)
  2023-06-21 12:24 — Analyst investigated on host Henry
  2023-06-21 12:30 — Host contained, user not created
artifacts: |
  - IP: 172.16.17.149
  - Process: Utilman.exe
  - Parent Process: Winlogon.exe
  - Command: net user superman onepunch123 /add
analysis: |
  Utilman.exe executed as child of Winlogon.exe with suspicious command to add a local user.
  Verified no user was created. Autoruns confirmed persistence attempt.
mitigation: |
  - Isolated host
  - Verified no new user accounts
  - Closed alert as True Positive
recommendations: |
  - Harden accessibility executables
  - Monitor LOLBins usage
  - Review persistence mechanisms
owner: "Ievgen Bondarenko"
