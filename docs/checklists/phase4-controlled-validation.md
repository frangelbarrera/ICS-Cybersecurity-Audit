# Phase 4: Controlled Security Validation Checklist

## CRITICAL SAFETY DISCLAIMER

**ALL ACTIVE TESTING DESCRIBED IN THIS CHECKLIST REQUIRES:**

1. Written authorization signed by the client's authorized representative
2. Presence of a designated Safety Officer during all active testing
3. Confirmation that testing occurs within an approved maintenance window
4. Pre-tested emergency stop procedure that can halt all testing within 30 seconds
5. Rollback plan for any configuration change made during testing
6. Continuous communication with plant operations personnel

**Under no circumstances should active testing be performed on production systems without all of the above conditions met. Violation may result in process disruption, equipment damage, personnel injury, or loss of life.**

---

## Purpose

This checklist guides the auditor through controlled security validation of OT systems. Testing is limited to authorized activities within defined maintenance windows. The goal is to validate the effectiveness of security controls -- not to demonstrate exploitation.

**Reference Standards**: ISA/IEC 62443-3-3 (System Security Requirements), NIST SP 800-82r3 Section 6 (Security Controls)

---

## 1. Pre-Test Safety Checks (MANDATORY -- must be completed before any active test)

| # | Item | Status | Responsible | Safety Constraint | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 1.1 | Verify signed authorization letter and scope document are on-site and accessible | [ ] | Auditor + Client | STOP if authorization is missing, expired, or incomplete | SR 5.1 |
| 1.2 | Confirm all testing will be performed within the approved maintenance window | [ ] | Auditor + Client OT | STOP if outside authorized window -- reschedule | SR 5.1 |
| 1.3 | Verify Safety Officer is present on-site and has authority to halt testing | [ ] | Auditor | STOP if Safety Officer is unavailable | SR 4.2 |
| 1.4 | Confirm plant operations personnel are aware of testing and have direct communication line to auditor | [ ] | Client OT + Auditor | STOP if operations are not notified | SR 4.2 |
| 1.5 | Verify emergency stop procedure is tested and functional (auditor can halt all testing within 30 seconds) | [ ] | Auditor | STOP if emergency stop procedure cannot be demonstrated | SR 4.2 |
| 1.6 | Confirm rollback plan is documented for any configuration change that may be made during testing | [ ] | Auditor + Client OT | STOP if rollback is not documented and approved | SR 3.2 |
| 1.7 | Verify all test equipment (laptops, cables, tools) is listed in approved equipment appendix | [ ] | Auditor | STOP if unapproved equipment is present on-site | SR 2.4 |
| 1.8 | Confirm Safety Instrumented Systems (SIS) are categorically excluded from testing scope | [ ] | Auditor + Client | STOP immediately if any SIS device is accidentally targeted | SR 4.2 |

---

## 2. Network Access Control Testing

| # | Item | Status | Responsible | Safety Constraint | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 2.1 | Attempt to connect to HMI web interface using default credentials from an authorized test station | [ ] | Auditor | STOP if connection attempt causes HMI to freeze, reboot, or lock out operators | SR 1.1 |
| 2.2 | Attempt to access SCADA server login page without authentication (direct URL access to application paths) | [ ] | Auditor | STOP if SCADA application becomes unresponsive -- restore immediately | SR 1.1 |
| 2.3 | Test if operator-level accounts can access engineering configuration functions | [ ] | Auditor | STOP if any process alarm is triggered during privilege test | SR 2.1 |
| 2.4 | Attempt to browse network shares (SMB/NFS) on engineering workstations from IT network | [ ] | Auditor | STOP if file transfer could impact running engineering applications | SR 2.1 |
| 2.5 | Verify USB ports on HMI/engineering station are disabled or access-controlled (plug in approved test USB) | [ ] | Auditor | STOP if test USB triggers auto-run or interrupts HMI display | SR 2.4 |
| 2.6 | Test if unauthenticated SNMP read access provides device information on OT network devices | [ ] | Auditor | STOP if SNMP walk triggers device CPU spike or management interface lock | SR 3.1 |
| 2.7 | Verify that administrative interfaces (SSH, Telnet, HTTPS) on PLCs are not accessible from unauthorized VLANs | [ ] | Auditor | STOP if any communication disruption is detected on Level 0-1 traffic | SR 5.1 |

