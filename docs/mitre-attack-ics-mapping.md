# MITRE ATT&CK for ICS Mapping

## Comprehensive Technique-to-Audit-Phase Mapping

### Overview

MITRE ATT&CK for ICS is a knowledge base of adversary tactics, techniques, and procedures (TTPs) targeting industrial control systems. Unlike the enterprise ATT&CK matrix, the ICS matrix focuses on the unique operational realities of OT environments: safety-critical processes, real-time constraints, proprietary protocols, and the Purdue Model architecture.

This document maps every technique in the MITRE ATT&CK for ICS matrix to the 5-phase audit methodology defined in the [ICS-Cybersecurity-Audit Framework](../../README.md). Each mapping identifies:

- **Which audit phase** provides the best detection opportunity
- **Which IEC 62443-3-3 Security Requirement (SR)** would prevent, detect, or mitigate the technique
- **Which NIST SP 800-82r3 control** is relevant
- **Severity if undetected** in the OT context

**How to Use This Mapping:**

1. During an audit, use the technique tables to identify which TTPs your existing controls address and which represent detection gaps.
2. Cross-reference findings against the corresponding IEC 62443 SR to provide standards-based justification for remediation.
3. Use the attack scenario walkthroughs to train operations and security teams on realistic ICS attack paths.
4. Complete the Detection Gap Analysis template to prioritize security investments.

