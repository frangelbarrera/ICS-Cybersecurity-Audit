# Case Study: Ukraine Power Grid Attack (2015)

## The First Confirmed Cyber-Attack to Cause a Power Outage

---

### Executive Summary

**What happened**: On December 23, 2015, attackers executed a coordinated cyber-attack against three Ukrainian regional electric power distribution companies (Prykarpattyaoblenergo, Kyivoblenergo, and Chernivtsioblenergo), causing a power outage affecting approximately 225,000 customers. The attack involved multiple stages: spearphishing to gain initial access, network reconnaissance, credential theft, SCADA system takeover, and a coordinated series of circuit breaker openings. The attackers also deployed KillDisk malware to destroy files on operator workstations and disable the UPS systems at two facilities, delaying restoration efforts.

**When**: December 23, 2015; power was out for 1-6 hours across the affected regions. Restoration required manual operation of substations because SCADA systems were rendered inoperable.

**Impact**: 225,000 customers lost power for 1-6 hours. 30 substations were taken offline. Control center SCADA systems were rendered inoperable for months due to KillDisk destruction. The attack demonstrated that a nation-state actor could cause physical disruption through cyber means alone.

**Attribution**: The US Department of Homeland Security and Ukrainian authorities attributed the attack to the Russian state-sponsored threat group "Sandworm" (also known as Voodoo Bear, APT28-adjacent). The group used BlackEnergy3 malware, a variant previously observed in other attacks against Ukrainian infrastructure.

---

### ATT&CK for ICS Techniques Used

| Technique ID | Technique Name | How It Was Used |
| :---: | :--- | :--- |
| T0865 | Spearphishing Attachment | Initial infection via spearphishing emails containing a malicious Microsoft Office document with BlackEnergy3 macro |
| T0859 | Valid Accounts | Attackers harvested VPN credentials and Active Directory credentials to access the OT network |
| T0822 | External Remote Services | Used legitimate VPN access to connect to the control center network from the internet |
| T0840 | Network Connection Enumeration | Conducted extensive network discovery to map the OT environment, identify SCADA servers, and locate substation RTUs |
| T0886 | Remote Services | Used remote desktop and remote administration tools to move laterally within the OT network |
| T0853 | Scripting | Used scripts to automate the opening of circuit breakers across multiple substations simultaneously |
| T0823 | Graphical User Interface | Directly interacted with SCADA HMI to open breakers, overriding normal operator controls |
| T0878 | Alarm Suppression | Disabled UPS systems at two facilities, preventing backup power from maintaining operations after grid power was cut |
| T0809 | Data Destruction | Deployed KillDisk malware to overwrite the master boot record (MBR) on operator workstations and SCADA servers, rendering them unbootable |
| T0816 | Device Restart/Shutdown | KillDisk caused workstations to crash and become unbootable, delaying restoration |
| T0836 | Modify Parameter | Modified setpoints and breaker states on RTUs and protection relays via the compromised SCADA |
| T0813 | Denial of Control | After opening breakers, attackers locked operators out of SCADA and destroyed workstations, denying operators the ability to remotely close breakers |

---

### IEC 62443-3-3 Security Requirement Failures

| Security Requirement | Failure Description |
| :--- | :--- |
| **SR 1.1 -- Identification and Authentication** | Shared operator credentials; no MFA on VPN access; Active Directory credentials not segregated between IT and OT |
| **SR 1.12 -- Multi-Factor Authentication** | VPN access to control center used single-factor authentication (username + password only) |
| **SR 2.1 -- Authorization** | Operators had excessive privileges -- attackers using operator credentials could open breakers at any substation |
| **SR 2.8 -- Auditable Events** | SCADA actions (breaker opening, setpoint changes) were logged but attackers had access to delete or manipulate logs |
| **SR 3.1 -- Communication Integrity** | Communications between control center and substations lacked integrity verification -- commands from a compromised HMI were indistinguishable from legitimate operator commands |
| **SR 4.1 -- Information Confidentiality** | UPS management interfaces were accessible from the control network without additional authentication |
| **SR 4.2 -- Physical Security** | UPS systems could be remotely disabled -- physical or logical isolation of power systems would have prevented this |
| **SR 5.1 -- Network Segmentation** | IT and OT networks were inadequately segmented; VPN access from IT provided direct path to SCADA |

---

### NIST SP 800-82 Control Failures

