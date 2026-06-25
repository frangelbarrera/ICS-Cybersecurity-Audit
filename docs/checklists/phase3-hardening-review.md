# Phase 3: Configuration and Hardening Review Checklist

## Purpose

This checklist guides the auditor through a systematic review of OT system configurations and security hardening. Findings are mapped to IEC 62443-3-3 System Requirements (SR) and NIST SP 800-82r3 controls for traceability.

**Safety Precondition**: All configuration reviews are performed on offline backups or read-only copies. No changes are made to live systems.

---

## 1. PLC / Controller Hardening

| # | Check Item | Status | Finding | Severity | IEC 62443 Ref | NIST 800-82 Ref |
| :---: | :--- | :---: | :--- | :---: | :--- | :--- |
| 1.1 | Verify no default credentials on any PLC (Siemens, Allen-Bradley, Schneider, etc.) | [ ] Pass [ ] Fail [ ] N/A | | Critical / High / Med / Low | SR 1.1 | Section 6.2.1 |
| 1.2 | Verify firmware is at vendor-recommended version (check against latest security advisories) | [ ] Pass [ ] Fail [ ] N/A | | | SR 3.2 | Section 6.2.3 |
| 1.3 | Verify access protection / know-how protection is enabled (Siemens S7-1200/1500) | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.1 | Section 6.2.1 |
| 1.4 | Verify CIP Security is enabled (Allen-Bradley ControlLogix/CompactLogix) | [ ] Pass [ ] Fail [ ] N/A | | | SR 3.1 | Section 6.2.1 |
| 1.5 | Verify application password is set (Schneider M340/M580) | [ ] Pass [ ] Fail [ ] N/A | | | SR 1.1 | Section 6.2.1 |
| 1.6 | Verify unused communication protocols are disabled on each controller | [ ] Pass [ ] Fail [ ] N/A | | | SR 7.1 | Section 6.2.4 |
| 1.7 | Verify web server interface is disabled or access-controlled on each controller | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.1 |
| 1.8 | Verify electronic keying is configured (Allen-Bradley -- Exact Match or Compatible Module) | [ ] Pass [ ] Fail [ ] N/A | | | SR 3.2 | Section 6.2.4 |
| 1.9 | Review PLC program for hardcoded credentials or sensitive data in logic comments | [ ] Pass [ ] Fail [ ] N/A | | | SR 1.1 | Section 6.2.1 |

---

## 2. HMI / SCADA Hardening

| # | Check Item | Status | Finding | Severity | IEC 62443 Ref | NIST 800-82 Ref |
| :---: | :--- | :---: | :--- | :---: | :--- | :--- |
| 2.1 | Verify SCADA/HMI servers run vendor-supported and patched operating system | [ ] Pass [ ] Fail [ ] N/A | | | SR 3.2 | Section 6.3.1 |
| 2.2 | Verify no default credentials on SCADA/HMI applications (WinCC, FactoryTalk, iFIX, etc.) | [ ] Pass [ ] Fail [ ] N/A | | | SR 1.1 | Section 6.3.1 |
| 2.3 | Verify role-based access control (RBAC) is configured with least-privilege principle | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.1 | Section 6.3.1 |
| 2.4 | Verify operator accounts cannot modify engineering configurations | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.11 | Section 6.3.1 |
| 2.5 | Verify automatic logout / screen lock is configured after idle timeout (max 15 minutes) | [ ] Pass [ ] Fail [ ] N/A | | | SR 1.11 | Section 6.3.1 |
| 2.6 | Verify audit logging is enabled and logs are forwarded to a central SIEM | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.8 | Section 6.3.3 |
| 2.7 | Verify anti-virus / application whitelisting is installed and up to date | [ ] Pass [ ] Fail [ ] N/A | | | SR 3.2 | Section 6.3.20 |
| 2.8 | Verify project encryption is enabled (TIA Portal WinCC, FactoryTalk View) | [ ] Pass [ ] Fail [ ] N/A | | | SR 4.1 | Section 6.3.1 |
| 2.9 | Verify USB and removable media ports are disabled or controlled on all HMI/SCADA hosts | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.4 | Section 6.5.2 |

---

## 3. Network Infrastructure Hardening

