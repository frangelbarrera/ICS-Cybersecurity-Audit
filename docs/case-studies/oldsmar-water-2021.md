# Case Study: Oldsmar Water Treatment Attack (2021)

## Remote Access Without MFA Threatens Public Safety

---

### Executive Summary

**What happened**: On February 5, 2021, an attacker gained unauthorized remote access to the SCADA system controlling the water treatment plant in Oldsmar, Florida (population approximately 15,000). The attacker used TeamViewer software installed on an operator workstation and increased the sodium hydroxide (lye) setpoint from 100 parts per million (ppm) to 11,100 ppm -- a dangerously high level that could cause severe health effects if consumed. A plant operator observed the mouse cursor moving on screen and watched as the attacker changed the setpoint. The operator immediately corrected the change and notified supervisors. No harm occurred, and the water supply was not compromised.

**When**: February 5, 2021, at approximately 1:30 PM EST. The attacker was active for approximately 3-5 minutes before being detected.

**Impact**: No physical harm to the public. The sodium hydroxide level was corrected before it could affect the water supply (the water treatment process includes approximately 24-36 hours of retention time before water reaches consumers). The incident caused significant reputational damage and regulatory scrutiny. It resulted in multiple security advisories from CISA and EPA, and accelerated the development of cybersecurity requirements for the US water sector.

**Attribution**: No group or individual has been publicly identified or charged. The attack vector (TeamViewer with shared credentials and no MFA) is consistent with opportunistic rather than targeted attack patterns. The IP address used by the attacker was traced to a location outside the United States, but further attribution details remain unconfirmed.

---

### ATT&CK for ICS Techniques Used

| Technique ID | Technique Name | How It Was Used |
| :---: | :--- | :--- |
| T0822 | External Remote Services | Gained access to the plant's SCADA system via TeamViewer remote desktop software exposed to the internet |
| T1694 | Insecure Credentials | Exploited shared TeamViewer credentials -- all plant operators and supervisors used the same password for remote access |
| T0886 | Remote Services | TeamViewer provided direct graphical access to the HMI/SCADA workstation without a jump server or VPN intermediary |
| T0823 | Graphical User Interface | Interacted directly with the SCADA HMI screen to locate and modify the sodium hydroxide setpoint |
| T0836 | Modify Parameter | Changed the chemical dosing setpoint from 100 ppm to 11,100 ppm (110x increase) |
| T0801 | Monitor Process State | Observed the HMI display to identify which control to manipulate (the attacker moved the mouse cursor around the screen before making the change) |

---

### IEC 62443-3-3 Security Requirement Failures

| Security Requirement | Failure Description |
| :--- | :--- |
| **SR 1.1 -- Identification and Authentication** | TeamViewer used shared credentials across all operators; no individual user accounts; attacker could not be distinguished from legitimate operator |
| **SR 1.12 -- Multi-Factor Authentication** | No MFA on TeamViewer remote access -- a password alone was sufficient to gain full control of the SCADA workstation |
| **SR 2.1 -- Authorization** | All TeamViewer users had the same privilege level; no role-based differentiation between view-only monitoring and setpoint modification |
| **SR 2.8 -- Auditable Events** | TeamViewer logs existed but did not trigger real-time alerts; the operator detected the intrusion visually, not through an alert |
| **SR 2.11 -- Least Privilege** | The remote access tool provided full desktop control (keyboard + mouse) rather than restricted access to specific SCADA functions |
| **SR 5.1 -- Network Segmentation** | The SCADA workstation was directly internet-accessible via TeamViewer; no jump server, VPN, or IDMZ architecture |
| **SR 3.1 -- Communication Integrity** | TeamViewer communications were encrypted between endpoints, but there was no verification that the remote user was authorized before granting access to OT functions |

---

### NIST SP 800-82 Control Failures

| Control Area | Failure Description |
| :--- | :--- |
| **Access Control (6.2.1)** | No MFA for remote access; shared credentials; no individual accountability |
| **Network Segmentation (6.2.6)** | SCADA workstation directly accessible from internet via TeamViewer -- no DMZ, jump server, or VPN gateway |
| **Audit and Accountability (6.3.3)** | No real-time alerting on remote access sessions; detection relied on operator observation |
| **Identification and Authentication (6.2.1)** | No mechanism to uniquely identify remote users or limit their capabilities based on role |

---

### Purdue Model Layer Affected