| Control Area | Failure Description |
| :--- | :--- |
| **Access Control (6.2.1)** | No MFA for remote access; shared credentials; excessive privileges for operator roles |
| **Network Segmentation (6.2.6)** | IT and OT networks not adequately isolated; VPN terminated too close to OT assets |
| **Audit and Accountability (6.3.3)** | Logs not sent to centralized, immutable storage; attackers could manipulate local logs |
| **System and Communications Protection (6.2.4)** | No integrity verification for commands sent between SCADA and substation devices |
| **Contingency Planning (6.5.1)** | No offline backup for SCADA systems; restoration required months of manual rebuild |

---

### Purdue Model Layer Affected

| Purdue Level | Impact |
| :---: | :--- |
| **Level 4 (Enterprise)** | Initial compromise point -- spearphishing emails reached corporate IT users |
| **Level 3.5 (Industrial DMZ)** | VPN access bridged IT to OT without adequate security controls |
| **Level 3 (Site Operations)** | SCADA servers compromised and destroyed; operator workstations rendered unbootable |
| **Level 2 (Area Supervision)** | HMIs and local control interfaces affected by credential theft and remote access |
| **Level 1 (Basic Control)** | RTUs and protection relays received unauthorized commands to open breakers |
| **Level 0 (Process)** | Circuit breakers physically opened, disconnecting power to 225,000 customers and 30 substations |

---

### How This Audit Framework Would Have Detected It

| Audit Phase | Detection Opportunity |
| :--- | :--- |
| **Phase 1 -- Documentation** | Asset inventory and network architecture review would have identified the IT-to-OT VPN path as a high-risk boundary lacking adequate controls |
| **Phase 2 -- Passive Discovery** | Baseline traffic analysis would have flagged: (a) unusual RDP and remote administration traffic from IT VPN subnet to SCADA, (b) anomalous SCADA commands outside normal operating hours, (c) sustained network discovery activity |
| **Phase 3 -- Hardening Review** | The following would have been findings: (a) No MFA on VPN access -- Critical, (b) Shared operator credentials on SCADA -- Critical, (c) No network segmentation between IT VPN and SCADA -- Critical, (d) UPS management accessible from control network -- High, (e) No immutable centralized logging -- High, (f) Excessive operator privileges -- High |
| **Phase 4 -- Controlled Validation** | Testing would have confirmed: (a) VPN access provides direct SCADA reachability, (b) Operator credentials can open breakers at any substation, (c) UPS management interface is accessible without additional authentication |
| **Phase 5 -- Reporting** | Overall risk rating would have been Critical across multiple domains: access control, segmentation, and incident response readiness |

---

### Key Lessons

1. **Remote access to OT must use MFA**: Single-factor VPN authentication was the critical failure that enabled the entire attack chain. MFA on all OT remote access is non-negotiable.
2. **IT compromise can cascade into OT**: The attackers started with a phishing email in the IT environment and pivoted to OT. Strong IT/OT segmentation with an Industrial DMZ and jump servers would have blocked lateral movement.
3. **SCADA systems need offline, tested backups**: The KillDisk destruction of SCADA workstations extended the outage from hours to months for full system restoration. Immutable, offline, regularly tested backups are essential.
4. **Operator credentials must be scoped and monitored**: The attackers used legitimate operator credentials to open breakers. Privileged access to critical control functions must be scoped by substation, role, and time.
5. **UPS and power systems need physical or logical isolation**: The attackers disabled UPS systems to delay recovery. UPS management interfaces must be on a physically or logically isolated management network, not the general control network.
6. **Centralized, immutable logging is essential for incident response**: Without logs forwarded to a secure, centralized location, forensic investigation and post-incident learning are severely limited.
7. **Two-person integrity for critical commands**: Requiring independent approval for opening multiple breakers simultaneously would have provided a procedural defense against automated or unauthorized mass operations.

---

### References

1. Electricity Information Sharing and Analysis Center (E-ISAC) & SANS Industrial Control Systems. (2016). *Analysis of the Cyber Attack on the Ukrainian Power Grid*. https://ics.sans.org/media/E-ISAC_SANS_Ukraine_DUC_5.pdf
2. ICS-CERT. (2016). *IR-ALERT-H-16-056-01: Cyber-Attack Against Ukrainian Critical Infrastructure*. https://www.cisa.gov/news-events/ics-alerts/ir-alert-h-16-056-01
3. Lee, R. M., Assante, M. J., & Conway, T. (2016). *Analysis of the Cyber Attack on the Ukrainian Power Grid*. SANS ICS Defense Use Case No. 5.
4. Dragos, Inc. (2017). *CRASHOVERRIDE: Analysis of the Malware Targeting Electric Grid Operations*. https://www.dragos.com/wp-content/uploads/CrashOverride-01.pdf
5. MITRE ATT&CK for ICS. *Ukraine 2015 Electric Grid Attack*. https://attack.mitre.org/campaigns/C0028/

---

*Case study version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