| # | Check Item | Status | Finding | Severity | IEC 62443 Ref | NIST 800-82 Ref |
| :---: | :--- | :---: | :--- | :---: | :--- | :--- |
| 3.1 | Verify network segmentation aligns with Purdue model (Levels 0-3 separated) | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.6 |
| 3.2 | Verify industrial firewalls are deployed at zone boundaries with least-privilege rules | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.6 |
| 3.3 | Verify no default credentials on managed switches, firewalls, or routers | [ ] Pass [ ] Fail [ ] N/A | | | SR 1.1 | Section 6.2.1 |
| 3.4 | Verify switch port security is enabled (MAC limiting, sticky MAC, port shutdown on violation) | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.6 |
| 3.5 | Verify unused switch ports are administratively disabled | [ ] Pass [ ] Fail [ ] N/A | | | SR 7.1 | Section 6.2.6 |
| 3.6 | Verify VLANs are properly configured and trunk ports are secured (no VLAN 1 for user traffic) | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.6 |
| 3.7 | Verify DHCP snooping, ARP inspection, and IP Source Guard are enabled on OT switches | [ ] Pass [ ] Fail [ ] N/A | | | SR 3.1 | Section 6.2.6 |
| 3.8 | Verify SNMP is v3 only (no SNMP v1/v2c) or disabled if not needed | [ ] Pass [ ] Fail [ ] N/A | | | SR 3.1 | Section 6.2.1 |
| 3.9 | Verify LLDP/CDP is disabled on OT network interfaces facing untrusted segments | [ ] Pass [ ] Fail [ ] N/A | | | SR 7.1 | Section 6.2.4 |
| 3.10 | Verify network device management is on a dedicated out-of-band VLAN | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.6 |

---

## 4. Remote Access Hardening

| # | Check Item | Status | Finding | Severity | IEC 62443 Ref | NIST 800-82 Ref |
| :---: | :--- | :---: | :--- | :---: | :--- | :--- |
| 4.1 | Verify all remote access to OT traverses an Industrial DMZ (IDMZ) | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.6 |
| 4.2 | Verify multi-factor authentication (MFA) is enforced for all remote access | [ ] Pass [ ] Fail [ ] N/A | | | SR 1.12 | Section 6.3.1 |
| 4.3 | Verify jump servers are used (no direct remote desktop to OT assets) | [ ] Pass [ ] Fail [ ] N/A | | | SR 5.1 | Section 6.2.6 |
| 4.4 | Verify session recording is enabled on jump servers for audit purposes | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.8 | Section 6.3.3 |
| 4.5 | Verify vendor remote access uses time-limited, just-in-time credentials | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.1 | Section 6.2.1 |
| 4.6 | Verify modems (PSTN, cellular) on OT equipment are identified, documented, and secured | [ ] Pass [ ] Fail [ ] N/A | | | SR 4.2 | Section 6.5.2 |

---

## 5. Physical Security

| # | Check Item | Status | Finding | Severity | IEC 62443 Ref | NIST 800-82 Ref |
| :---: | :--- | :---: | :--- | :---: | :--- | :--- |
| 5.1 | Verify physical access to control rooms and PLC enclosures is restricted to authorized personnel | [ ] Pass [ ] Fail [ ] N/A | | | SR 4.2 | Section 6.5.1 |
| 5.2 | Verify access control system logs are reviewed periodically | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.8 | Section 6.5.1 |
| 5.3 | Verify unused physical ports (USB, Ethernet, serial) on HMIs and engineering stations are locked or disabled | [ ] Pass [ ] Fail [ ] N/A | | | SR 2.4 | Section 6.5.2 |
| 5.4 | Verify key-operated switches on PLCs are in "Run" (not "Program/Remote") position during normal operation | [ ] Pass [ ] Fail [ ] N/A | | | SR 4.2 | Section 6.5.1 |
| 5.5 | Verify environmental controls (temperature, humidity) are monitored for equipment rooms | [ ] Pass [ ] Fail [ ] N/A | | | SR 4.1 | Section 6.5.1 |

---

## Severity Classification Criteria

| Severity | Criteria |
| :--- | :--- |
| **Critical** | Direct safety impact, loss of view/control, unauthenticated remote access, default credentials on Level 1 device |
| **High** | Significant security gap, exploitable from adjacent zone, missing segmentation, EOL firmware with known CVE |
| **Medium** | Configuration weakness, defense-in-depth gap, policy violation without immediate exploit path |
| **Low** | Best practice deviation, informational finding, hardening opportunity |

---

## Phase 3 Completion Sign-Off

| | |
| :--- | :--- |
| **All items reviewed and findings documented** | [ ] Yes [ ] No |
| **Findings severity reviewed with client** | [ ] Yes [ ] No |
| **Ready to proceed to Phase 4 (Controlled Validation)** | [ ] Yes [ ] No |
| **Auditor Name / Signature** | |
| **Date** | |

---

*Checklist version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
