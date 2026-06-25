# Phase 5: Reporting and Remediation Roadmap Checklist

## Purpose

This checklist guides the auditor through the final phase of the ICS/OT security assessment: validating findings, generating reports, presenting to stakeholders, and establishing the remediation tracking framework.

**Reference Standards**: ISA/IEC 62443-3-3, NIST SP 800-82r3, ISO/IEC 27019

---

## 1. Finding Validation

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 1.1 | Cross-reference each finding with supporting evidence (PCAPs, screenshots, configuration excerpts, logs) | [ ] | Auditor | Every finding must have at least one piece of verifiable evidence |
| 1.2 | Peer review all Critical and High-severity findings with a second qualified auditor before final report | [ ] | Peer Auditor | Independent verification reduces error and strengthens report credibility |
| 1.3 | Verify CVSS-OT score calculation for each finding -- include OT-specific safety and availability metrics | [ ] | Auditor | Double-check CVSS vector string against CVSS v3.1 specification |
| 1.4 | Map each finding to applicable IEC 62443-3-3 System Requirements (SR) and NIST SP 800-82 controls | [ ] | Auditor | Each finding should reference at least one standard |
| 1.5 | Validate that each finding's severity classification (Critical/High/Medium/Low) is consistent with the OT-specific criteria defined in the technical findings template | [ ] | Auditor | Re-classify if severity criteria changed based on client operational context |
| 1.6 | Review findings with client OT engineers to confirm technical accuracy and operational context before final report | [ ] | Auditor + Client OT | Client review may reveal compensating controls not visible to auditor |

---

## 2. Report Generation

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 2.1 | Complete the Executive Summary using the provided template -- ensure it is written for a CISO/executive audience | [ ] | Auditor | Focus on business risk, not technical jargon |
| 2.2 | Complete the Technical Findings Report using the provided template -- ensure each finding has complete details (description, evidence, impact, recommendation) | [ ] | Auditor | Each finding must be independently actionable by the remediation team |
| 2.3 | Complete the Remediation Roadmap using the provided template -- align timeline with client operational constraints | [ ] | Auditor + Client | Maintenance windows, budget cycles, and procurement lead times affect timeline |
| 2.4 | Verify consistency across all three documents -- no contradictory findings, recommendations, or timelines | [ ] | Auditor | Read all three reports in sequence to check narrative flow |
| 2.5 | Include compliance summary table (IEC 62443 SR mapping, NIST 800-82 alignment, industry-specific regulations) | [ ] | Auditor | This is often the most referenced section by compliance teams |
| 2.6 | Review and redact any sensitive operational details that should not appear in certain report distribution tiers | [ ] | Auditor + Client Security | Consider creating tiered reports: full (CISO), technical (OT eng), sanitized (board) |
| 2.7 | Generate SHA-256 hash of final report package and record in chain of custody documentation | [ ] | Auditor | Ensures report integrity after delivery |

---

## 3. Client Presentation

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 3.1 | Prepare executive presentation slides (10-15 slides maximum) covering: overview, top findings, risk summary, remediation roadmap, next steps | [ ] | Auditor | Keep slides visual -- use the risk rating table and remediation timeline from templates |
| 3.2 | Schedule and conduct presentation to CISO/IT Security leadership (business risk focus) | [ ] | Auditor + Client | Separate from technical deep-dive for OT engineering team |
| 3.3 | Schedule and conduct technical walkthrough with OT engineering team (detailed findings, remediation steps, timelines) | [ ] | Auditor + Client OT | Include hands-on demonstration of findings where possible (in lab environment) |
| 3.4 | Document all feedback, questions, and concerns raised during presentations -- incorporate into final report revision | [ ] | Auditor | Stakeholder feedback may reveal business context that changes remediation priorities |
| 3.5 | Communicate Critical findings to client within 24 hours of discovery (do not wait for final report) | [ ] | Auditor | This should already be done during Phase 4 -- verify it was completed |

---

## 4. Remediation Tracking Setup

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 4.1 | Assign a responsible party (name, not team) for each finding in the remediation roadmap | [ ] | Client OT/IT | Unassigned findings will not be remediated |
| 4.2 | Define measurable KPIs for remediation progress (e.g., % of Critical findings resolved within 30 days) | [ ] | Client Security | Example: "90% of Critical findings remediated within 30 days, 100% within 60 days" |
| 4.3 | Establish remediation tracking mechanism -- ticketing system, spreadsheet, or dedicated GRC platform | [ ] | Client IT/OT | Must be accessible to all remediation stakeholders |
| 4.4 | Define escalation process for findings not remediated by target date | [ ] | Client Security | Escalation path: OT Engineer -> OT Manager -> Plant Manager -> CISO |
| 4.5 | Schedule monthly remediation progress review meetings for the first 6 months post-assessment | [ ] | Client + Auditor | Auditor may attend as advisor or client may self-manage |

---

## 5. Re-Testing Planning

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 5.1 | Define criteria for closing each finding -- what evidence is required to confirm remediation | [ ] | Auditor + Client | Example: "Show updated PLC password policy AND verify no default credentials on re-test" |
| 5.2 | Plan re-testing schedule for Critical and High findings after remediation (recommended: 30-90 days) | [ ] | Client + Auditor | Re-testing validates that fixes are effective and have not introduced new issues |
| 5.3 | Define scope for follow-up assessment (12 months recommended) to verify sustained security posture improvement | [ ] | Client | Annual assessments recommended per NIST SP 800-82 and IEC 62443 guidance |
| 5.4 | Document lessons learned from this assessment for process improvement in future engagements | [ ] | Auditor | What worked well, what could be improved, any methodology adjustments needed |

---

## Phase 5 Completion Sign-Off

| Field | Details |
| :--- | :--- |
| **All findings validated with supporting evidence** | [ ] Yes [ ] No |
| **Executive Summary, Technical Findings, and Remediation Roadmap completed and consistent** | [ ] Yes [ ] No |
| **Client presentations conducted (executive + technical)** | [ ] Yes [ ] No |
| **Remediation tracking mechanism established with assigned responsibilities** | [ ] Yes [ ] No |
| **Re-testing schedule defined for Critical and High findings** | [ ] Yes [ ] No |
| **Final report package delivered with SHA-256 integrity hash** | [ ] Yes [ ] No |
| **Assessment formally closed** | [ ] Yes [ ] No |
| **Auditor Name / Signature** | |
| **Client Project Sponsor Name / Signature** | |
| **Date** | |

**Final Notes:**

[Document any open items, deferred findings, client acceptance of risks, or recommendations for the next assessment cycle.]

---

*Checklist version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
