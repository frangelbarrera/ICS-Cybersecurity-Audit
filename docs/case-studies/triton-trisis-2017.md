# Case Study: TRITON / TRISIS (2017)

## The First Malware Targeting Safety Instrumented Systems

---

### Executive Summary

**What happened**: In August 2017, a petrochemical facility in Saudi Arabia experienced a plant safety shutdown triggered by the Safety Instrumented System (SIS). Investigation revealed that the shutdown was caused by TRITON (also known as TRISIS or HatMan), the first known malware specifically designed to target and compromise Safety Instrumented Systems. TRITON targeted Schneider Electric Triconex SIS controllers, attempting to modify the safety logic that would have disabled the plant's fail-safe mechanisms. If successful, a subsequent process upset could have resulted in catastrophic equipment failure, toxic gas release, or explosion.

**When**: The initial compromise likely occurred in 2016-2017. The safety shutdown that led to discovery occurred in August 2017. The malware was publicly disclosed by FireEye/Mandiant and Dragos in December 2017.

**Impact**: The plant experienced an automatic safety shutdown (the SIS functioned correctly despite the compromise attempt). The forensic investigation revealed that the attackers had gained deep access to the OT environment and had specifically targeted the Safety Instrumented System. The incident is considered one of the most significant OT cyber events due to its clear intent to cause physical destruction with potential loss of life.

**Attribution**: The attack was attributed to the Russian-sponsored Central Scientific Research Institute of Chemistry and Mechanics (TsNIIKhM), a state-owned research institution. The malware and associated tools were linked to a group tracked as TEMP.Veles (FireEye) or XENOTIME (Dragos).

---

### ATT&CK for ICS Techniques Used

| Technique ID | Technique Name | How It Was Used |
| :---: | :--- | :--- |
| T0822 | External Remote Services | Initial access to the facility's IT/OT network via remote services (details of initial access vector remain classified by the victim) |
| T0886 | Remote Services | Lateral movement within the OT network to reach the engineering workstation connected to the Triconex SIS |
| T0840 | Network Connection Enumeration | Reconnaissance to locate the Triconex engineering workstation and map the SIS architecture |
| T0888 | Remote System Information Discovery | Gathering information about the Triconex SIS controllers, including firmware versions and safety logic configurations |
| T1693 | Modify Firmware | Developing and deploying custom malware (TRITON) to modify the Triconex controller firmware |
| T0833 | Modify Program | Attempting to modify the SIS safety logic to prevent the system from triggering a safety shutdown under dangerous conditions |
| T0878 | Alarm Suppression | The modified logic would have suppressed safety alarms and prevented the SIS from activating protective actions |
| T0804 | Block Command Message | TRITON was designed to prevent the SIS from sending shutdown commands to final control elements |
| T0859 | Valid Accounts | Using compromised credentials to access the Triconex engineering workstation and communicate with the SIS controller |
| T0890 | Exploitation for Privilege Escalation | Exploiting vulnerabilities in the Triconex TriStation protocol to gain privileged access to the SIS controller |

---

### IEC 62443-3-3 Security Requirement Failures

| Security Requirement | Failure Description |
| :--- | :--- |
| **SR 1.1 -- Identification and Authentication** | The Triconex SIS controller did not require strong authentication for firmware updates or program downloads |
| **SR 1.2 -- Software Process and Device Authentication** | The SIS controller accepted modified firmware without cryptographic signature verification |
| **SR 2.1 -- Authorization** | The engineering workstation had excessive privileges -- any user with workstation access could modify SIS logic |
| **SR 3.1 -- Communication Integrity** | The TriStation protocol lacked integrity protection; commands between the engineering workstation and SIS controller could be intercepted and modified |
| **SR 4.1 -- Information Confidentiality** | Safety logic and firmware were readable and writable by any device with network access to the SIS controller |
| **SR 4.2 -- Physical Security** | The SIS was logically accessible from the general control network rather than being physically or logically isolated |
| **SR 5.1 -- Network Segmentation** | The SIS was not adequately segmented from the rest of the OT network; no boundary protection between basic process control and safety |
| **SR 3.2 -- Malicious Code Protection** | No mechanism to verify the integrity of code running on the SIS controller; no whitelisting or behavior monitoring on the engineering workstation |

---

### NIST SP 800-82 Control Failures

