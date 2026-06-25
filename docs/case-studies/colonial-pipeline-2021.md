# Case Study: Colonial Pipeline Ransomware (2021)

## When an IT Ransomware Attack Shuts Down Critical OT Infrastructure

---

### Executive Summary

**What happened**: On May 7, 2021, Colonial Pipeline Company, which operates the largest refined products pipeline in the United States (approximately 5,500 miles, transporting 2.5 million barrels per day of gasoline, diesel, and jet fuel), suffered a ransomware attack by the DarkSide criminal group. The ransomware encrypted data on Colonial's corporate IT network. In response, Colonial proactively shut down pipeline operations -- the first time in the company's history it had taken such action. The attack did NOT directly compromise OT/SCADA systems, but the company's decision to halt operations (driven by concerns over billing systems, scheduling software, and uncertainty about whether OT systems had been affected) caused a 5-day shutdown and cascading fuel shortages across the southeastern United States.

**When**: Attack detected May 7, 2021; pipeline operations restored May 12, 2021. Fuel shortages and panic buying persisted for approximately 2 weeks in affected regions.

**Impact**: 5-day pipeline shutdown; fuel shortages across 12+ states; average US gas prices rose to their highest level since 2014; Colonial Pipeline paid approximately $4.4 million in ransom (approximately $2.3 million of which was recovered by the US Department of Justice); the attack triggered the first-ever emergency declaration under a new US cybersecurity executive order.

**Attribution**: DarkSide, a ransomware-as-a-service (RaaS) criminal group believed to operate from Eastern Europe or Russia. The group publicly claimed they were financially motivated and did not intend to cause societal disruption.

---

### ATT&CK for ICS Techniques Used

| Technique ID | Technique Name | How It Was Used |
| :---: | :--- | :--- |
| T0859 | Valid Accounts | Initial access believed to be via a compromised VPN account using credentials from a previous data breach (exact account details remain unconfirmed) |
| T0822 | External Remote Services | VPN access provided entry point to Colonial's corporate IT network |
| T0840 | Network Connection Enumeration | Attackers performed reconnaissance on the IT network to identify high-value targets (file servers, domain controllers, backup systems) |
| T0867 | Lateral Tool Transfer | Moved ransomware payload across IT systems using standard enterprise tools and protocols (SMB, RDP) |
| T0881 | Service Stop | Disabled security tools and backup services before deploying ransomware |
| T0809 | Data Destruction/Encryption | Ransomware encrypted data on approximately 100 GB of corporate IT systems |
| T0826 | Loss of Productivity and Revenue | The decision to proactively shut down OT operations caused financial losses estimated at tens of millions of dollars in ransom, lost revenue, and recovery costs |

**Note**: Unlike the other case studies in this directory, Colonial Pipeline did NOT experience direct OT/SCADA compromise. The ATT&CK techniques used were primarily enterprise IT tactics applied to an organization where IT and OT were operationally interdependent. The shutdown was a defensive decision -- not an attacker action against OT systems.

---

### IEC 62443-3-3 Security Requirement Failures

| Security Requirement | Failure Description |
| :--- | :--- |
| **SR 1.12 -- Multi-Factor Authentication** | VPN access to the corporate IT network used single-factor authentication (reports indicated the compromised account was protected only by a password) |
| **SR 5.1 -- Network Segmentation** | While OT systems were not directly compromised, the IT/OT operational dependency meant that an IT outage forced an OT shutdown. The billing and scheduling systems required for pipeline operations were hosted on the IT network. |
| **SR 4.1 -- Information Confidentiality** | Approximately 100 GB of corporate data was exfiltrated by the attackers before encryption |
| **SR 3.2 -- Malicious Code Protection** | Endpoint detection and response (EDR) did not prevent or contain the ransomware before it spread across the IT network |

---

### NIST SP 800-82 Control Failures

| Control Area | Failure Description |
| :--- | :--- |
| **Access Control (6.2.1)** | VPN access lacked MFA; credential reuse from previous breaches was not detected |
| **Business Continuity (6.5.1)** | OT operations depended on IT systems (billing, scheduling) to function; no OT contingency plan for extended IT outage |
| **Incident Response (6.4.1)** | The decision to shut down the pipeline was made without a pre-existing playbook for ransomware scenarios affecting IT/OT interdependencies |
| **Audit and Accountability (6.3.3)** | Lack of visibility into anomalous VPN activity allowed the attackers to operate undetected in the IT environment prior to ransomware deployment |

---