| Purdue Level | Impact |
| :---: | :--- |
| **Level 4 (Enterprise)** | Not directly affected; the internet connection to the SCADA workstation bypassed any enterprise IT infrastructure |
| **Level 3.5 (Industrial DMZ)** | Non-existent -- no DMZ architecture existed between the internet and the SCADA system |
| **Level 3 (Site Operations)** | SCADA workstation directly compromised via TeamViewer; HMI display and controls exposed |
| **Level 2 (Area Supervision)** | The compromised workstation functioned as the plant's HMI/SCADA interface |
| **Level 1 (Basic Control)** | Not directly accessed by the attacker, but setpoint changes from the SCADA workstation would have been transmitted to the PLC controlling chemical dosing |
| **Level 0 (Process)** | Not impacted -- the operator detected and reversed the setpoint change before it affected the chemical dosing process |

---

### How This Audit Framework Would Have Detected It

| Audit Phase | Detection Opportunity |
| :--- | :--- |
| **Phase 1 -- Documentation** | Network architecture review would have identified the TeamViewer installation as an unmanaged remote access path. Asset inventory would have flagged the SCADA workstation's internet accessibility. |
| **Phase 2 -- Passive Discovery** | Baseline traffic analysis would have detected unexpected TeamViewer traffic from external IP addresses to the SCADA workstation. Protocol analysis would have identified remote access sessions outside normal business hours. |
| **Phase 3 -- Hardening Review** | The following would have been Critical findings: (a) SCADA workstation directly accessible from the internet via TeamViewer without VPN or jump server, (b) Shared remote access credentials with no MFA, (c) No role-based access to limit remote users to view-only, (d) No real-time alerting on remote access sessions, (e) No centralized logging of remote access activity with alerting thresholds |
| **Phase 4 -- Controlled Validation** | Testing would have confirmed: (a) TeamViewer accessible from external IP address with shared credentials, (b) Remote user has full desktop control including setpoint modification capability, (c) No alarm generated when setpoint is changed remotely |
| **Phase 5 -- Reporting** | Overall risk rating: Critical. Direct public health impact from chemical setpoint manipulation. Every element of the remote access architecture failed simultaneously. |

---

### Key Lessons

1. **Remote access to OT must never use consumer-grade tools without enterprise security controls**: TeamViewer, AnyDesk, VNC, and similar tools are convenient but are not designed for OT security. They must be deployed behind a VPN with MFA, or replaced with OT-specific remote access solutions.
2. **MFA is the single most impactful control for remote access**: A password alone was sufficient to gain full SCADA control. Even a simple SMS-based MFA would have prevented the attack or at least provided an alert of unauthorized access attempts.
3. **Shared credentials eliminate accountability**: When all operators use the same password, there is no way to distinguish legitimate access from unauthorized access. Individual accounts with role-based privileges are essential.
4. **Remote access should default to view-only with elevated privileges requiring explicit approval**: An operator monitoring from home does not need the ability to change chemical setpoints. Just-in-time privilege elevation with approval workflow would have prevented the modification.
5. **Operator vigilance is the last line of defense -- and it worked**: The operator at Oldsmar noticed the mouse cursor moving and watched the attacker make the change. This human detection layer is critical, but it should never be the primary defense.
6. **Real-time alerting on remote access sessions is essential**: The operator detected the intrusion visually. An automated alert triggered by remote access from an unrecognized IP or outside business hours would have provided earlier detection and attribution data.
7. **The water sector faces unique security challenges**: Many water utilities are small, under-resourced, and lack dedicated cybersecurity staff. The Oldsmar incident accelerated regulatory efforts (EPA sanitary survey cybersecurity requirements, America's Water Infrastructure Act) to mandate baseline cybersecurity controls.

---

### References

1. CISA. (2021). *Compromise of U.S. Water Treatment Facility*. https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-042a
2. Massachusetts Water Resources Authority. (2021). *Official Incident Summary: Oldsmar Water Treatment Plant*. https://www.mwra.com/oldsmar-incident-report.pdf
3. ICS-CERT. (2021). *Advisory (ICSA-21-042-01): Oldsmar Water Treatment Facility Unauthorized Access*. https://www.cisa.gov/news-events/ics-advisories/icsa-21-042-01
4. Environmental Protection Agency. (2021). *Memorandum: Cybersecurity Best Practices for the Water Sector*. https://www.epa.gov/waterresilience/cybersecurity-best-practices-water-sector
5. US Senate Committee on Environment and Public Works. (2021). *Hearing on Cybersecurity Threats to Water Systems*. Testimony of Eric Goldstein, CISA.

---

*Case study version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