---

## 3. Segmentation Validation

| # | Item | Status | Responsible | Safety Constraint | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 3.1 | Test connectivity from IT network (Level 4) to OT supervision network (Level 3) -- should be blocked by IDMZ firewall | [ ] | Auditor | STOP if test traffic triggers IDS/IPS alert on OT side -- coordinate with security team | SR 5.1 |
| 3.2 | Test connectivity from OT supervision (Level 3) to control network (Level 1) -- verify only authorized protocols pass | [ ] | Auditor | STOP if any unexpected packet reaches a Level 1 controller | SR 5.1 |
| 3.3 | Attempt to bypass IDMZ firewall via alternate paths (secondary interfaces, VPN tunnels, wireless bridges) | [ ] | Auditor | STOP if route discovery could disrupt production traffic on alternate paths | SR 5.1 |
| 3.4 | Verify VLAN isolation: send ARP packets on one VLAN and confirm they do not leak to other VLANs | [ ] | Auditor | STOP if ARP traffic is observed on protected VLANs -- potential switch misconfiguration | SR 5.1 |
| 3.5 | Test firewall ruleset for default-deny behavior by sending traffic on non-whitelisted ports between zones | [ ] | Auditor | STOP if any unexpected connection succeeds to a Level 0-1 device | SR 5.2 |
| 3.6 | Verify that industrial firewall deep packet inspection (DPI) is correctly identifying and allowing only authorized Modbus function codes | [ ] | Auditor | STOP if DPI misconfiguration could block legitimate SCADA-to-PLC commands | SR 3.1 |

---

## 4. Protocol Security Testing

| # | Item | Status | Responsible | Safety Constraint | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 4.1 | Modbus TCP: Send read-only function codes (FC 01-04) from an unauthorized test station -- verify access is denied by firewall or PLC configuration | [ ] | Auditor | STOP if read attempt triggers PLC fault or watchdog timeout | SR 3.1 |
| 4.2 | Modbus TCP: Attempt to send write function codes (FC 05, 06, 15, 16) from unauthorized test station -- verify commands are dropped | [ ] | Auditor | **CRITICAL**: Test against replica PLC or during confirmed outage. STOP immediately if any write command reaches a production PLC. | SR 3.1 |
| 4.3 | S7Comm: Verify that read/write protection is enabled on Siemens controllers (attempt connection with S7 client without password) | [ ] | Auditor | STOP if connection attempt triggers PLC communication error on engineering station | SR 1.1 |
| 4.4 | S7Comm: Test if change of operating mode (STOP/RUN) is possible from unauthorized engineering station | [ ] | Auditor | **CRITICAL**: NEVER change mode on production PLC. Test against offline/replica only, or confirm PLC is in maintenance bypass. | SR 2.1 |
| 4.5 | EtherNet/IP: Verify CIP Security is enforced -- attempt unauthenticated CIP explicit message to read/write tag values | [ ] | Auditor | STOP if unauthenticated CIP message could modify I/O tag values | SR 3.1 |
| 4.6 | OPC UA: Test if anonymous authentication is accepted by OPC UA server (attempt connection with SecurityPolicy=None) | [ ] | Auditor | STOP if OPC UA server rejects legitimate client connections after test | SR 1.1 |
| 4.7 | OPC UA: Verify certificate validation -- attempt connection with self-signed or expired certificate | [ ] | Auditor | STOP if certificate manipulation causes trust chain breakage for legitimate clients | SR 1.2 |
| 4.8 | BACnet/IP: Send Who-Is broadcast from external network segment -- verify BBMD does not forward across boundaries | [ ] | Auditor | STOP if broadcast triggers device discovery storms on operational BACnet network | SR 5.1 |
| 4.9 | DNP3: Attempt unauthenticated control command (select/operate) on DNP3 outstation from unauthorized source | [ ] | Auditor | **CRITICAL**: Test against offline/replica or during confirmed outage. DNP3 control commands can operate breakers, valves, and switches. | SR 3.1 |