**Reference**: MITRE ATT&CK for ICS v16 -- [https://attack.mitre.org/matrices/ics/](https://attack.mitre.org/matrices/ics/)

---

### The 12 ATT&CK for ICS Tactics

| Tactic ID | Tactic Name | Description | Primary Audit Phase | Key IEC 62443 SR |
| :--- | :--- | :--- | :---: | :--- |
| TA0108 | Initial Access | Techniques used to gain initial entry into the ICS environment | Phase 2, 3, 4 | SR 1.1, SR 2.1, SR 5.1 |
| TA0104 | Execution | Techniques that result in adversary-controlled code running on an ICS device | Phase 3, 4 | SR 2.8, SR 3.2 |
| TA0110 | Persistence | Techniques used to maintain access across restarts, credential changes, or network disconnections | Phase 3, 4 | SR 1.1, SR 3.2 |
| TA0111 | Privilege Escalation | Techniques to obtain higher-level permissions | Phase 3 | SR 2.1, SR 2.11 |
| TA0103 | Evasion | Techniques to avoid detection during an attack | Phase 2, 4, 5 | SR 2.8, SR 3.1 |
| TA0102 | Discovery | Techniques to gain knowledge about the ICS environment | Phase 2, 4 | SR 2.8, SR 5.1 |
| TA0109 | Lateral Movement | Techniques to move between systems within the ICS environment | Phase 3, 4 | SR 5.1, SR 5.2 |
| TA0100 | Collection | Techniques to gather ICS process data, configurations, and operational information | Phase 2, 4 | SR 3.1, SR 4.1 |
| TA0101 | Command and Control | Techniques to communicate with compromised systems | Phase 2, 4 | SR 3.1, SR 5.1 |
| TA0107 | Inhibit Response Function | Techniques to prevent safety, protective, or operator response functions | Phase 3, 4 | SR 4.1, SR 4.2 |
| TA0106 | Impair Process Control | Techniques to manipulate, disable, or damage physical processes | Phase 3, 4 | SR 3.1, SR 4.2 |
| TA0105 | Impact | Techniques to disrupt, destroy, or manipulate the operational process and its data | Phase 4, 5 | SR 4.1, SR 4.2 |

---

## Technique-by-Technique Mapping

### Initial Access (TA0108)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0817 | Drive-by Compromise | Monitor engineering workstation web browsing; application whitelisting; restrict internet access from OT | Phase 3 | SR 3.2, SR 7.1 | 6.2.4, 6.3.1 | **High** |
| T0819 | Exploit Public-Facing Application | Vulnerability scanning of OT-facing web servers; patch management audit; IDS signatures for known CVEs | Phase 3, 4 | SR 3.1, SR 3.2 | 6.2.4, 6.3.1 | **Critical** |
| T0866 | Exploitation of Remote Services | Audit remote access paths; verify MFA enforcement; review remote service logs | Phase 3, 4 | SR 1.12, SR 2.1 | 6.2.1, 6.2.6 | **Critical** |
| T0822 | External Remote Services | Inventory all remote access methods (VPN, dial-up, cellular, vendor portals); verify jump server configuration | Phase 3 | SR 5.1, SR 1.12 | 6.2.6, 6.3.1 | **Critical** |
| T0883 | Internet Accessible Device | Passive discovery of OT devices with internet-reachable interfaces; Shodan/Censys search for client IP ranges | Phase 2 | SR 5.1, SR 7.1 | 6.2.6 | **Critical** |
| T0886 | Remote Services | Review RDP, SSH, VNC, TeamViewer configurations on OT hosts; verify access control and MFA | Phase 3 | SR 1.1, SR 2.1 | 6.2.1, 6.3.1 | **Critical** |
| T0847 | Replication Through Removable Media | USB port control audit; removable media policy verification; endpoint protection on engineering workstations | Phase 3, 5 | SR 2.4, SR 3.2 | 6.3.20, 6.5.2 | **High** |
| T0848 | Rogue Master | Protocol-level monitoring for unauthorized Modbus/DNP3 master devices; network baseline deviation alerts | Phase 2, 4 | SR 3.1, SR 5.1 | 6.2.5, 6.2.6 | **Critical** |
| T0865 | Spearphishing Attachment | Email security gateway audit; phishing simulation results for OT personnel; security awareness training records | Phase 3, 5 | SR 1.1, SR 2.1 | 6.3.1 | **High** |
| T0862 | Supply Chain Compromise | Vendor security assessment; firmware integrity verification; secure procurement policy review | Phase 3 | SR 1.2, SR 3.2 | 6.2.3, 6.2.4 | **Critical** |
| T0864 | Transient Cyber Asset | Policy for contractor/vendor laptops connecting to OT; network access control (NAC) on OT network | Phase 3 | SR 2.4, SR 5.1 | 6.2.1, 6.5.2 | **Medium** |
| T0860 | Wireless Compromise | Wireless survey of OT areas; verify WPA3-Enterprise on OT WiFi; detect rogue APs | Phase 4 | SR 4.2, SR 5.1 | 6.2.6, 6.5.2 | **High** |

---

### Execution (TA0104)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0895 | Autorun Image | Verify autorun disabled on all OT hosts; check startup folder and registry run keys on engineering workstations | Phase 3 | SR 2.4, SR 3.2 | 6.3.1, 6.3.20 | **Medium** |
| T0858 | Change Operating Mode | Monitor PLC mode changes (RUN to STOP/PROGRAM); alert on unexpected mode transitions; key switch position audit | Phase 2, 4 | SR 2.1, SR 2.8 | 6.2.1, 6.3.3 | **Critical** |
| T0807 | Command-Line Interface | Enable PowerShell logging; audit command history on engineering workstations; application whitelisting | Phase 3, 5 | SR 2.8, SR 3.2 | 6.3.1, 6.3.3 | **High** |
| T0871 | Execution through API | Monitor SCADA/HMI API access patterns; review API authentication and authorization; audit SCADA scripting | Phase 3, 4 | SR 2.1, SR 2.8 | 6.3.1, 6.3.3 | **High** |
| T0823 | Graphical User Interface | Verify HMI operator actions are logged with user attribution; detect anomalous HMI interaction patterns | Phase 3 | SR 2.8, SR 2.1 | 6.3.1, 6.3.3 | **High** |
| T0874 | Hooking | Verify code integrity on engineering workstations; application whitelisting; anti-malware with exploit protection | Phase 3 | SR 3.2 | 6.3.1, 6.3.20 | **High** |
| T0821 | Modify Controller Tasking | Monitor PLC logic execution changes; compare running logic against approved baseline; watch for unexpected program downloads | Phase 4 | SR 3.1, SR 3.2 | 6.2.4, 6.3.3 | **Critical** |
| T0834 | Native API | Monitor for unusual API calls to OT system libraries; application control policies; restrict engineering software to authorized workstations | Phase 3, 4 | SR 2.1, SR 2.8 | 6.3.1 | **Medium** |
| T0853 | Scripting | Restrict scripting engine access on OT hosts; audit scheduled tasks; monitor for unusual script execution | Phase 3 | SR 2.4, SR 2.8 | 6.3.1, 6.3.3 | **Medium** |
| T0863 | User Execution | Security awareness training for OT personnel; phishing simulation; email attachment filtering for OT users | Phase 3, 5 | SR 1.1 | 6.3.1 | **High** |

---

### Persistence (TA0110)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T1694 | Insecure Credentials | Default credential audit (Phase 3 checklist); password policy review; SSH key and certificate management audit | Phase 3 | SR 1.1, SR 1.2 | 6.2.1 | **Critical** |
| T1693 | Modify Firmware | Firmware integrity verification; compare running firmware hash against known-good baseline; secure boot verification | Phase 3, 4 | SR 1.2, SR 3.2 | 6.2.3, 6.2.4 | **Critical** |
| T0889 | Modify Program | PLC program comparison against offline backup; program change logging; electronic keying and access protection | Phase 3, 4 | SR 3.1, SR 3.2 | 6.2.4 | **Critical** |
| T0873 | Project File Infection | Scan engineering project files for unauthorized modifications; verify project file checksums; secure file storage | Phase 3 | SR 3.2, SR 4.1 | 6.2.4, 6.3.1 | **High** |
| T0859 | Valid Accounts | User account audit (dormant accounts, shared accounts, excessive privileges); access review process verification | Phase 3, 5 | SR 1.1, SR 2.1 | 6.2.1 | **Critical** |

---

### Privilege Escalation (TA0111)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0890 | Exploitation for Privilege Escalation | Patch management audit; vulnerability assessment on engineering workstations and SCADA servers | Phase 3, 4 | SR 3.2, SR 2.11 | 6.2.3, 6.3.1 | **High** |
| T0874 | Hooking | Application whitelisting; anti-malware with privilege escalation detection; code integrity verification | Phase 3 | SR 3.2 | 6.3.1 | **High** |

---

### Evasion (TA0103)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0858 | Change Operating Mode | See Execution -- cross-tactic technique. Monitor PLC mode transitions | Phase 2, 4 | SR 2.1, SR 2.8 | 6.2.1, 6.3.3 | **Critical** |
| T0820 | Exploitation for Evasion | Patch management for security software; verify AV/EDR is running and updated on OT assets; log review completeness | Phase 3 | SR 3.2 | 6.2.3, 6.3.3 | **High** |
| T0872 | Indicator Removal on Host | Audit logging configuration (ensure logs cannot be cleared by operators); forward logs to central SIEM before local deletion | Phase 3, 5 | SR 2.8, SR 2.9 | 6.3.3 | **High** |
| T0849 | Masquerading | Network traffic anomaly detection; protocol compliance checking (verify Modbus traffic conforms to spec); DPI for protocol anomalies | Phase 2, 4 | SR 3.1, SR 5.1 | 6.2.5 | **High** |
| T0851 | Rootkit | Firmware integrity verification; secure boot; hardware root of trust; periodic integrity scans of engineering workstations | Phase 3, 4 | SR 1.2, SR 3.2 | 6.2.4 | **Critical** |
| T0894 | System Binary Proxy Execution | Application whitelisting; monitor for LOLBins (Living off the Land Binaries) on OT Windows hosts; restrict execution paths | Phase 3 | SR 2.4, SR 3.2 | 6.3.1, 6.3.20 | **Medium** |
| T1692 | Unauthorized Message | Protocol-aware IDS for unauthorized Modbus/DNP3 commands; baseline traffic comparison; alert on unknown function codes | Phase 2, 4 | SR 3.1 | 6.2.5 | **High** |

---

### Discovery (TA0102)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0840 | Network Connection Enumeration | Monitor for port scanning and connection attempts on OT network; baseline deviation alerts for unusual connection patterns | Phase 2, 4 | SR 2.8, SR 5.1 | 6.2.5, 6.2.6 | **High** |
| T0842 | Network Sniffing | Physical access control to network infrastructure; encrypted protocols between zones; detect promiscuous-mode NICs | Phase 2, 4 | SR 3.1, SR 4.2 | 6.2.4, 6.5.1 | **High** |
| T0846 | Remote System Discovery | Monitor for unusual enumeration traffic; restrict network discovery tools on OT hosts; segment OT network from IT discovery protocols | Phase 2, 4 | SR 5.1, SR 2.8 | 6.2.6 | **Medium** |
| T0888 | Remote System Information Discovery | System information queries via SNMP, WMI, or proprietary protocols; restrict information disclosure on OT devices | Phase 3, 4 | SR 2.8, SR 7.1 | 6.2.1, 6.2.5 | **Medium** |
| T0887 | Wireless Sniffing | Physical security controls for wireless coverage areas; detect unauthorized wireless devices in OT zones | Phase 4 | SR 4.2 | 6.5.1, 6.5.2 | **Medium** |

---

### Lateral Movement (TA0109)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0866 | Exploitation of Remote Services | See Initial Access. Vulnerability management on OT applications and services | Phase 3, 4 | SR 3.2 | 6.2.3, 6.2.4 | **Critical** |
| T1694 | Insecure Credentials | See Persistence. Default credential audit; shared credential detection | Phase 3 | SR 1.1 | 6.2.1 | **Critical** |
| T0867 | Lateral Tool Transfer | Restrict file transfers between OT zones; USB port control; network segmentation enforcement | Phase 3, 4 | SR 2.4, SR 5.1 | 6.2.6, 6.5.2 | **High** |
| T0843 | Program Download | Monitor PLC program download events; restrict program download to authorized engineering workstations only; require authentication | Phase 4 | SR 1.2, SR 2.1 | 6.2.4 | **Critical** |
| T0886 | Remote Services | See Initial Access. Audit all remote service configurations; verify jump server architecture | Phase 3 | SR 1.12, SR 5.1 | 6.2.6 | **Critical** |
| T0859 | Valid Accounts | See Persistence. Account usage auditing; detect anomalous account activity across OT zones | Phase 3, 5 | SR 1.1, SR 2.1 | 6.2.1 | **Critical** |

---

### Collection (TA0100)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0830 | Adversary-in-the-Middle | Protocol encryption audit; ARP spoofing detection; switch port security review; certificate validation | Phase 3, 4 | SR 3.1 | 6.2.4, 6.2.6 | **Critical** |
| T0802 | Automated Collection | Data exfiltration monitoring; unusual data volume patterns; restrict data aggregation capabilities to authorized hosts | Phase 2, 4 | SR 4.1, SR 2.8 | 6.2.5, 6.3.3 | **High** |
| T0811 | Data from Information Repositories | Access control on document repositories (network diagrams, passwords, procedures); audit file access on shared drives | Phase 3 | SR 2.1, SR 4.1 | 6.2.1, 6.3.1 | **High** |
| T0893 | Data from Local System | File integrity monitoring on engineering workstations; detect bulk file access; restrict local data storage of sensitive OT documents | Phase 3, 5 | SR 2.8, SR 4.1 | 6.3.1, 6.3.3 | **Medium** |
| T0868 | Detect Operating Mode | Monitor for unusual queries about system state; consider whether operational state information is excessively exposed | Phase 2, 4 | SR 2.8, SR 7.1 | 6.2.5 | **Medium** |
| T0877 | I/O Image | Monitor for unauthorized access to I/O data tables; restrict read access to I/O memory on controllers; network segmentation | Phase 3, 4 | SR 2.1, SR 5.1 | 6.2.1, 6.2.6 | **High** |
| T0801 | Monitor Process State | Baseline process variable access patterns; alert on anomalous tag reads; restrict HMI view access based on role | Phase 2, 4 | SR 2.1, SR 2.8 | 6.2.1, 6.3.3 | **High** |
| T0861 | Point & Tag Identification | Restrict engineering database access; audit SCADA tag enumeration queries; protect tag databases with access controls | Phase 3 | SR 2.1, SR 4.1 | 6.2.1 | **Medium** |
| T0845 | Program Upload | Restrict PLC program upload to authorized engineering workstations; log all upload events; require authentication for upload | Phase 3, 4 | SR 1.2, SR 2.1 | 6.2.4 | **High** |
| T0852 | Screen Capture | Application control on HMI/SCADA hosts; restrict screen capture and remote desktop recording capabilities on operator stations | Phase 3 | SR 2.4 | 6.3.1 | **Low** |

---

### Command and Control (TA0101)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0885 | Commonly Used Port | Firewall rule audit; detect OT protocol traffic on non-standard ports; protocol compliance checking | Phase 3, 4 | SR 5.1, SR 3.1 | 6.2.6 | **High** |
| T0884 | Connection Proxy | Egress filtering on OT network; detect anomalous outbound connections; restrict internet access from OT zones | Phase 3, 4 | SR 5.1, SR 5.2 | 6.2.6 | **High** |
| T0869 | Standard Application Layer Protocol | Protocol whitelisting on OT firewalls; deep packet inspection for protocol compliance; restrict allowed application protocols on OT network | Phase 3, 4 | SR 5.1, SR 3.1 | 6.2.6 | **High** |

---

### Inhibit Response Function (TA0107)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0800 | Activate Firmware Update Mode | Monitor PLC mode transitions; restrict firmware update capability to authorized engineering workstations during maintenance windows | Phase 3, 4 | SR 3.2, SR 2.1 | 6.2.4 | **Critical** |
| T0878 | Alarm Suppression | Verify alarm configuration integrity; monitor for suppressed or disabled alarms; alarm flood protection review | Phase 3, 4 | SR 2.8, SR 4.1 | 6.3.3 | **Critical** |
| T1695 | Block Communications | Network monitoring for communication loss; redundant communication path verification; detect deliberate communication disruption | Phase 2, 4 | SR 3.1, SR 4.1 | 6.2.5, 6.2.6 | **Critical** |
| T1691 | Block Operational Technology Message | Protocol-aware monitoring for missing expected messages; heartbeat monitoring between controllers and SCADA; watchdog verification | Phase 2, 4 | SR 3.1 | 6.2.5 | **Critical** |
| T0892 | Change Credential | Monitor for unauthorized password changes on OT accounts; privileged account activity alerting; credential vault audit | Phase 3, 5 | SR 1.1, SR 2.1 | 6.2.1 | **Critical** |
| T0809 | Data Destruction | Backup integrity verification; restore procedure testing; offline backup storage audit; detect mass file deletion on OT hosts | Phase 3, 4 | SR 4.1, SR 3.2 | 6.2.4, 6.3.1 | **Critical** |
| T0814 | Denial of Service | Network resilience testing; verify redundant paths and failover; traffic rate limiting on OT devices; DDoS protection | Phase 4 | SR 4.1, SR 3.1 | 6.2.5, 6.2.6 | **Critical** |
| T0816 | Device Restart/Shutdown | Monitor for unexpected device reboots or shutdowns; UPS health monitoring; physical security for power controls | Phase 2, 4 | SR 4.1, SR 4.2 | 6.5.1 | **Critical** |
| T0835 | Manipulate I/O Image | Compare I/O image against expected values; I/O forcing detection; monitor for unexpected changes to I/O mapping | Phase 4 | SR 3.1, SR 4.1 | 6.2.4 | **Critical** |
| T0838 | Modify Alarm Settings | Alarm configuration baseline comparison; change management for alarm parameters; restrict alarm configuration to authorized personnel | Phase 3, 4 | SR 2.1, SR 2.8 | 6.2.1, 6.3.3 | **Critical** |
| T1693 | Modify Firmware | See Persistence. Firmware integrity verification; detect unauthorized firmware modifications | Phase 3, 4 | SR 1.2, SR 3.2 | 6.2.3, 6.2.4 | **Critical** |
| T0851 | Rootkit | See Evasion. Hardware-based integrity verification; periodic firmware comparison against known-good | Phase 3, 4 | SR 1.2, SR 3.2 | 6.2.4 | **Critical** |
| T0881 | Service Stop | Monitor OT service status; verify automatic service recovery is configured; alert on unexpected service termination | Phase 3, 4 | SR 4.1, SR 2.8 | 6.3.1, 6.3.3 | **Critical** |

---

### Impair Process Control (TA0106)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0806 | Brute Force I/O | I/O value integrity monitoring; detect rapid or unexpected I/O changes; rate limiting on I/O writes; safety interlock verification | Phase 4 | SR 4.1, SR 4.2 | 6.2.4 | **Critical** |
| T1693 | Modify Firmware | See Persistence and Inhibit Response Function. Cross-tactic technique spanning persistence and process impairment | Phase 3, 4 | SR 1.2, SR 3.2 | 6.2.3, 6.2.4 | **Critical** |
| T0836 | Modify Parameter | Parameter change logging; compare operational parameters against approved setpoints; restrict parameter modification to authorized roles | Phase 3, 4 | SR 2.1, SR 2.8 | 6.2.1, 6.3.3 | **Critical** |
| T0833 | Modify Program | See Persistence. PLC program change detection; logic comparison tools; program change approval workflow verification | Phase 3, 4 | SR 3.2 | 6.2.4 | **Critical** |

---

### Impact (TA0105)

| Technique ID | Technique Name | Detection Opportunity | Audit Phase | IEC 62443 SR | NIST 800-82 Control | Severity if Undetected |
| :--- | :--- | :--- | :---: | :--- | :--- | :---: |
| T0815 | Denial of View | Redundant HMI/SCADA deployment verification; failover testing; detect when operator view is blocked or manipulated | Phase 4 | SR 4.1 | 6.3.1, 6.5.1 | **Critical** |
| T0813 | Denial of Control | Redundant control paths; manual override capability verification; safety interlock independence from digital controls | Phase 3, 4 | SR 4.1, SR 4.2 | 6.2.4, 6.5.1 | **Critical** |
| T0827 | Loss of Control | Control loop integrity monitoring; detect when process control is lost or manipulated; verify manual/backup control procedures | Phase 4 | SR 4.1, SR 4.2 | 6.2.4 | **Critical** |
| T0826 | Loss of Productivity and Revenue | Business continuity plan for OT; production impact analysis; verify recovery time objectives (RTO) for critical processes | Phase 3, 5 | SR 4.1 | 6.5.1 | **High** |
| T0828 | Loss of Safety | Safety instrumented system (SIS) independence verification; SIS bypass audit; verify safety functions cannot be disabled remotely | Phase 3, 4 | SR 4.1, SR 4.2 | 6.5.1 | **Critical** |
| T0837 | Loss of View | Redundant HMI deployment; verify operator can monitor process from backup station; test failover to backup SCADA | Phase 4 | SR 4.1 | 6.3.1 | **Critical** |
| T0848 | Rogue Master Device | See Initial Access. Protocol authentication enforcement; device whitelisting; detect unauthorized masters on OT network | Phase 2, 4 | SR 1.2, SR 3.1 | 6.2.5 | **Critical** |
| T0856 | Manipulation of Control | Control command verification; detect commands from unauthorized sources; sequence-of-events recording for post-incident analysis | Phase 4 | SR 3.1, SR 2.8 | 6.2.4, 6.3.3 | **Critical** |
| T0857 | Spoof Reporting Message | Data integrity verification between field devices and SCADA; detect discrepancies between redundant measurements; cross-validation | Phase 4 | SR 3.1, SR 2.8 | 6.2.4 | **Critical** |
| T0829 | Loss of Protection | Protection relay setting audit; verify protection settings cannot be changed remotely without authorization; SIS testing records | Phase 3, 4 | SR 4.2 | 6.5.1 | **Critical** |
| T0818 | Damage to Property | Physical security controls; environmental monitoring; equipment protection systems verification | Phase 3 | SR 4.2 | 6.5.1 | **Critical** |
| T0880 | Manipulation of View | HMI display integrity verification; detect discrepancies between HMI display and actual process values; redundant measurement cross-check | Phase 4 | SR 3.1, SR 2.8 | 6.3.1 | **Critical** |

---

## Attack Scenario Walkthroughs

### Scenario 1: Compromising an HMI via Exposed Web Interface

**ATT&CK Chain**: T0819 (Exploit Public-Facing Application) -> T0859 (Valid Accounts) -> T0886 (Remote Services) -> T0831 (Manipulate I/O Image) -> T0836 (Modify Parameter)

**Walkthrough:**

1. **T0819 -- Exploit Public-Facing Application**: The attacker discovers an HMI web interface exposed to the internet (or accessible from the IT network without proper segmentation). The HMI runs an outdated web server with a known CVE. The attacker exploits this vulnerability to gain initial code execution on the HMI host.

2. **T0859 -- Valid Accounts**: Once on the HMI host, the attacker discovers that the SCADA application uses shared operator credentials stored in a plaintext configuration file. The attacker extracts these credentials for persistent access.

3. **T0886 -- Remote Services**: Using the compromised credentials, the attacker establishes RDP access to the SCADA server from the HMI host. The jump between HMI and SCADA goes undetected because it appears as legitimate operator activity.

4. **T0831 -- Manipulate I/O Image**: From the SCADA server, the attacker accesses tag databases and discovers the Modbus register mappings for critical process variables. The attacker manipulates I/O image values sent to the PLC, causing the PLC to act on falsified process data.

5. **T0836 -- Modify Parameter**: The attacker modifies setpoint parameters for a critical process (e.g., pressure setpoint for a chemical reactor), pushing the process outside its safe operating envelope.

**Detection by Audit Phase:**

- **Phase 2 (Passive Discovery)**: Internet-facing OT assets would be detected during passive network mapping. Traffic from the IT network to HMI web interfaces would be flagged.
- **Phase 3 (Hardening Review)**: Default/shared credentials audit would identify the plaintext credential file. Missing MFA on SCADA would be flagged. Patch management review would identify the outdated HMI web server.
- **Phase 4 (Controlled Validation)**: Segmentation testing would detect the IT-to-HMI path. Default credential testing would confirm the vulnerability. Parameter modification testing would verify write access controls.
- **Phase 5 (Reporting)**: Findings would map to IEC 62443 SR 1.1 (identification), SR 5.1 (segmentation), SR 2.1 (authorization).

**IEC 62443 Failures:**
- SR 5.1 -- Network Segmentation: HMI accessible from IT/internet
- SR 1.1 -- Identification and Authentication: Shared credentials, no MFA
- SR 2.1 -- Authorization: Operator credentials could modify engineering parameters
- SR 2.8 -- Auditable Events: No logging of parameter changes with user attribution

---

### Scenario 2: Lateral Movement from IT to OT Through Compromised Jump Server

**ATT&CK Chain**: T0840 (Network Connection Enumeration) -> T0859 (Valid Accounts) -> T0886 (Remote Services) -> T0888 (Remote System Information Discovery) -> T0821 (Modify Controller Tasking)

**Walkthrough:**

1. **T0840 -- Network Connection Enumeration**: An attacker has compromised a user workstation on the corporate IT network. They perform network discovery and identify a jump server in the Industrial DMZ that bridges IT and OT networks.

2. **T0859 -- Valid Accounts**: The attacker discovers that the jump server uses domain credentials synced between IT and OT Active Directory forests, with no additional authentication step. They harvest valid credentials from the compromised IT workstation.

3. **T0886 -- Remote Services**: Using the valid domain credentials, the attacker establishes an RDP session to the jump server. Because the jump server lacks session recording and MFA, the access goes undetected.

4. **T0888 -- Remote System Information Discovery**: From the jump server, the attacker queries the OT network and discovers engineering workstations, SCADA servers, and PLC IP addresses. They use SNMP queries to gather device information.

5. **T0821 -- Modify Controller Tasking**: The attacker connects to a PLC from the engineering workstation using the native engineering software (which trusts connections from the jump server). They modify the controller tasking to change process logic.

**Detection by Audit Phase:**

- **Phase 2 (Passive Discovery)**: IT-to-OT traffic patterns would be mapped. Unusual RDP sessions from IT to DMZ would be detected in baseline analysis.
- **Phase 3 (Hardening Review)**: IDMZ configuration audit would reveal lack of MFA. Session recording audit would identify missing controls. Jump server configuration review would flag domain trust between IT and OT.
- **Phase 4 (Controlled Validation)**: Attempted cross-zone RDP would validate segmentation effectiveness. Privilege escalation testing would confirm domain trust risk.

**IEC 62443 Failures:**
- SR 5.1 -- Network Segmentation: Jump server inadequately isolated IT and OT
- SR 1.12 -- Multi-Factor Authentication: No MFA on jump server
- SR 2.8 -- Auditable Events: No session recording
- SR 2.1 -- Authorization: Domain trust extended IT privileges into OT

---

### Scenario 3: Supply Chain Compromise via PLC Firmware Manipulation

**ATT&CK Chain**: T0862 (Supply Chain Compromise) -> T1693 (Modify Firmware) -> T0833 (Modify Program) -> T0836 (Modify Parameter) -> T0804/0805 (Block Command/Reporting Message)

**Walkthrough:**

1. **T0862 -- Supply Chain Compromise**: A threat actor compromises a third-party system integrator's engineering laptop. The integrator has legitimate access to client PLCs for maintenance and upgrades. The compromised laptop contains the attacker's payload, which activates when connected to the OT network.

2. **T1693 -- Modify Firmware**: During a scheduled maintenance window, the compromised engineering laptop downloads modified firmware to a safety-critical PLC. The firmware includes a backdoor that activates under specific process conditions. Because the download appears to come from an authorized engineering workstation with valid credentials, it raises no alarms.

3. **T0833 -- Modify Program**: The modified firmware alters the PLC's runtime logic. The change is subtle -- it only activates when specific operational parameters are met, making it difficult to detect during normal operations.

4. **T0836 -- Modify Parameter**: When triggered, the malicious logic modifies critical process parameters, pushing the controlled process into an unsafe state.

5. **T0804/0805 -- Block Command/Reporting Message**: The compromised firmware blocks SCADA commands to stop the process and suppresses alarm reporting, preventing operators from detecting or responding to the unsafe condition.

**Detection by Audit Phase:**

- **Phase 2 (Passive Discovery)**: Firmware download traffic during maintenance windows would be captured and logged. Anomalous protocol behavior during firmware update would be detected.
- **Phase 3 (Hardening Review)**: Firmware integrity verification process audit would identify gaps. Supply chain security policy review would flag third-party access risks. Electronic keying and firmware signing audit would identify protections not enabled.
- **Phase 4 (Controlled Validation)**: Firmware integrity testing would verify that unauthorized modifications are detected. Program comparison tools would identify logic changes.
- **Phase 5 (Reporting)**: Findings would map to supply chain security controls and vendor access management.

**IEC 62443 Failures:**
- SR 1.2 -- Device Identification and Authentication: No firmware signing verification
- SR 3.2 -- Malicious Code Protection: No integrity check before firmware deployment
- SR 2.1 -- Authorization: Third-party integrator had excessive PLC access
- SR 2.4 -- Mobile Code: No verification of code from external source
- SR 4.1 -- Information Confidentiality: PLC firmware accepted from unverified source

---

## Detection Gap Analysis Template

Use this template to evaluate your organization's current detection capability against each ATT&CK for ICS technique. For each technique, assess whether you can detect it with current tools and processes.

| ATT&CK Technique | Technique ID | Current Detection | Detection Tool/Process | Gap Description | Priority to Address |
| :--- | :---: | :---: | :--- | :--- | :---: |
| Drive-by Compromise | T0817 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Exploit Public-Facing Application | T0819 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| External Remote Services | T0822 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Internet Accessible Device | T0883 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Remote Services | T0886 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Rogue Master | T0848 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Supply Chain Compromise | T0862 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Modify Controller Tasking | T0821 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Modify Program | T0889 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Modify Firmware | T1693 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Default/Insecure Credentials | T1694 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Adversary-in-the-Middle | T0830 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Alarm Suppression | T0878 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Denial of Service | T0814 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Modify Parameter | T0836 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Block Communications | T1695 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| Valid Accounts | T0859 | [ ] Yes [ ] No [ ] Partial | | | [ ] Critical [ ] High [ ] Medium [ ] Low |
| [Add rows for additional techniques as needed] | | | | | |

**Instructions:**

1. For each technique, assess your current detection capability honestly -- "Partial" is acceptable if you have some but not complete coverage.
2. Document the specific tool or process that provides (or should provide) detection.
3. Describe the gap clearly -- what specifically is missing?
4. Prioritize based on the technique's potential impact on your environment (safety > production > compliance > best practice).

---

*Document version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
