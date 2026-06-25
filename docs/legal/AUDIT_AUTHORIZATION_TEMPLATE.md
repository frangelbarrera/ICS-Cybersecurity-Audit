# Audit Authorization Template

## ICS/OT Security Assessment Authorization Letter

**DISCLAIMER**: This document is a template provided for educational and reference purposes only. It must be reviewed and customized by qualified legal counsel before use in any professional engagement. The authors and contributors assume no liability for its use.

---

### Section 1: Client Information

| Field | Details |
| :--- | :--- |
| **Organization Name** | [Client legal entity name] |
| **Industry Sector** | [e.g., Manufacturing / Energy / Water / Oil & Gas / Chemical] |
| **Primary Facility Address** | [Street, City, State/Province, Country] |
| **Additional Locations in Scope** | [List all facilities / remote sites] |
| **Primary Contact** | [Name, Title, Phone, Email] |
| **Secondary / Escalation Contact** | [Name, Title, Phone, Email] |
| **Emergency Contact (24/7)** | [Name, Phone — required for safety-related stop-work] |

---

### Section 2: Auditor Information

| Field | Details |
| :--- | :--- |
| **Audit Firm / Organization** | [Legal entity name] |
| **Lead Auditor** | [Name, Title] |
| **Certifications Held** | [e.g., GICSP, CISSP, ISA/IEC 62443 Expert, CSSA] |
| **Team Members** | [Name, Role, Certification — list all personnel with network/physical access] |
| **Professional Liability Insurance** | [Carrier, Policy Number, Coverage Amount] |
| **Contact During Engagement** | [Phone, Email, Signal/secure comms] |

---

### Section 3: Authorized Scope of Work

#### 3.1 Systems and Networks in Scope

| System / Zone | Purdue Level | IP Range / Identifier | Assessment Type |
| :--- | :--- | :--- | :--- |
| [e.g., SCADA DMZ] | Level 3.5 | 10.100.50.0/24 | Architecture review, config audit |
| [e.g., Historian Server] | Level 3 | 10.100.30.10/32 | Configuration review only |
| [e.g., HMI Cluster A] | Level 2 | 10.100.20.0/25 | Passive discovery + config audit |
| [e.g., PLC Line 3] | Level 1 | 10.100.10.50/32 | Offline project file review |
| [Add rows as needed] | | | |

#### 3.2 Assessment Activities Authorized

- [ ] Passive network traffic capture and analysis
- [ ] Configuration review of PLC/HMI project files (offline)
- [ ] Network architecture and segmentation review
- [ ] Firewall and ACL rule-set audit
- [ ] User account and access control review
- [ ] Firmware version and vulnerability assessment (read-only)
- [ ] Physical security walk-through
- [ ] Policy and procedure document review
- [ ] Interview of operations and engineering personnel
- [ ] Controlled active discovery (limited to read-only protocol queries)

#### 3.3 Explicitly Excluded Activities

- [ ] Exploitation of vulnerabilities (no proof-of-concept execution)
- [ ] Denial-of-service testing of any kind
- [ ] Modification of process variables, setpoints, or logic
- [ ] Firmware uploads or downloads to any controller
- [ ] Password cracking or brute-force attempts
- [ ] Social engineering of plant personnel
- [ ] Physical tampering with safety instrumented systems (SIS)
- [ ] Any activity on Level 0 devices (sensors, actuators) without explicit written exception
- [ ] [Add additional exclusions]

---

### Section 4: Engagement Period and Authorized Windows

| Item | Details |
| :--- | :--- |
| **Engagement Start Date** | [YYYY-MM-DD] |
| **Engagement End Date** | [YYYY-MM-DD] |
| **Authorized Working Hours** | [e.g., Monday-Friday 08:00-18:00 local time] |
| **Maintenance Windows for Active Testing** | [e.g., Sundays 02:00-06:00 — pre-approved 7 days in advance] |
| **Blackout Periods** | [e.g., Year-end production push, scheduled plant turnaround dates] |

---

### Section 5: Rules of Engagement

#### 5.1 Safety Overrides (Highest Priority)

1. **Immediate Stop-Work Authority**: The client retains the unconditional right to halt all assessment activities at any time, for any reason, without notice. The verbal instruction of any authorized client representative is sufficient.
2. **Safety Instrumented Systems (SIS)**: No assessment activity of any kind shall target, interact with, or connect to any Safety Instrumented System. SIS networks are categorically out of scope.
3. **Production Impact**: If any assessment activity is suspected of causing a process upset, degradation, or anomaly, the activity must be halted immediately and the client notified.

#### 5.2 Data Handling and Confidentiality

- All data collected during the assessment (network captures, configuration files, screenshots, findings) is the exclusive property of the client.
- Data must be stored on encrypted media and transmitted only over encrypted channels.
- No assessment data may be stored on personal devices or cloud services without explicit client authorization.
- Within 30 calendar days of engagement completion, all raw assessment data must be returned to the client or securely destroyed per client instructions.
- The auditor may retain only the final sanitized report for professional records, with client approval.

#### 5.3 Communication Protocol

- Daily stand-up: [Time, attendees, format — in-person/video]
- Findings requiring immediate attention: Direct call to primary contact
- Weekly status report: Written summary to [distribution list]
- Incident communication: [Define escalation path and responsible parties]

#### 5.4 Tools and Equipment

- All assessment devices (laptops, network TAPs, USB drives) must be listed and approved before deployment.
- Devices must run up-to-date, licensed security software.
- No assessment device may connect to the OT network without prior inspection by client IT/OT staff.
- [Attach equipment list as Appendix A]

---

### Section 6: Legal Provisions

#### 6.1 Indemnification

[To be completed by legal counsel — define mutual indemnification terms]

#### 6.2 Limitation of Liability

[To be completed by legal counsel]

#### 6.3 Governing Law

This agreement shall be governed by the laws of [jurisdiction].

#### 6.4 Non-Disclosure

The auditor agrees to maintain confidentiality of all client information, trade secrets, and assessment findings in perpetuity, except as required by law or with written client consent.

---

### Section 7: Signatures

By signing below, the undersigned certify that they have read, understood, and agree to all terms and conditions set forth in this Authorization Letter and its appendices. They further certify that they possess the authority to bind their respective organizations.

**Client Authorization:**

| | |
| :--- | :--- |
| Printed Name: | ______________________________ |
| Title: | ______________________________ |
| Signature: | ______________________________ |
| Date: | ______________________________ |

**Auditor Authorization:**

| | |
| :--- | :--- |
| Printed Name: | ______________________________ |
| Title: | ______________________________ |
| Signature: | ______________________________ |
| Date: | ______________________________ |

**Witness (optional but recommended):**

| | |
| :--- | :--- |
| Printed Name: | ______________________________ |
| Title: | ______________________________ |
| Signature: | ______________________________ |
| Date: | ______________________________ |

---

### Appendix A: Approved Equipment List

| Device | Make/Model | Serial Number | Purpose | MAC Address |
| :--- | :--- | :--- | :--- | :--- |
| | | | | |
| | | | | |
| | | | | |

### Appendix B: Network Diagram Reference

Reference drawing number(s): ______________________________

Drawing revision(s): ______________________________

Date of last update: ______________________________

---

*Template version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
