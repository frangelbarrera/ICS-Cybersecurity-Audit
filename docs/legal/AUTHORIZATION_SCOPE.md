# Authorization Scope Definition Template

## ICS/OT Security Assessment -- Scope of Work

**DISCLAIMER**: This template is provided for educational and reference purposes. It must be completed, reviewed, and approved by authorized client representatives and qualified legal counsel before use in any professional engagement.

---

### 1. Engagement Overview

| Field | Details |
| :--- | :--- |
| **Engagement ID / Reference** | [e.g., ENG-2026-001] |
| **Client Organization** | [Name] |
| **Audit Firm** | [Name] |
| **Lead Auditor** | [Name, Contact] |
| **Engagement Type** | [Architecture Review / Configuration Audit / Full Assessment / Compliance Audit] |
| **Applicable Standards** | [e.g., IEC 62443-3-3, NIST SP 800-82r3, ISO 27019] |

---

### 2. Purdue Model Scope Definition

| Purdue Level | Designation | In Scope? | Systems Included | Assessment Activities |
| :--- | :--- | :---: | :--- | :--- |
| Level 4 | Enterprise / IT | [ ] Yes [ ] No | [ERP, email, file servers — typically out of scope unless IDMZ review included] | [e.g., IDMZ boundary review only] |
| Level 3.5 | Industrial DMZ | [ ] Yes [ ] No | [Historian replicas, patch servers, AV servers, remote access gateways] | Architecture review, firewall audit, jump server config |
| Level 3 | Site Operations | [ ] Yes [ ] No | [SCADA servers, historians, engineering workstations] | Config audit, access control, patch management review |
| Level 2 | Area Supervision | [ ] Yes [ ] No | [Plant-floor HMIs, local engineering stations] | Config audit, application security, remote access paths |
| Level 1 | Basic Control | [ ] Yes [ ] No | [PLCs, RTUs, DCS controllers, IEDs, safety PLCs] | Offline project file review, firmware inventory, protocol audit |
| Level 0 | Process | [ ] Yes [ ] No | [Sensors, actuators, drives, valves] | Physical security walk-through only. NO active testing. |

---

### 3. Network Segments in Scope

| Network Name / VLAN | CIDR Range | Purdue Level | Authorized Activity | Notes |
| :--- | :--- | :---: | :--- | :--- |
| [e.g., OT-SCADA-CORE] | [e.g., 10.100.30.0/24] | Level 3 | Passive capture, config review | Production — maintenance windows only |
| [e.g., OT-CELL-A] | [e.g., 10.100.10.0/25] | Level 1 | Passive capture, offline review | NO active probing |
| | | | | |
| | | | | |

---

### 4. OT Protocols in Scope

| Protocol | Transport | Default Port(s) | Authorized Activity | SAFETY Constraint |
| :--- | :--- | :--- | :--- | :--- |
| Modbus TCP | TCP | 502 | Passive capture, offline config review, read-only queries | Never send Write Single Coil (FC 05) or Write Multiple (FC 15/16) |
| S7Comm / S7Comm-Plus | TCP | 102 | Passive capture, offline project review | Never upload/download to live PLC |
| EtherNet/IP | TCP/UDP | 44818, 2222 | Passive capture, read-only CIP queries | Never modify CIP objects or I/O connections |
| OPC UA | TCP | 4840 | Certificate audit, endpoint discovery | Never modify server configuration |
| PROFINET | EtherType 0x8892 | N/A (Layer 2) | Passive capture only | Do not interfere with RT/IRT traffic |
| BACnet/IP | UDP | 47808 | Passive capture, device discovery | Avoid broadcast storms; limit Who-Is frequency |
| DNP3 | TCP/UDP | 20000 | Passive capture, read-only queries | Never send control commands |
| IEC 61850 (MMS/GOOSE) | TCP/L2 | 102 (MMS) | Passive capture only | GOOSE/SV messages handle protection — DO NOT INTERFERE |

---

### 5. Explicitly Out of Scope

| System / Network / Device | Reason for Exclusion |
| :--- | :--- |
| Safety Instrumented Systems (SIS) | Safety-critical -- zero tolerance for interference |
| Emergency Shutdown Systems (ESD) | Regulatory and safety requirements |
| Fire and Gas Systems (F&G) | Life-safety systems |
| [Add additional exclusions] | |

---

### 6. Authorized Time Windows

| Activity Type | Authorized Windows | Advance Notice Required |
| :--- | :--- | :--- |
| Passive discovery & traffic capture | [e.g., 24/7 during engagement period] | 48 hours before deployment |
| Configuration review (offline) | [e.g., Business hours, Mon-Fri 08:00-17:00] | 1 week |
| Read-only protocol queries | [e.g., Maintenance windows: Sun 02:00-06:00] | 7 days written approval |
| Physical walk-through | [e.g., Business hours, escorted by plant personnel] | 48 hours |
| Active testing (if authorized) | [e.g., Scheduled plant shutdown / turnaround] | 30 days minimum |

---

### 7. Key Personnel and Escalation

| Role | Name | Phone | Email |
| :--- | :--- | :--- | :--- |
| **Client Project Sponsor** | | | |
| **Client OT/Engineering Lead** | | | |
| **Client IT Security Lead** | | | |
| **Client Plant Manager** | | | |
| **Client Emergency Stop Authority** | | | |
| **Audit Lead** | | | |
| **Audit Technical Lead** | | | |

---

### 8. Exclusion Criteria -- Automatic Stop Conditions

The following conditions, if encountered, require immediate suspension of relevant activities and notification to the client:

- Unexpected reboots, restarts, or faults on any in-scope device
- Process alarms or abnormal operating conditions in any audited zone
- Communication loss to any controller or HMI
- Discovery of previously undocumented interdependencies or shared infrastructure
- Suspicion that assessment activity has triggered a safety or production impact
- Client verbal or written request to stop (unconditional)

---

### 9. Deliverables

| Deliverable | Format | Due Date |
| :--- | :--- | :--- |
| Daily activity log | Written summary (email) | End of each business day |
| Weekly progress report | PDF presentation | Friday 17:00 |
| Draft technical findings | Markdown / DOCX | [Date] |
| Executive summary | PDF | [Date] |
| Remediation roadmap | PDF + spreadsheet | [Date] |
| Raw data return / destruction certificate | Signed document | Within 30 days of completion |

---

### 10. Approvals

This scope definition is valid only when signed by authorized representatives of both parties. Any deviation from the defined scope requires a written change request approved by both parties before execution.

| Client Representative | Auditor Representative |
| :--- | :--- |
| Name: _________________________ | Name: _________________________ |
| Title: _________________________ | Title: _________________________ |
| Signature: _____________________ | Signature: _____________________ |
| Date: _________________________ | Date: _________________________ |

---

*Template version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
