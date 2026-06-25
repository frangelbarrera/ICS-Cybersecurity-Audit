# Phase 1: Documentation and Scope Definition Checklist

## Purpose

This checklist guides the auditor through the initial documentation review and scope definition phase of an ICS/OT security assessment. All items should be completed before any technical testing begins.

**Reference Standards**: ISA/IEC 62443-3-2 (Security Risk Assessment), NIST SP 800-82r3 Section 5 (Risk Management)

---

## 1. Network Documentation

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 1.1 | Obtain current OT network architecture diagrams (all Purdue levels) | [ ] | Client OT Eng. | Must include Level 0-3.5; verify revision date is within 12 months |
| 1.2 | Obtain IT/OT boundary and IDMZ diagrams | [ ] | Client IT/OT | Identify all interconnection points between IT and OT |
| 1.3 | Verify network diagrams include VLAN assignments and subnet ranges | [ ] | Auditor | Cross-reference with live discovery in Phase 2 |
| 1.4 | Obtain managed switch configuration backups (all OT switches) | [ ] | Client OT Eng. | Offline review only; verify port security, VLAN config, STP settings |
| 1.5 | Obtain industrial firewall rule sets (all OT firewalls) | [ ] | Client OT/IT | Tofino, Palo Alto, Fortinet, or equivalent |
| 1.6 | Identify all remote access paths into OT environment | [ ] | Auditor | VPN concentrators, vendor dial-up modems, cellular gateways |
| 1.7 | Document all third-party / vendor connections and maintenance links | [ ] | Client OT Eng. | Includes OEM remote support, cloud-based HMI/SCADA |
| 1.8 | Identify wireless networks in OT environment | [ ] | Client OT Eng. | WirelessHART, ISA100.11a, Wi-Fi for mobile HMIs |

---

## 2. Asset Inventory

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 2.1 | Obtain complete asset inventory for Levels 0-3 | [ ] | Client OT Eng. | Include make, model, firmware, IP/MAC, Purdue level |
| 2.2 | Verify asset inventory includes PLCs, RTUs, DCS controllers, IEDs | [ ] | Auditor | Level 1 devices -- highest criticality |
| 2.3 | Verify asset inventory includes HMI/SCADA servers and engineering workstations | [ ] | Auditor | Level 2-3 devices |
| 2.4 | Verify asset inventory includes network infrastructure devices | [ ] | Auditor | Switches, routers, firewalls, TAPs |
| 2.5 | Identify any assets missing from inventory during Phase 2 discovery | [ ] | Auditor | Flag for remediation -- unknown assets are a finding |
| 2.6 | Document end-of-life (EOL) and end-of-support (EOS) status for all assets | [ ] | Auditor | EOL/EOS devices carry elevated risk; reference vendor lifecycle policies |
| 2.7 | Create asset criticality matrix (SL-Tags per IEC 62443-3-2) | [ ] | Auditor + Client | Safety, financial, operational, environmental impact ratings |

---

## 3. Security Policies and Procedures

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 3.1 | Obtain OT cybersecurity policy document | [ ] | Client Security | Verify it exists and has been reviewed within 12 months |
| 3.2 | Obtain network segmentation policy | [ ] | Client Security | Must address Purdue model zones and conduits |
| 3.3 | Obtain access control policy (physical and logical) | [ ] | Client Security | Include account provisioning, deprovisioning, and periodic review |
| 3.4 | Obtain patch management policy for OT systems | [ ] | Client OT | Must address vendor certification, testing, and deployment windows |
| 3.5 | Obtain backup and recovery policy for OT systems | [ ] | Client OT | Include PLC program backups, HMI project files, historian data |
| 3.6 | Obtain incident response plan (OT-specific) | [ ] | Client Security | Must include OT-specific scenarios and contacts |
| 3.7 | Obtain change management policy for OT systems | [ ] | Client OT | Include approval workflow and maintenance window procedures |
| 3.8 | Obtain vendor / third-party access policy | [ ] | Client Security | Must address remote vendor access to OT systems |

---

## 4. Access Controls

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 4.1 | Obtain user account list for all OT systems (SCADA, HMI, engineering) | [ ] | Client IT/OT | Review for default, shared, and orphaned accounts |
| 4.2 | Verify role-based access control (RBAC) implementation | [ ] | Auditor | Operator vs. engineer vs. administrator privileges |
| 4.3 | Verify multi-factor authentication is enforced for remote access to OT | [ ] | Auditor | VPN, jump servers, vendor portals |
| 4.4 | Review password policy for OT systems | [ ] | Auditor | Complexity, rotation, and whether different from IT policy |

---

## 5. Compliance and Governance

| # | Item | Status | Responsible | Notes |
| :---: | :--- | :---: | :--- | :--- |
| 5.1 | Identify applicable regulatory requirements | [ ] | Client + Auditor | NERC CIP, CFATS, TSA security directives, EU NIS2, etc. |
| 5.2 | Identify applicable industry standards | [ ] | Client + Auditor | IEC 62443, NIST 800-82, ISO 27019, ENISA guidelines |
| 5.3 | Obtain results of previous audits or assessments | [ ] | Client Security | Review for recurring findings and remediation status |
| 5.4 | Verify existence of cybersecurity awareness training program for OT personnel | [ ] | Client HR/Security | Include training records for operators and engineers |

---

## 6. Phase 1 Completion Sign-Off

| Field | Details |
| :--- | :--- |
| **All items reviewed and documented** | [ ] Yes [ ] No -- list exceptions below |
| **Scope document (AUTHORIZATION_SCOPE.md) signed by both parties** | [ ] Yes [ ] No |
| **Authorization letter (AUDIT_AUTHORIZATION_TEMPLATE.md) signed** | [ ] Yes [ ] No |
| **Ready to proceed to Phase 2 (Passive Discovery)** | [ ] Yes [ ] No |
| **Auditor Name / Signature** | |
| **Client Representative Name / Signature** | |
| **Date** | |

**Exceptions and Notes:**

[Document any items that could not be completed, with justification and mitigation for proceeding]

---

*Checklist version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
