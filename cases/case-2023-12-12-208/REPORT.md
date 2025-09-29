# Forced Authentication Attempt (SOC246) (case-2023-12-12-208)

**Case owner:** Ievgen Bondarenko
**Executive summary:** Brute-force attempt detected from external IP 120.48.36.175 targeting /accounts/login on WebServer_Test. Multiple POST requests observed. Attack confirmed as True Positive, but unsuccessful. No Tier 2 escalation required.

---

## 1) Timeline
Dec 12, 2023 02:15 PM – Alert triggered (SOC246 – Forced Authentication Detected).

Dec 12, 2023 02:15–02:06 PM – Multiple POST requests from IP 120.48.36.175 to /accounts/login.

Dec 12, 2023 02:20 PM – Analyst investigation completed, brute-force confirmed, attack unsuccessful.

## 2) Artifacts / IOCs
Source IP: 120.48.36.175

Destination IP: 104.26.15.61

Request URL: http://test-frontend.letsdefend.io/accounts/login

Method: POST

Indicator type: Brute-force login attempts

## 3) Technical analysis
The source IP generated multiple POST requests to the login endpoint in a short timeframe, indicative of brute-force activity. No evidence of successful authentication attempts was found. Endpoint WebServer_Test showed no compromise.

## 4) Actions taken (containment & remediation)
Verified traffic logs for repeated attempts.

Correlated IOC (120.48.36.175) against threat intel feeds (no critical matches found).

Classified event as True Positive, but unsuccessful attack.

No Tier 2 escalation performed.

## 5) Recommendations
Continue monitoring for repeated attempts from the same IP.

Consider blocking 120.48.36.175 at the firewall if activity persists.

Review authentication policy and ensure account lockout thresholds are in place.

## 6) References
- Issue: https://github.com/ibondarenko1/SOC-Investigations/issues/10