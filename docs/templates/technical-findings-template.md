# Technical Findings Report Template

## ICS/OT Security Assessment -- Technical Findings

---

### Report Metadata

| Field | Details |
| :--- | :--- |
| **Client** | [Organization Name] |
| **Assessment Period** | [Start] to [End] |
| **Report Date** | [YYYY-MM-DD] |
| **Classification** | [Confidential / Client Proprietary] |
| **Lead Auditor** | [Name, Certification] |

---

### How to Use This Template

Each finding follows a standard format designed to provide technical teams with sufficient detail to understand, reproduce (where safe), and remediate each issue. The template includes **five example findings** that represent common OT security observations. Replace these with actual findings from your assessment.

---

### Finding Format

| Field | Description |
| :--- | :--- |
| **Finding ID** | Unique identifier: `ICS-[YEAR]-[###]` |
| **Title** | Brief, descriptive title |
| **Severity** | Critical / High / Medium / Low (see classification criteria below) |
| **Date Identified** | Discovery date |
| **Affected System(s)** | Hostname, IP, Purdue Level, Asset Type |
| **Description** | Detailed technical description of the finding |
| **Evidence** | Commands run, screenshots, configuration excerpts, packet captures (sanitized) |
| **Impact** | What an attacker could achieve; include safety, production, and data impacts |
| **IEC 62443-3-3 Reference** | Applicable System Requirement (SR) |
| **NIST SP 800-82 Reference** | Applicable control section |
| **CVSS-OT Score** | CVSS vector with OT-specific metrics where applicable |
| **Recommendation** | Step-by-step remediation guidance |
| **Estimated Effort** | Hours/days and required skill level |
| **Verified By** | Auditor name |

---

### Severity Classification (OT-Specific)

| Severity | Criteria |
| :--- | :--- |
| **Critical** | Direct safety impact (injury or loss of life potential), unauthenticated remote control of Level 1 device, active exploit in the wild, loss of view/control of safety functions |
| **High** | Authenticated control of Level 1 device, network segmentation bypass, EOL firmware with known remote CVE, default credentials on Level 2-3 systems |
| **Medium** | Information disclosure, insufficient logging, weak encryption, policy violations without immediate exploitation path |
| **Low** | Best practice deviations, hardening opportunities, informational observations |

---

## Findings

---

### Finding ICS-2026-001: Default Credentials on PLC Engineering Interface

| Field | Details |
| :--- | :--- |
| **Severity** | **Critical** |
| **Date Identified** | [YYYY-MM-DD] |
| **Affected System(s)** | PLC-03 (Siemens S7-1200, FW v4.5), IP 10.100.10.30, Purdue Level 1 |
| **Description** | The Siemens S7-1200 controller responsible for [process description] was found using default access-level credentials. The controller's web server and TIA Portal engineering interface both accepted the factory-default password. This allows any device on the OT network with TCP access to port 102 (S7Comm) or port 80/443 (web server) to modify the PLC program, change process setpoints, or stop the controller. |
| **Evidence** | Offline project file review confirmed password hash matched known default. Web interface accepted default credentials when tested from a controlled engineering station within the same VLAN (read-only access was verified before testing). |
| **Impact** | An attacker who gains access to the OT network could upload malicious logic to the controller, causing process disruption, equipment damage, or safety incident. The controller manages [safety-critical function / production-critical process]. |
| **IEC 62443-3-3 Reference** | SR 1.1 -- Identification and Authentication Control; SR 1.2 -- Software Process and Device Identification and Authentication |
| **NIST SP 800-82 Reference** | Section 6.2.1 -- User Authentication and Authorization |
| **CVSS-OT Score** | CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H (9.8) -- note: OT-specific safety impact not captured in base CVSS; see CVSS-OT supplemental |
| **Recommendation** | 1. During the next maintenance window, change the access-level password to a strong, unique credential following organizational password policy. 2. Enable "Full access protection" in TIA Portal project settings. 3. Disable the web server interface if not required for operations. 4. Document the new credential in a secured password vault accessible only to authorized engineering personnel. 5. Update the standard PLC configuration baseline to require non-default credentials for all new deployments. |
| **Estimated Effort** | 2 hours per controller (maintenance window); Low complexity |
| **Verified By** | [Auditor Name] |

---

### Finding ICS-2026-002: Missing Network Segmentation Between IT and OT

