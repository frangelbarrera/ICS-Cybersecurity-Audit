# Vendor Security Advisory Index

## ICS/OT Vendor Security Resources

This directory indexes official security advisory portals and hardening guides for the major industrial control system vendors referenced in the ICS-Cybersecurity-Audit framework. Use these resources to track vulnerabilities, firmware updates, and security best practices for your OT assets.

---

### Tier 1: Control System Vendors

#### Siemens

| Resource | URL | Description |
| :--- | :--- | :--- |
| Siemens ProductCERT | https://www.siemens.com/cert | Central security advisory portal. Covers all Siemens industrial products: SIMATIC, SINUMERIK, SCALANCE, etc. Note: may be geo-restricted in some regions. |
| Siemens Industrial Security | https://www.siemens.com/global/en/products/automation/topic-areas/industrial-security.html | Industrial security concepts, whitepapers, and configuration guides |
| S7-1200/S7-1500 Security Guide | Refer to TIA Portal documentation | Access protection, know-how protection, firmware signing, and certificate management |

#### Rockwell Automation (Allen-Bradley)

| Resource | URL | Description |
| :--- | :--- | :--- |
| Security Advisories | https://www.rockwellautomation.com/en-us/trust/security-advisories.html | Official security advisories for ControlLogix, CompactLogix, FactoryTalk, and Stratix products |
| Knowledgebase (requires login) | https://rockwellautomation.custhelp.com/ | Technical knowledgebase including security configuration guides and patch information |
| Industrial Security | https://www.rockwellautomation.com/en-us/capabilities/industrial-security.html | CIP Security, FactoryTalk security, network segmentation guidance |

#### Schneider Electric

| Resource | URL | Description |
| :--- | :--- | :--- |
| Cybersecurity Support | https://www.se.com/ww/en/work/support/cybersecurity/ | Security advisories, vulnerability notifications, and cybersecurity best practices |
| EcoStruxure Security | Refer to Schneider Electric documentation portal | Modicon M340/M580, EcoStruxure Control Expert security configuration |

---

### Tier 2: Specialized OT Vendors

#### Emerson / GE / Honeywell

| Resource | URL | Description |
| :--- | :--- | :--- |
| Emerson Cybersecurity | https://www.emerson.com/en-us/automation/cybersecurity | DeltaV and Ovation DCS security resources |
| GE Vernova (Grid Solutions) | https://www.gevernova.com/grid-solutions/ | Protection relays, RTUs, and substation automation |
| Honeywell Process Solutions | https://process.honeywell.com/us/en/cybersecurity | Experion PKS and Safety Manager security advisories. Note: may be geo-restricted in some regions. |

#### Yokogawa / ABB / Mitsubishi Electric

| Resource | URL | Description |
| :--- | :--- | :--- |
| Yokogawa Security Advisories | https://www.yokogawa.com/solutions/solutions/security/ | CENTUM DCS and FA-M3 controller security |
| ABB Cybersecurity | https://global.abb/group/en/technology/cyber-security | ABB Ability, 800xA DCS, and AC500 PLC security |
| Mitsubishi Electric FA Security | https://www.mitsubishielectric.com/fa/support/security/ | MELSEC PLC and iQ Platform security advisories |

---

### Government and Industry Bodies

| Resource | URL | Description |
| :--- | :--- | :--- |
| **CISA ICS-CERT** | https://www.cisa.gov/ics | U.S. Cybersecurity and Infrastructure Security Agency -- ICS advisories, alerts, and best practices |
| **CISA Known Exploited Vulnerabilities (KEV)** | https://www.cisa.gov/known-exploited-vulnerabilities-catalog | Catalog of vulnerabilities known to be actively exploited, including OT/ICS entries |
| **ISA Global Cybersecurity Alliance (ISAGCA)** | https://www.isa.org/ | ISA/IEC 62443 standards, training, and certification programs |
| **MITRE ATT&CK for ICS** | https://attack.mitre.org/matrices/ics/ | Adversary tactics, techniques, and procedures targeting industrial control systems |
| **ENISA OT Security** | https://www.enisa.europa.eu/topics/ics-security | European Union Agency for Cybersecurity -- OT/ICS good practices and threat landscape |

---

### Threat Intelligence Sources

| Resource | URL | Description |
| :--- | :--- | :--- |
| **Dragos** | https://www.dragos.com/ | OT/ICS-focused threat intelligence, incident response, and research |
| **Nozomi Networks Labs** | https://www.nozominetworks.com/labs/ | OT/IoT threat research, protocol analysis, and vulnerability disclosures |
| **Claroty Team82** | https://claroty.com/team82/ | OT/ICS vulnerability research and responsible disclosure |
| **OTORIO Research** | https://www.otorio.com/resources/research/ | OT security research, threat reports, and protocol analysis |
| **Mandiant (Google Cloud)** | https://www.mandiant.com/ | ICS-focused threat intelligence and incident response (now part of Google Cloud) |

---

### How to Use This Index

1. **During an audit**: Cross-reference the firmware versions found in your asset inventory against each vendor's security advisory list to identify known vulnerabilities.
2. **For ongoing monitoring**: Subscribe to vendor RSS feeds or mailing lists where available. Check CISA ICS-CERT weekly for new advisories affecting your environment.
3. **For hardening**: Use vendor-specific security configuration guides (linked above) to validate that each asset is configured according to the vendor's recommended security baseline.

---

### URL Verification Notes

- **Siemens ProductCERT**: May enforce geo-IP restrictions. If inaccessible, try from a VPN with a European or North American exit node, or access via the Siemens Industry Online Support portal.
- **Rockwell Automation Knowledgebase**: Requires a valid TechConnect support contract for full access. Public advisories are available without login.
- **Schneider Electric**: May redirect based on geographic region. The `ww` (worldwide) URL should provide the most consistent access.

---

*Index version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