### Purdue Model Layer Affected

| Purdue Level | Impact |
| :---: | :--- |
| **Level 4 (Enterprise)** | Corporate IT systems directly impacted -- file servers, email, billing, scheduling systems encrypted by ransomware |
| **Level 3.5 (Industrial DMZ)** | Not directly compromised, but the operational dependency between IT billing/scheduling and OT pipeline control forced the OT shutdown |
| **Level 3 (Site Operations)** | SCADA and pipeline control systems were NOT directly compromised -- Colonial confirmed OT systems remained operational throughout |
| **Level 2-0** | Not affected -- pipeline control systems remained intact; the shutdown was a proactive business decision |

---

### How This Audit Framework Would Have Detected It

| Audit Phase | Detection Opportunity |
| :--- | :--- |
| **Phase 1 -- Documentation** | Business impact analysis would have identified IT/OT operational dependencies: "If IT billing and scheduling systems are unavailable, can OT pipeline operations continue?" This would have surfaced the need for OT-independent operational procedures. |
| **Phase 2 -- Passive Discovery** | An OT-focused Phase 2 might not have detected the IT-side precursor activity unless OT network monitoring extended to the IT/OT boundary and IDMZ traffic analysis. |
| **Phase 3 -- Hardening Review** | The following would have been findings: (a) VPN access lacks MFA -- Critical, (b) IT/OT operational dependency documented but no contingency plan -- High, (c) No OT-specific incident response playbook for ransomware scenarios -- High, (d) No OT-offline operational capability (billing/scheduling redundancy) -- Medium |
| **Phase 4 -- Controlled Validation** | MFA bypass testing would have confirmed the VPN vulnerability. Tabletop exercises for ransomware affecting IT/OT would have identified the operational dependency gap. |
| **Phase 5 -- Reporting** | Risk rating would have been High for business continuity and IT/OT convergence risks. |

---

### Key Lessons

1. **IT/OT convergence creates cascading risk**: The attackers never touched a PLC, SCADA server, or HMI. Yet the pipeline shut down for 5 days because OT operations depended on IT systems. Critical OT functions must be able to operate independently of IT.
2. **MFA on all remote access is non-negotiable**: The most likely initial access vector was a compromised VPN account without MFA. This is the single most impactful control that would have prevented the attack.
3. **OT needs its own incident response playbooks**: The decision to shut down was made without a pre-planned, tested procedure. OT-specific ransomware playbooks should define exactly when to shut down, who decides, and how to operate without IT.
4. **Business continuity for OT must include IT outage scenarios**: "What if our billing system is down?" should not force a pipeline shutdown. Manual, offline operational procedures must exist and be regularly tested.
5. **Proactive OT shutdown is a valid defensive action**: Colonial's decision to shut down was controversial but defensible. The alternative -- continuing operations during an active ransomware incident with unknown OT impact -- could have been far worse.
6. **Paying ransoms funds future attacks**: Colonial paid $4.4 million. The FBI recovered $2.3 million, but the payment reinforced the ransomware business model. Organizations need robust backups and tested recovery procedures to make paying unnecessary.
7. **Regulatory response can be swift and consequential**: The Colonial Pipeline attack triggered the first Transportation Security Administration (TSA) security directives for pipeline cybersecurity, mandating specific controls. Organizations in critical infrastructure sectors should anticipate regulatory requirements rather than waiting for a mandate.

---

### References

1. CISA. (2021). *DarkSide Ransomware: Best Practices for Preventing Business Disruption from Ransomware Attacks*. https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-131a
2. US Department of Justice. (2021). *Department of Justice Seizes $2.3 Million in Cryptocurrency Paid to the Ransomware Extortionists Darkside*. https://www.justice.gov/opa/pr/department-justice-seizes-23-million-cryptocurrency-paid-ransomware-extortionists-darkside
3. Transportation Security Administration. (2021). *Security Directive Pipeline-2021-01: Enhancing Pipeline Cybersecurity*. https://www.tsa.gov/for-industry/pipeline-cybersecurity
4. Turton, W. & Mehrotra, K. (2021). *Hackers Breached Colonial Pipeline Using Compromised Password*. Bloomberg News. https://www.bloomberg.com/news/articles/2021-06-04/hackers-breached-colonial-pipeline-using-compromised-password
5. US Government Accountability Office. (2022). *Colonial Pipeline Cyberattack Highlights Need for Better Federal and Private-Sector Preparedness*. GAO-22-104995.

---

*Case study version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