---

## 5. Wireless Assessment

| # | Item | Status | Responsible | Safety Constraint | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 5.1 | Survey for unauthorized WiFi access points in OT areas (2.4 GHz and 5 GHz bands) | [ ] | Auditor | STOP if WiFi scanning equipment could interfere with WirelessHART, ISA100.11a, or other industrial wireless | SR 4.2 |
| 5.2 | Identify Bluetooth-enabled devices in OT areas (engineering stations, PLC programming ports, wireless HMIs) | [ ] | Auditor | STOP if Bluetooth scanning interferes with Bluetooth-based industrial sensors | SR 4.2 |
| 5.3 | Verify wireless network used for OT is on dedicated SSID with WPA3-Enterprise or WPA2-Enterprise (not PSK) | [ ] | Auditor | STOP if wireless scanning disrupts active WiFi connections to mobile HMIs | SR 3.1 |
| 5.4 | Test if OT wireless network is isolated from IT wireless network (attempt cross-SSID communication) | [ ] | Auditor | STOP if test traffic could impact industrial wireless devices on 2.4 GHz | SR 5.1 |
| 5.5 | Document any rogue wireless devices detected and their approximate location (signal strength triangulation) | [ ] | Auditor | STOP if locating rogue device requires entering restricted plant areas | SR 2.8 |

---

## 6. Post-Test Verification

| # | Item | Status | Responsible | Safety Constraint | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 6.1 | Verify all test equipment is disconnected from the OT network | [ ] | Auditor | Confirm physically -- visual inspection of all connection points | SR 5.1 |
| 6.2 | Verify no test user accounts, sessions, or credentials remain active on any OT system | [ ] | Auditor + Client | Lock/delete any test accounts created during validation | SR 1.11 |
| 6.3 | Verify all configuration changes made during testing are rolled back to pre-test state | [ ] | Auditor + Client OT | Confirm rollback against documented baseline | SR 3.2 |
| 6.4 | Verify all OT systems return to normal operational state (no errors, no alarms triggered by testing) | [ ] | Client OT + Auditor | Check SCADA alarm list for any test-induced alarms | SR 2.8 |
| 6.5 | Confirm with plant operations that all processes are operating within normal parameters | [ ] | Client OT | Verbal confirmation from shift supervisor | SR 4.2 |
| 6.6 | Document all test results, including both successful validations and identified weaknesses | [ ] | Auditor | Findings feed into Phase 5 technical report | SR 2.8 |
| 6.7 | Archive all test logs, packet captures, and screenshots with chain of custody | [ ] | Auditor | SHA-256 hash of all evidence files | SR 2.8 |

---

## Phase 4 Completion Sign-Off

| Field | Details |
| :--- | :--- |
| **All pre-test safety checks completed and verified** | [ ] Yes [ ] No |
| **No safety incidents or process disruptions during testing** | [ ] Yes [ ] No -- document below |
| **All test equipment removed from OT network** | [ ] Yes [ ] No |
| **All configuration changes rolled back** | [ ] Yes [ ] No |
| **All findings documented and evidence archived** | [ ] Yes [ ] No |
| **Ready to proceed to Phase 5 (Reporting and Remediation)** | [ ] Yes [ ] No |
| **Auditor Name / Signature** | |
| **Safety Officer Name / Signature** | |
| **Client Representative Name / Signature** | |
| **Date** | |

**Incidents and Observations:**

[Document any alarms triggered, unexpected behavior, or deviations from test plan. Include corrective actions taken.]

---

*Checklist version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