| Control Area | Failure Description |
| :--- | :--- |
| **Access Control (6.2.1)** | Engineering workstation lacked MFA; no separation between process control and safety system access |
| **System Integrity (6.2.4)** | No firmware signing or integrity verification for SIS controllers; no program change detection |
| **Network Segmentation (6.2.6)** | Safety Instrumented System not logically or physically separated from Basic Process Control System |
| **Audit and Accountability (6.3.3)** | No logging of firmware modifications or SIS logic changes; changes detected only when safety shutdown occurred |
| **Incident Response (6.4.1)** | No procedure for detecting or responding to SIS compromise; attack discovered accidentally via safety shutdown |

---

### Purdue Model Layer Affected

| Purdue Level | Impact |
| :---: | :--- |
| **Level 4 (Enterprise)** | Not directly impacted; initial access point not publicly confirmed |
| **Level 3 (Site Operations)** | Engineering workstations and SCADA systems potentially compromised as intermediate targets |
| **Level 2 (Area Supervision)** | Triconex engineering workstation -- the primary target for SIS access |
| **Level 1 (Basic Control)** | Triconex SIS controllers directly targeted with custom firmware malware |
| **Level 0 (Process)** | Not directly impacted (the SIS triggered a safe shutdown) -- but the attacker's goal was to prevent future safe shutdowns, which would have allowed a Level 0 catastrophe |

---

### How This Audit Framework Would Have Detected It

| Audit Phase | Detection Opportunity |
| :--- | :--- |
| **Phase 1 -- Documentation** | Network architecture review would have flagged the SIS as being logically accessible from the control network, identifying the need for physical or logical isolation |
| **Phase 2 -- Passive Discovery** | Baseline traffic analysis would have captured unusual TriStation protocol traffic to the SIS controller from unauthorized sources |
| **Phase 3 -- Hardening Review** | The following would have been Critical findings: (a) SIS not isolated from basic process control network, (b) No firmware signing on SIS controller, (c) No authentication for SIS firmware/program downloads, (d) No change detection on SIS logic, (e) No separation of safety-related access from process control access |
| **Phase 4 -- Controlled Validation** | Testing would have confirmed: (a) SIS reachable from control network, (b) Firmware and logic modifiable without authentication, (c) No alarms generated by unauthorized SIS access |
| **Phase 5 -- Reporting** | Overall risk rating: Critical. A compromised SIS represents the highest possible risk in an industrial environment because it directly threatens human life and environmental safety. |

---

### Key Lessons

1. **Safety Instrumented Systems must be physically or logically isolated**: The SIS must never be reachable from the same network as the Basic Process Control System. IEC 61511 requires independence between protection layers.
2. **SIS controllers need the same security rigor as any other OT device**: The assumption that SIS controllers are inherently secure because they are proprietary or obscure is dangerously wrong. They need authentication, firmware signing, and access controls.
3. **Firmware integrity verification is essential**: If the Triconex controller had cryptographic firmware signing and the engineering workstation verified signatures before download, the TRITON malware would not have loaded.
4. **The intent of OT attackers has escalated**: TRITON demonstrated that attackers are willing to target safety systems and cause physical destruction with potential for loss of life. Threat modeling must account for this escalation.
5. **SIS program changes must be detected and alerted in real time**: Any modification to SIS logic or firmware should generate an immediate alarm to operations and security personnel, regardless of whether the change appears to come from an authorized workstation.
6. **Engineering workstations for SIS must be dedicated and hardened**: The SIS engineering workstation should be a single-purpose device, physically and logically isolated, with no internet access, strong authentication, and application whitelisting.
7. **Regular SIS proof-testing includes cybersecurity**: Periodic proof-testing of safety functions should include verification that the SIS logic and firmware match the approved, known-good baseline.

---

### References

1. Dragos, Inc. (2017). *TRISIS Malware: Analysis of Safety System Targeted Malware*. https://www.dragos.com/wp-content/uploads/TRISIS-01.pdf
2. FireEye Mandiant. (2017). *Attackers Deploy New ICS Attack Framework "TRITON" and Cause Operational Disruption to Critical Infrastructure*. https://www.mandiant.com/resources/blog/attackers-deploy-new-ics-attack-framework-triton
3. Johnson, B., Caban, D., Krotofil, M., Scali, D., Brubaker, N., & Glyer, C. (2019). *Triton Actor TTP Profile, Custom Attack Tools, Detections, and ATT&CK Mapping*. FireEye Mandiant.
4. MITRE ATT&CK for ICS. *Triton Safety Instrumented System Attack*. https://attack.mitre.org/campaigns/C0030/
5. ICS-CERT. (2017). *MAR-17-352-01: HatMan -- Safety System Targeted Malware (Update A)*. https://www.cisa.gov/news-events/ics-advisories/icsa-17-318-01

---

*Case study version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