| Field | Details |
| :--- | :--- |
| **Severity** | **Critical** |
| **Date Identified** | [YYYY-MM-DD] |
| **Affected System(s)** | OT Core Switch (Cisco IE-4000, 10.100.30.1), Purdue Level 3 to Level 4 boundary |
| **Description** | The boundary between the corporate IT network (Level 4) and the OT supervision network (Level 3) lacks an Industrial DMZ (IDMZ). A Layer 3 routed connection exists with only basic ACLs filtering traffic. No application-layer firewall, data diode, or proxy is in place. IT workstations can initiate connections directly to SCADA servers and engineering workstations. |
| **Evidence** | Route table examination confirmed direct Layer 3 reachability between IT and OT subnets. Review of ACLs showed broad permit rules (e.g., `permit ip any any` between certain IT and OT subnets). Traceroute from IT workstation confirmed direct path to SCADA servers. |
| **Impact** | A compromise of any corporate IT asset (workstation, server, or user account) could provide an attacker with direct network access to SCADA servers, historians, and engineering workstations. This enables ransomware propagation, data exfiltration, or manipulation of industrial processes from the IT network. |
| **IEC 62443-3-3 Reference** | SR 5.1 -- Network Segmentation; SR 5.2 -- Zone Boundary Protection |
| **NIST SP 800-82 Reference** | Section 6.2.6 -- Network Segmentation and Segregation |
| **CVSS-OT Score** | CVSS:3.1/AV:A/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H (9.3) |
| **Recommendation** | 1. Design and implement an Industrial DMZ (IDMZ) per IEC 62443-3-3 guidance between IT and OT networks. 2. Deploy application-layer firewalls at the IDMZ boundary with default-deny rules. 3. Implement a jump server / terminal server solution for all IT-to-OT remote access with MFA and session recording. 4. Consider data diodes for historian replication to IT (unidirectional). 5. Remove all direct IT-to-OT routing; all traffic must traverse IDMZ security controls. |
| **Estimated Effort** | Design: 40 hours; Implementation: 80-120 hours during scheduled outages; High complexity, requires IT and OT coordination |
| **Verified By** | [Auditor Name] |

---

### Finding ICS-2026-003: Unencrypted OT Protocols on Control Network

| Field | Details |
| :--- | :--- |
| **Severity** | **High** |
| **Date Identified** | [YYYY-MM-DD] |
| **Affected System(s)** | Control network VLAN 110 (10.100.10.0/24), Purdue Level 1-2 |
| **Description** | Multiple OT protocols traversing the control network transmit data in cleartext with no integrity protection. Protocols observed include: Modbus TCP (port 502), S7Comm (port 102), and EtherNet/IP (ports 44818, 2222). An attacker with passive access to the control network could capture process data, PLC logic uploads/downloads, and engineering communications. An attacker with active Man-in-the-Middle capability could inject spoofed commands. |
| **Evidence** | Packet captures (PCAP files available upon request, restricted distribution) confirm cleartext Modbus Read/Write operations, S7Comm job requests containing PLC program blocks, and unauthenticated CIP messages. Wireshark dissectors confirm absence of TLS or any encryption layer. |
| **Impact** | Passive eavesdropping reveals process parameters, operational setpoints, and potentially PLC program logic. Active manipulation could alter process variables, disrupt operations, or cause equipment damage. The lack of integrity protection means commands cannot be verified as authentic. |
| **IEC 62443-3-3 Reference** | SR 3.1 -- Communication Integrity; SR 4.1 -- Information Confidentiality |
| **NIST SP 800-82 Reference** | Section 6.2.4 -- Communication Security |
| **CVSS-OT Score** | CVSS:3.1/AV:A/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N (8.1) |
| **Recommendation** | 1. Where protocol-level encryption is available (e.g., OPC UA with SecurityPolicy, CIP Security for EtherNet/IP, S7Comm-Plus with TLS on S7-1500), enable it during the next upgrade cycle. 2. For protocols without native encryption (Modbus TCP), implement compensating controls: network segmentation, encrypted VPN tunnels between zones, and strict physical/logical access controls to the control network. 3. Deploy network monitoring with protocol-aware IDS (e.g., Zeek with ICS protocol analyzers) to detect anomalous commands. 4. Prioritize migration to controllers that support secure protocols during lifecycle refresh. |
| **Estimated Effort** | Variable; Controller upgrades require capital planning (12-24 months). Near-term: deploy IDS monitoring (40 hours), implement tighter access controls (20 hours). |
| **Verified By** | [Auditor Name] |

---

### Finding ICS-2026-004: EOL Firmware on Critical PLC with Known Vulnerabilities

