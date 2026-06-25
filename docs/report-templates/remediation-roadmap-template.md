# Remediation Roadmap Template

## ICS/OT Security Assessment -- Remediation Roadmap

---

### Document Control

| Field | Details |
| :--- | :--- |
| **Client** | [Organization Name] |
| **Assessment Reference** | [Engagement ID] |
| **Report Date** | [YYYY-MM-DD] |
| **Version** | 1.0 |
| **Classification** | Confidential -- Client Proprietary |

---

### Prioritization Criteria

Findings are prioritized based on the following weighted factors:

| Factor | Weight | Description |
| :--- | :---: | :--- |
| **Safety Impact** | 40% | Potential for personnel injury, loss of life, or environmental damage |
| **Exploitability** | 25% | Ease of exploitation, availability of public exploits, required access level |
| **Production Impact** | 20% | Potential for downtime, production loss, equipment damage |
| **Regulatory / Compliance** | 15% | Violations of NERC CIP, CFATS, TSA SD, or other mandated requirements |

**Priority Calculation:** `(Safety * 0.4) + (Exploitability * 0.25) + (Production * 0.2) + (Compliance * 0.15)` -- each scored 1 (low) to 10 (critical). Higher scores = higher remediation priority.

---

### Remediation Phases

---

#### Phase 1: Immediate (0-30 Days)

Critical findings requiring emergency action. These represent active risks to safety, production, or compliance.

| Priority | Finding ID | Title | Recommended Action | Responsible Team | Target Date | Status |
| :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| 1 | ICS-2026-001 | Default Credentials on PLC Engineering Interface | Change all PLC passwords during next maintenance window; document in secured vault | OT Engineering | [Date] | [ ] Open / [ ] In Progress / [ ] Complete |
| 2 | ICS-2026-002 | Missing Network Segmentation IT-OT | Deploy emergency ACLs limiting IT-to-OT traffic to essential services only; begin IDMZ design | IT Security + OT Engineering | [Date] | [ ] Open / [ ] In Progress / [ ] Complete |
| [3] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| [4] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| [5] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |

**Phase 1 Success Criteria:**
- All Critical-severity findings addressed or have compensating controls in place
- Zero default credentials on any in-scope asset
- IDMZ design approved and procurement initiated
- Emergency ACLs verified and documented

---

#### Phase 2: Short-Term (30-90 Days)

High-severity findings requiring prompt remediation. These close significant security gaps.

| Priority | Finding ID | Title | Recommended Action | Responsible Team | Target Date | Status |
| :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| 1 | ICS-2026-003 | Unencrypted OT Protocols on Control Network | Deploy OT-aware IDS (Zeek/Suricata); begin planning secure protocol migration for next controller refresh | OT Security | [Date] | [ ] Open / [ ] In Progress / [ ] Complete |
| 2 | ICS-2026-004 | EOL Firmware on Critical PLC | Establish support contract; schedule firmware upgrade during planned outage; implement interim compensating controls | OT Engineering | [Date] | [ ] Open / [ ] In Progress / [ ] Complete |
| [3] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| [4] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| [5] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |

**Phase 2 Success Criteria:**
- All High-severity findings addressed or have approved exception with compensating controls
- OT-aware network monitoring deployed and generating alerts
- Firmware lifecycle management process documented and approved
- Vendor support contracts established for all critical Level 1 assets

---

#### Phase 3: Medium-Term (90-180 Days)

Medium-severity findings requiring systematic improvement. These strengthen defense in depth.

| Priority | Finding ID | Title | Recommended Action | Responsible Team | Target Date | Status |
| :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| 1 | ICS-2026-005 | Insufficient Audit Logging on SCADA Servers | Deploy centralized OT log collector/SIEM; configure SCADA audit trails; define retention policy | OT Security + IT Security | [Date] | [ ] Open / [ ] In Progress / [ ] Complete |
| [2] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| [3] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| [4] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| [5] | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |

**Phase 3 Success Criteria:**
- Centralized OT log collection operational
- Audit trail review process implemented (weekly review by OT Security)
- 90-day online log retention verified
- IDMZ deployment completed and validated

---

#### Phase 4: Long-Term (180+ Days)

Low-severity findings and program maturation. These represent continuous improvement.

| Priority | Finding ID | Title | Recommended Action | Responsible Team | Target Date | Status |
| :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| 1 | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] Open / [ ] In Progress / [ ] Complete |
| 2 | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| 3 | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| 4 | [ID] | [Title] | [Action] | [Team] | [Date] | [ ] |
| 5 | [ID] | Secure Protocol Migration | Upgrade controllers to models supporting OPC UA, CIP Security, S7Comm-Plus during lifecycle refresh | OT Engineering + Procurement | [Date] | [ ] Open / [ ] In Progress / [ ] Complete |

**Phase 4 Success Criteria:**
- All known findings remediated or formally accepted with documented risk
- OT security program operating with defined roles, responsibilities, and metrics
- Annual penetration testing and architecture review scheduled
- Secure protocol migration incorporated into capital planning

---

### Resource Requirements

| Resource | Phase 1 | Phase 2 | Phase 3 | Phase 4 | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **OT Engineering (hours)** | [Estimate] | [Estimate] | [Estimate] | [Estimate] | Requires maintenance window coordination |
| **IT Security (hours)** | [Estimate] | [Estimate] | [Estimate] | [Estimate] | |
| **Network Engineering (hours)** | [Estimate] | [Estimate] | [Estimate] | [Estimate] | |
| **External Consultant (hours)** | [Estimate] | [Estimate] | [Estimate] | [Estimate] | If additional support needed |
| **Hardware / Software Budget** | [Estimate] | [Estimate] | [Estimate] | [Estimate] | Firewalls, IDS, SIEM, etc. |

---

### Risk Acceptance

For findings that cannot be remediated within the recommended timeline (due to technical limitations, cost, or operational constraints), a formal risk acceptance must be documented:

| Finding ID | Reason for Delay | Compensating Controls | Accepted By | Acceptance Date | Review Date |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [ID] | [e.g., Controller replacement requires capital budget FY2027] | [e.g., Strict VLAN isolation, IDS monitoring, manual review of changes] | [Name, Title] | [Date] | [Date -- max 12 months] |

---

### Progress Tracking

| Milestone | Target Date | Actual Date | Status | Notes |
| :--- | :--- | :--- | :---: | :--- |
| Kickoff meeting with stakeholders | [Date] | | [ ] |
| Phase 1 remediation complete | [Date] | | [ ] |
| 30-day progress review | [Date] | | [ ] |
| Phase 2 remediation complete | [Date] | | [ ] |
| 90-day progress review | [Date] | | [ ] |
| Phase 3 remediation complete | [Date] | | [ ] |
| 180-day progress review | [Date] | | [ ] |
| Phase 4 remediation complete | [Date] | | [ ] |
| Post-remediation validation assessment | [Date] | | [ ] |

---

### Approvals

| Role | Name | Signature | Date |
| :--- | :--- | :--- | :--- |
| **OT Engineering Manager** | | | |
| **IT Security Manager** | | | |
| **Plant Manager / Operations Director** | | | |
| **CISO / Executive Sponsor** | | | |

---

*Template version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
