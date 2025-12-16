...# 🛡️  Security — SOC Investigations Repository

Centralized repository for documenting security incidents, investigations, and AI-assisted SOC workflows.  
This repository reflects professional SOC/MSSP operations using standardized case templates, GitHub Actions automation, and MITRE ATT&CK–aligned investigation methodology.

---

## 📊 Active SOC Cases (Dynamic Counter)

<p align="center">
  <img src="https://img.shields.io/github/directory-file-count/ibondarenko1/SOC-Investigations/cases?label=Active%20SOC%20Cases&style=for-the-badge&color=blue" />
</p>

---

## 📂 Repository Structure

SOC-Investigations/
├── .github/
│ └── workflows/
│ └── new_case.yml # Auto-generates cases from Issues
├── cases/
│ └── <case-id>/ # Generated investigation folders
│ └── README.md # Final SOC case report
├── templates/
│ ├── case_template.md # Manual SOC case template
│ └── issue_template.md # GitHub Issue → Case generator
└── README.md

---

## 🚀 How to Create a New Case

1. Open **Issues → New Case**  
2. Fill in the investigation fields  
3. Add label: **`new-case`**  
4. Submit  

GitHub Action will automatically:

- create a folder under `cases/<case-id>/`  
- generate a complete SOC Case README  
- open a Pull Request  

This ensures consistent, automated SOC documentation.

---

## 🧠 AI-Assisted SOC Pipeline

This diagram shows how AI assists investigations: triage → enrichment → case drafting → analyst validation → auto-storage.

```mermaid
flowchart LR
    A[Alert Generated (SIEM / EDR / Firewall)] --> B{AI Triage}

    B -->|Benign| Z[Auto-Close Alert]
    B -->|Suspicious| C[AI Enrichment]
    B -->|Malicious| D[High Severity Path]

    C --> E[Threat Intel Lookup (VT, AbuseIPDB, URLScan)]
    C --> F[MITRE Technique Mapping]
    C --> G[Context Summary]

    D --> H[Endpoint Isolation]
    D --> I[AI Drafts Initial Case]

    E --> I
    F --> I
    G --> I

    I --> J[Analyst Review]
    J --> K[Create GitHub Issue]
    K --> L[GitHub Action Generates Case Folder]
    L --> M[SOC Case Stored]
    M --> N[Knowledge Base Growth]

🧩 SOC Case Template Structure

Every case includes:

Executive Summary

Timeline

Indicators of Compromise (IOCs)

Technical Analysis

Mitigation & Response Actions

Recommendations / Next Steps

AI Prompt & Response (AI Support Summary)

Case Owner

This ensures full traceability and consistent quality of incident reports.

📘 Purpose

This repository serves as:

A centralized SOC knowledge base

A training tool for developing analyst skills

A real portfolio of incident investigations

A foundation for building automated SOC workflows

A structured documentation system aligned with enterprise IR standards

🛡️ Maintainer

Evgeniy Bondarenko
Security Architect & SOC Lead
Founder — CiberBond Security

🔧 Planned Enhancements

Automated enrichment (VirusTotal, URLScan, AbuseIPDB)

Auto-export incident reports to PDF

MITRE ATT&CK technique heatmaps

AI-generated triage summaries

Integration with SIEM/SOAR pipelines
