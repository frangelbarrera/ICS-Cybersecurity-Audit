# Tools Directory

## Purpose

This directory contains tool configurations, scripts, and references that support the ICS-Cybersecurity-Audit framework. In future releases, this will expand to include ready-to-use profiles, configuration templates, and automation scripts for OT security assessments.

---

### Current Contents

This directory is under active development. The following materials are planned for inclusion:

#### Wireshark and Network Analysis Profiles

- **OT Protocol Dissector Profiles**: Pre-configured Wireshark profiles optimized for industrial protocol analysis, including:
  - Modbus TCP (port 502) -- Function code and register-level decoding
  - S7Comm / S7Comm-Plus (port 102) -- Siemens PLC communication analysis
  - EtherNet/IP and CIP (ports 44818, 2222) -- Implicit and explicit messaging
  - PROFINET (EtherType 0x8892) -- RT and IRT frame analysis
  - BACnet/IP (UDP port 47808) -- Building automation protocol inspection
  - DNP3 (TCP/UDP port 20000) -- SCADA protocol with secure authentication
  - OPC UA (TCP port 4840) -- Certificate exchange and session analysis
  - IEC 61850 MMS/GOOSE/SV -- Substation automation protocol analysis

#### Asset Integrity Verification

- **PLC Project Hash Verifier**: Educational Python script demonstrating the concept of project file integrity verification before controller download. Reference implementation aligning with the Phase 3 checklist.
- **Firmware Version Checker**: Script template for automated firmware version collection and comparison against vendor advisory databases (read-only, offline use).

#### Network Baseline Tools

- **Passive Asset Discovery Script**: Guidance for using NetworkMiner, GrassMarlin, and Zeek for passive OT asset identification.
- **Traffic Baseline Templates**: Reference PCAP filter expressions for capturing baseline OT traffic without generating any packets on the control network.

#### Configuration Audit Scripts

- **Offline Project File Analyzer**: Script template for searching TIA Portal, Studio 5000, and EcoStruxure Control Expert project files for common security misconfigurations (e.g., default credentials, weak protection settings). Operates on exported/backup project files only.
- **Firewall Rule Auditor**: Reference methodology for auditing industrial firewall rule sets against the principle of least privilege for OT protocols.

---

### Tool Categories Referenced in the Framework

The following third-party tools are referenced throughout the framework. Links are provided in the main [README.md](../../README.md). This directory will contain companion configurations and integration guidance:

| Category | Tools | Companion Content Planned |
| :--- | :--- | :--- |
| **Passive Discovery** | NetworkMiner, GrassMarlin | Deployment guides, filter configurations |
| **Traffic Analysis** | Wireshark, Zeek/Brim | Protocol dissector profiles, Zeek scripts for OT protocols |
| **Vulnerability Management** | OpenVAS, CISA CSET | OT-tuned scan configurations, compliance assessment templates |
| **PLC Analysis** | Snap7, ISF | Safe-mode configuration guides emphasizing read-only operations |

---

### Safety Notice

All tools and scripts provided in this directory are intended for **defensive security assessment only**:

- **Never** execute scripts against live production controllers without explicit written authorization during approved maintenance windows.
- **Never** use any tool to modify process variables, logic, or configurations on operational systems.
- **Always** test scripts in an offline lab environment with replica hardware before any field deployment.
- **Always** maintain the ability to immediately disconnect from the OT network if unexpected behavior is observed.

The scripts and configurations provided here are educational reference implementations. They should be reviewed, tested, and customized for each specific engagement by qualified OT security professionals.

---

### Contribution Guidelines for Tools

If you would like to contribute a tool, script, or configuration to this directory:

1. Ensure it aligns with the defensive-only philosophy of this framework.
2. Include clear comments and safety warnings in the code.
3. Provide a README or header documentation explaining usage, prerequisites, and limitations.
4. Test against offline/replica hardware before submission.
5. Submit via Pull Request following the [CONTRIBUTING.md](../../CONTRIBUTING.md) process.

No tool should be capable of causing harm to a production system when used as documented.

---

### Roadmap

| Release | Planned Additions |
| :--- | :--- |
| v1.1 (Q3 2026) | Wireshark OT protocol profiles, asset integrity verification script (Python reference) |
| v2.0 (Q1 2027) | Automation scripts for asset inventory collection, incident response playbook templates, vendor hardening configuration checkers |

---

*Directory version: 1.0 | Created: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
