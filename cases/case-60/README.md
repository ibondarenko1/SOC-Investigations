# [CASE] Monitoring Gap due to Misconfigured SNMP & Syslog on pfSense

### Case ID (slug-friendly)

monitoring-gap-2025-11-26

### Case Title

Monitoring Failure on pfSense Due to SNMP & Syslog Misconfiguration

### Executive Summary

During routine network availability validation, the SOC identified that SNMP polling and Syslog forwarding from the pfSense firewall were misconfigured.
This resulted in missing telemetry (SNMP OIDs & syslog counters) and reduced monitoring visibility.
Issue was corrected, and monitoring was restored

### Timeline (Key Timestamps)

21:55 — Started working on the lab (NTP, SNMP, Syslog configuration).

22:00 — Checked NTP status on pfSense (Stratum 16, Pool Placeholder).

22:03 — Windows client attempted NTP sync and returned an error.

22:08 — Windows client successfully synchronized time with pfsense.local.com.

22:10 — Tried SNMP discovery in PowerSNMP Manager (Get Request Failed).

22:14 — Reviewed SNMP settings on pfSense; missing Trap fields.

22:19 — Tested SNMP via snmpwalk; pfSense responded correctly.

22:24 — Applied Syslog settings on pfSense.

22:26 — Syslog Viewer received messages (counters updated).

22:29 — Final check completed; NTP, SNMP, and Syslog all operational.

### Artifacts / Indicators of Compromise (IOCs)

Device: pfSense firewall (192.168.1.254)

SNMP Community String: pfSense123

SNMP Port: 161

Syslog Server: Windows host running Syslog Viewer

NTP Host: pfSense.local.com

Failed SNMP discovery logs from PowerSNMP Manager

Successful snmpwalk output confirming recovery

### Technical Analysis

Initial symptom:
PowerSNMP Manager → "Get Request failed – connection attempt failed".

Root cause found:

SNMP service enabled

BUT SNMP Trap settings required Trap Server field even if traps not used

Missing/blank field blocked the SNMP daemon from starting properly

Verification:
Running

snmpwalk -v 2c -c pfSense123 192.168.1.254


returned full OID tree → SNMP operational.

### Mitigation / Response Actions

Configured all required SNMP Trap fields to allow daemon to start

Validated SNMP connectivity using snmpwalk

Confirmed correct SNMP community string

Re-synchronized Windows client time with pfSense

Applied correct Syslog settings & verified incoming logs

Updated monitoring checklist for pfSense configurations

Documented the incident in SOC records

### Recommendations / Next Steps

Implement automated pfSense configuration checks (baseline drift detection)

Set SNMP service health alerts in SIEM

Increase Syslog verbosity for better visibility

Perform weekly validation of NTP/SNMP/Syslog health

Add pfSense log ingestion into Elastic/Wazuh (future MSSP integration)

### AI Prompt & Response (AI Support Summary)

Prompt:
"Review pfSense SNMP/NTP/syslog configuration and identify why SNMP polling and traps are failing."

AI Response:
SNMP service failed to start due to missing Trap Server and Trap String fields in the SNMP Trap section.
Even if traps are not used, pfSense requires these fields for daemon validation.
Once fields were populated and service restarted, SNMP polling succeeded, confirmed by full OID tree in snmpwalk.
Syslog settings appear correct based on counters.
NTP synchronization failure was temporary and resolved automatically.

### Case Owner

Ievgen Bondarenko
