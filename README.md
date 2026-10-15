# OT Security Hazard & Risk Analysis – ChemoDemo AG

> **Note:** The analysis and the case-study documents are written in **German**. This README is in English for accessibility.

## Overview

Based on the company's ISMS documentation, the project performs two tasks:

1. **Hazard analysis (*Gefährdungsanalyse*)** – identifies critical assets, assigns relevant threats, and assesses protection needs (confidentiality, integrity, availability, safety) and impact.
2. **Risk analysis (*Risikoanalyse*)** – rates each scenario using **R = S × H** (damage × frequency) in line with BSI Standard 200-3, evaluates its acceptability, proposes measures and calculates the residual risk.

The workbook also includes a note on residual risks and a management summary.



## Repository Contents

```
├── README.md
├── ChemoDemo_OT_Security_Risk_Analysis.xlsx   # Hazard and risk analysis
└── ChemoDemo/                        # Case-study documents (PDF, German)
```

**Workbook sheets**

| Sheet | Content |
|-------|---------|
| `Gefährdungsanalyse` | Asset analysis, threat mapping, protection needs, impact, prioritisation |
| `Risikoanalyse` | Risk model, 30 scenario assessments, proposed measures, residual risk |
| `Hinweis_risiko` | Explanation of risks that cannot be fully reduced |
| `Management_Summary` | Results and recommendations for management |

**Case-study documents (`ChemoDemo/`)**: ISMS guideline, organisational structure, internal references, standards, ISMS overview, security policies, integrated management system, and security architecture.

## Scope

**Assets:** Engineering Station (ES1), external service-provider PC (C1), remote access path, industrial router (R4), MIS server (S3), jump server (S4), and mobile devices/storage media.

**Threats:** manipulation of information, malware, eavesdropping, loss of personnel, and power failure.

## Method

- **Protection-goal priority:** Safety > Availability > Integrity > Confidentiality, following the ChemoDemo ISMS guideline.
- **Damage (S):** 1 negligible, 2 limited, 3 considerable, 4 existence-threatening.
- **Frequency (H):** 1 rare, 2 medium, 3 frequent, 4 very frequent (qualitative).
- **Risk acceptance:**

| R | Class | Acceptance |
|---|-------|------------|
| 1–3 | Low | Acceptable |
| 4–6 | Medium | Acceptable with conditions |
| 7–9 | High | Not acceptable |
| 10–16 | Very high | Not acceptable, immediate action required |

## Key Findings

- The most critical areas are the **Engineering Station**, the **jump server** and **external remote access**.
- Several scenarios reach the "very high" class before measures, mainly malware and manipulation.
- Main causes:
  - no technical compliance check for external clients
  - no security incident management, audits or intrusion detection
  - insecure protocols (Telnet, unencrypted FTP)
  - weak malware protection (active USB ports, yearly signature updates)
- ES1 gives direct PLC access after login without further authentication, which makes it a central point of attack.

## Recommended Measures

- Additional authentication between ES1 and PLCs; four-eyes principle for PLC changes
- Security incident management process and annual security audits
- Replace Telnet with SSH and FTP with SFTP; enforce TLS/NLA for RDP
- Disable USB ports, scan removable media, update virus signatures monthly, add application whitelisting
- Endpoint compliance check (NAC), sandboxed and time-limited sessions, and session monitoring for remote access
- Network monitoring / IDS in the OT network
- Substitute concepts for key personnel and more frequent training

## Residual Risks

After the proposed measures, most scenarios reach an acceptable level. Two remain at **R = 8 (high)** and require a management decision on risk acceptance:

- **ES1 – manipulation of information:** direct PLC access is functionally required.
- **C1 – malware:** the device is operated by the service provider and can only be controlled contractually.

## Usage

Open the `.xlsx` file in Excel or LibreOffice and read the sheets in the order listed above. The PDFs in `ChemoDemo/` provide the background for the analysis.

## Authors

Mouheb Jounaidi, Aziz Hidri

## Disclaimer

ChemoDemo AG is a fictional company. This is an academic project and not a professional security assessment.