| Field | Details |
| :--- | :--- |
| **Severity** | **High** |
| **Date Identified** | [YYYY-MM-DD] |
| **Affected System(s)** | PLC-07 (Allen-Bradley ControlLogix 1756-L71, FW v28.011), Purdue Level 1 |
| **Description** | The ControlLogix controller is running firmware version 28.011, which reached end-of-support in [year]. The vendor has published multiple security advisories for vulnerabilities affecting this firmware version, including CVE-20XX-XXXX (remote denial of service via malformed CIP packets) and CVE-20XX-XXXX (authentication bypass on web interface). The controller manages [critical process description]. |
| **Evidence** | Firmware version confirmed via RSLinx Classic browsing (read-only). CVE matches verified against Rockwell Automation Security Advisory index. No maintenance contract or upgrade plan was identified during document review. |
| **Impact** | A denial-of-service attack against this controller would disrupt [critical process], with estimated production losses of [amount] per hour. The authentication bypass vulnerability could allow unauthorized logic changes. |
| **IEC 62443-3-3 Reference** | SR 3.2 -- Malicious Code Protection; SR 3.3 -- Security Functionality Verification |
| **NIST SP 800-82 Reference** | Section 6.2.3 -- Patch Management; Section 6.2.4 -- System Hardening |
| **CVSS-OT Score** | CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H (7.5) for DoS; OT safety supplement increases effective severity |
| **Recommendation** | 1. Establish an active support contract with Rockwell Automation to access firmware updates and security patches. 2. Schedule firmware upgrade to latest supported version (currently vXX.XXX) during the next planned maintenance window (coordinate with Rockwell for compatibility validation). 3. Implement compensating controls in the interim: isolate the controller on a dedicated VLAN, restrict access to authorized engineering stations only, and deploy network monitoring for malicious CIP traffic. 4. Create a firmware lifecycle management process to prevent future EOL situations. |
| **Estimated Effort** | Firmware upgrade: 4 hours per controller (maintenance window); Low-medium complexity. Support contract: 2-4 weeks procurement lead time. |
| **Verified By** | [Auditor Name] |

---

### Finding ICS-2026-005: Insufficient Audit Logging on SCADA Servers

| Field | Details |
| :--- | :--- |
| **Severity** | **Medium** |
| **Date Identified** | [YYYY-MM-DD] |
| **Affected System(s)** | SCADA-01, SCADA-02 (Windows Server 2019, Wonderware System Platform), Purdue Level 3 |
| **Description** | The SCADA servers have basic Windows event logging enabled, but OT-application-level audit logging is not configured. The following events are not captured: operator setpoint changes, alarm acknowledgments, engineering mode activations, and user login/logout timestamps. Additionally, Windows event logs are stored locally only with no forwarding to a centralized SIEM or log collector. Log retention is set to the Windows default (overwrite oldest events when maximum log size is reached). |
| **Evidence** | Review of SCADA application configuration confirms audit trail features are disabled. Windows Event Viewer shows only default system/security logs. Log retention policy review confirms no centralized collection or retention beyond local defaults. |
| **Impact** | Without adequate audit logging, the organization cannot: (a) detect unauthorized changes to process parameters, (b) investigate security incidents with forensic evidence, (c) demonstrate regulatory compliance, or (d) establish a baseline of normal operator behavior for anomaly detection. |
| **IEC 62443-3-3 Reference** | SR 2.8 -- Auditable Events; SR 2.9 -- Audit Storage Capacity |
| **NIST SP 800-82 Reference** | Section 6.3.3 -- Audit and Accountability |
| **CVSS-OT Score** | Not applicable; this is a control gap rather than an exploitable vulnerability |
| **Recommendation** | 1. Enable audit trail functionality in the SCADA application for all operator actions, alarm management, and configuration changes. 2. Configure Windows Advanced Audit Policy to capture process creation, account management, and privileged operations. 3. Deploy a centralized log collector or SIEM in the OT environment (ensure it is properly segmented and hardened). 4. Define log retention policy: minimum 90 days online, 12 months archived (or per regulatory requirement). 5. Integrate OT logs with security monitoring for anomaly detection and incident response. |
| **Estimated Effort** | SCADA audit configuration: 8 hours. SIEM deployment: 40-80 hours. Ongoing tuning: 20 hours/month initially. |
| **Verified By** | [Auditor Name] |

---

### Finding Summary Table

| ID | Title | Severity | Affected Level | Effort |
| :--- | :--- | :--- | :---: | :--- |
| ICS-2026-001 | Default Credentials on PLC Engineering Interface | Critical | Level 1 | Low (2h) |
| ICS-2026-002 | Missing Network Segmentation Between IT and OT | Critical | Level 3-4 | High (120-160h) |
| ICS-2026-003 | Unencrypted OT Protocols on Control Network | High | Level 1-2 | Variable |
| ICS-2026-004 | EOL Firmware on Critical PLC | High | Level 1 | Low-Med (4h + procurement) |
| ICS-2026-005 | Insufficient Audit Logging on SCADA Servers | Medium | Level 3 | Medium (48-100h) |
| [Add additional findings] | | | | |

---

*Template version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
