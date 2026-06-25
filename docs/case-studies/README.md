# ICS/OT Incident Case Studies

## Learning from Real-World Attacks on Industrial Control Systems

### Purpose

This directory contains detailed analyses of major ICS/OT cyber incidents. Each case study examines the attack through the lens of the [MITRE ATT&CK for ICS framework](../mitre-attack-ics-mapping.md) and maps how the [5-phase audit methodology](../index.md) would have detected or prevented the attack.

Studying real incidents is essential for OT security practitioners because:

- **Attack patterns repeat**: The same techniques (default credentials, missing segmentation, unpatched HMIs) appear in incident after incident.
- **Consequences are real**: These are not theoretical exercises -- each case study describes actual operational, safety, or financial impacts.
- **Defenses can be tested**: Each case study identifies specific Phase 2-4 audit activities that would have caught the attack before it succeeded.
- **Standards matter**: Every incident maps to specific IEC 62443 Security Requirement failures -- showing why compliance is not just paperwork.

### How to Use These Case Studies

1. **During an audit**: Reference relevant case studies when communicating risk to clients. "This is how attackers exploited the exact same vulnerability at [Company X]."
2. **For training**: Use the ATT&CK technique walkthroughs to train OT engineers and operators on real attack paths.
3. **For gap analysis**: Compare your environment against each case study's IEC 62443 failures. Are you vulnerable to the same techniques?
4. **For executive communication**: Case studies with real financial and operational impacts are more persuasive than CVSS scores alone.

### Index

| Incident | Year | Primary Sector | ATT&CK Tactics Demonstrated | Key Lesson |
| :--- | :---: | :--- | :--- | :--- |
| [Stuxnet](stuxnet-2010.md) | 2010 | Nuclear (Centrifuge Enrichment) | Initial Access, Execution, Persistence, Evasion, Impair Process Control | Air-gapped networks can be bridged; supply chain and removable media are powerful attack vectors |
| [Ukraine Power Grid](ukraine-power-grid-2015.md) | 2015 | Electric Utilities | Initial Access, Discovery, Lateral Movement, Collection, Inhibit Response Function | Coordinated multi-stage attacks can cause widespread physical disruption; SCADA takeover is achievable via IT compromise |
| [TRITON/TRISIS](triton-trisis-2017.md) | 2017 | Petrochemical | Persistence, Impair Process Control, Inhibit Response Function | Safety instrumented systems are not immune; SIS compromise can have catastrophic safety consequences |
| [Colonial Pipeline](colonial-pipeline-2021.md) | 2021 | Oil & Gas Pipeline | Initial Access, Impact | IT/OT convergence means IT ransomware can shut down OT; proactive shutdown is a valid defensive measure |
| [Oldsmar Water Treatment](oldsmar-water-2021.md) | 2021 | Water/Wastewater | Initial Access, Impair Process Control | Remote access without MFA is a direct threat to public safety; operator vigilance is the last line of defense |

### Incident Timeline

```
2010                 2015                 2017                 2021
  |                    |                    |                    |
Stuxnet           Ukraine Grid        TRITON/TRISIS      Colonial Pipeline
(Discovered)      (Dec 23)            (Discovered)       Oldsmar Water
                  225K customers      SIS-targeted       (Feb/May)
                  without power       malware            IT-to-OT cascade
```

---

*Index version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
