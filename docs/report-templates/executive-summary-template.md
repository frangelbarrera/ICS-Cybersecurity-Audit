# Executive Summary Template

## ICS/OT Security Assessment -- Executive Summary

---

### Assessment Overview

| Field | Details |
| :--- | :--- |
| **Client Organization** | [Name] |
| **Industry / Sector** | [Manufacturing / Energy / Water / Oil & Gas / Chemical / Other] |
| **Facility / Site Assessed** | [Name and location] |
| **Assessment Period** | [Start date] to [End date] |
| **Assessment Methodology** | ICS-Cybersecurity-Audit Framework (5-Phase Approach) |
| **Applicable Standards** | IEC 62443-3-3, NIST SP 800-82 Revision 3 |
| **Lead Auditor** | [Name, Certification] |
| **Assessment Type** | [Architecture Review / Configuration Audit / Full Assessment] |

---

### Executive Context

[Provide 2-3 paragraphs summarizing the engagement context: why the assessment was conducted, the scope of systems reviewed, the methodology applied, and the overall security posture observed. Frame this for a CISO or executive audience -- focus on business risk, not technical detail.]

Example structure:
- **Paragraph 1**: Why this assessment was commissioned and what was in scope (Purdue Levels reviewed, number of systems, key objectives).
- **Paragraph 2**: High-level summary of the security posture -- what was working well, what needs attention.
- **Paragraph 3**: The path forward -- key recommendations and expected outcomes from remediation.

---

### Overall Risk Rating

The following risk ratings reflect the current security posture of the assessed OT environment. Ratings consider safety impact, operational availability, and potential financial consequences.

| Domain | Rating | Status | Key Concern |
| :--- | :---: | :--- | :--- |
| **Network Segmentation** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |
| **Access Control & Authentication** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |
| **Asset & Patch Management** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |
| **PLC / Controller Hardening** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |
| **HMI / SCADA Hardening** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |
| **Remote Access Security** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |
| **Physical Security** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |
| **Incident Response Readiness** | [Critical / High / Medium / Low] | [Red / Yellow / Green] | [One-line summary] |

**Rating Legend:**

| Rating | Symbol | Description |
| :--- | :---: | :--- |
| **Critical** | Red | Active exploit path exists; immediate safety or production risk; requires emergency remediation |
| **High** | Red | Significant security gap; likely exploitable; remediate within 30 days |
| **Medium** | Yellow | Defense-in-depth gap; limited exploitability; remediate within 90 days |
| **Low** | Green | Best practice deviation; low risk; remediate within 180 days |

---

### Top 5 Critical Findings

| # | Finding | Impact | Affected System(s) | Recommended Timeline |
| :---: | :--- | :--- | :--- | :--- |
| 1 | [Finding title] | [Safety / Production / Data loss / Compliance] | [System / Zone] | [e.g., Immediate -- within 7 days] |
| 2 | [Finding title] | [Safety / Production / Data loss / Compliance] | [System / Zone] | [e.g., Short-term -- within 30 days] |
| 3 | [Finding title] | [Safety / Production / Data loss / Compliance] | [System / Zone] | [e.g., Short-term -- within 30 days] |
| 4 | [Finding title] | [Safety / Production / Data loss / Compliance] | [System / Zone] | [e.g., Medium-term -- within 90 days] |
| 5 | [Finding title] | [Safety / Production / Data loss / Compliance] | [System / Zone] | [e.g., Medium-term -- within 90 days] |

---

### Compliance Summary

| Standard / Framework | Compliance Level | Key Gaps |
| :--- | :--- | :--- |
| **IEC 62443-3-3 (SR 1-7)** | [e.g., 65% of applicable SR met] | [Top 3 missing requirements] |
| **NIST SP 800-82r3** | [e.g., Partial alignment] | [Top 3 control gaps] |
| **Industry-specific regulation** | [e.g., NERC CIP, CFATS, TSA SD] | [Compliance gaps] |

---

### Remediation Roadmap Summary

| Phase | Timeline | Focus Areas | Expected Risk Reduction |
| :--- | :--- | :--- | :--- |
| **Immediate** | 0-30 days | Critical findings requiring emergency action | High -- address active risks |
| **Short-term** | 30-90 days | High-severity findings, architectural improvements | Medium -- close key security gaps |
| **Medium-term** | 90-180 days | Medium-severity findings, process improvements | Moderate -- strengthen defense in depth |
| **Long-term** | 180+ days | Low-severity findings, program maturation | Incremental -- continuous improvement |

---

### Priority Recommendations

1. **[Recommendation 1]**: [Description, expected effort, expected impact]
2. **[Recommendation 2]**: [Description, expected effort, expected impact]
3. **[Recommendation 3]**: [Description, expected effort, expected impact]
4. **[Recommendation 4]**: [Description, expected effort, expected impact]
5. **[Recommendation 5]**: [Description, expected effort, expected impact]

---

### Next Steps

1. Review and prioritize findings with OT engineering, IT security, and plant management stakeholders.
2. Approve the remediation roadmap with executive sponsorship.
3. Initiate immediate-term actions within 7 business days.
4. Schedule a 30-day progress review with all stakeholders.
5. Plan a follow-up assessment to validate remediation effectiveness (recommended within 12 months).

---

### Statement of Limitations

This assessment represents a point-in-time evaluation based on the scope, access, and time constraints defined in the Authorization Scope document. It does not guarantee the absence of vulnerabilities beyond those identified. Continuous monitoring and periodic reassessment are essential components of a mature OT security program.

---

**Auditor:**

Name: _________________________

Signature: _________________________

Date: _________________________

---

*Template version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
