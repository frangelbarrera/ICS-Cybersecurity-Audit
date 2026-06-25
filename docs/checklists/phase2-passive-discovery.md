# Phase 2: Passive Discovery and Baseline Checklist

## Purpose

This checklist guides the auditor through passive network traffic capture, asset discovery, protocol analysis, and baseline documentation. **All activities in this phase are strictly passive -- zero packets are sent to the control network.**

**Reference Standards**: ISA/IEC 62443-3-2 (Security Risk Assessment), NIST SP 800-82r3 Section 6.2 (Network Security)

---

## Safety Preamble

Before beginning any Phase 2 activity, confirm:

- [ ] Network TAP or SPAN port is configured correctly and verified in a lab environment
- [ ] Capture device has no IP address on the OT network (or uses a read-only mirror)
- [ ] Capture interface is in promiscuous mode only -- no ARP, no DHCP, no broadcast
- [ ] All capture device services that could generate traffic are disabled (IPv6 autoconfig, mDNS, LLMNR, NetBIOS)
- [ ] Safety officer is aware of monitoring deployment location

---

## 1. Network Traffic Capture

| # | Item | Status | Responsible | Notes | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 1.1 | Verify capture device NIC is configured with no IP address (or is in stealth/monitor mode) | [ ] | Auditor | Critical safety check -- re-verify at deployment | SR 5.1 |
| 1.2 | Deploy network TAP or configure SPAN/mirror port on OT switch | [ ] | Client OT Eng. + Auditor | SPAN: risk of dropped frames under load; TAP preferred for Level 1-2 | SR 5.1 |
| 1.3 | Verify SPAN port is configured as RX-only (ingress mirror) to prevent packet injection | [ ] | Auditor | Check switch configuration before connecting capture device | SR 5.1 |
| 1.4 | Start packet capture with appropriate snaplen (snaplen 0 for full packets, or 128 for headers-only baseline) | [ ] | Auditor | `tcpdump -i eth0 -w baseline.pcap -s 0` | NIST 6.2.5 |
| 1.5 | Apply display filters to isolate industrial protocols: Modbus TCP (port 502), S7Comm (port 102), EtherNet/IP (ports 44818, 2222), OPC UA (port 4840), PROFINET (ethertype 0x8892), BACnet (UDP 47808), DNP3 (port 20000) | [ ] | Auditor | Wireshark: `modbus or s7comm or cip or opcua or pn_rt or bacnet or dnp3` | NIST 6.2.5 |
| 1.6 | Verify no outbound packets are detected from capture device during first 10 minutes of capture | [ ] | Auditor | Review capture with filter: `eth.src == <capture MAC>` -- must return zero packets | SR 5.1 |
| 1.7 | Ensure capture storage has sufficient capacity for full engagement duration (estimate: 500 MB/hour per 100 Mbps of OT traffic) | [ ] | Auditor | Verify disk space before starting; configure ring buffer if needed | NIST 6.2.5 |

---

## 2. Asset Discovery (Passive)

| # | Item | Status | Responsible | Notes | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 2.1 | Extract unique MAC addresses from capture and perform OUI lookup to identify device manufacturers | [ ] | Auditor | `tshark -r capture.pcap -T fields -e eth.src | sort -u` | NIST 6.2.2 |
| 2.2 | Identify PLCs by MAC OUI and protocol signatures (Siemens = 00:1B:1B, Rockwell = 00:00:BC, Schneider = 00:80:F4) | [ ] | Auditor | Cross-reference OUI database with known industrial vendor prefixes | SR 2.8 |
| 2.3 | Identify HMIs and engineering workstations by OS fingerprinting from traffic patterns (TCP stack, SMB, RDP) | [ ] | Auditor | Passive OS fingerprinting via p0f or Zeek | NIST 6.2.2 |
| 2.4 | Identify managed switches via SNMP, CDP, or LLDP traffic (if present in capture) | [ ] | Auditor | Filter: `cdp or lldp or snmp` | NIST 6.2.6 |
| 2.5 | Detect network printers, VoIP phones, and other non-OT devices on OT network segments | [ ] | Auditor | Flag for removal -- non-OT devices on control network are a finding | SR 5.1 |
| 2.6 | Compare passive discovery results against client-provided asset inventory -- flag any unknown devices | [ ] | Auditor | Unknown devices = potential shadow IT or unauthorized access | SR 2.8 |
| 2.7 | Use NetworkMiner or GrassMarlin for automated passive asset identification and metadata extraction | [ ] | Auditor | NetworkMiner: File > Open PCAP; GrassMarlin: `python grassmarlin.py -f capture.pcap` | NIST 6.2.2 |

---

## 3. Protocol Analysis

| # | Item | Status | Responsible | Notes | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 3.1 | Identify all OT protocols present on the network -- map each to Purdue level | [ ] | Auditor | Protocols expected at Level 1 may be anomalous at Level 3 | SR 3.1 |
| 3.2 | Analyze Modbus TCP traffic: identify master-slave relationships, function codes in use, register ranges accessed | [ ] | Auditor | Wireshark Statistics > Protocol Hierarchy; filter: `modbus` | SR 3.1 |
| 3.3 | Analyze S7Comm traffic: identify active connections, job types (read/write/upload/download), and firmware version strings | [ ] | Auditor | S7Comm Plus (S7-1200/1500) uses TLS -- verify if encryption is enabled | SR 3.1 |
| 3.4 | Analyze EtherNet/IP traffic: enumerate CIP class/instance/attribute requests, identify implicit (I/O) vs explicit messaging | [ ] | Auditor | Implicit = UDP port 2222 (real-time I/O); Explicit = TCP 44818 (config) | SR 3.1 |
| 3.5 | Map all active communication sessions between devices (src IP, dst IP, protocol, frequency, data volume) | [ ] | Auditor | Zeek `conn.log` provides comprehensive session tracking | NIST 6.2.5 |
| 3.6 | Identify communications that occur outside normal business hours or at unexpected frequencies | [ ] | Auditor | Compare against client-provided communication schedules | SR 2.8 |
| 3.7 | Flag any use of insecure protocol versions (Modbus TCP without wrappers, S7Comm without access protection, unauthenticated OPC UA) | [ ] | Auditor | These become Phase 3 hardening findings | SR 3.1 |

---

## 4. Baseline Documentation

| # | Item | Status | Responsible | Notes | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 4.1 | Document network topology inferred from traffic flows (which devices communicate with which) | [ ] | Auditor | GrassMarlin auto-generates topology diagrams from PCAP | NIST 6.2.6 |
| 4.2 | Create traffic profile baseline: protocols, typical packet rates, bandwidth utilization per segment, peak vs average | [ ] | Auditor | Wireshark Statistics > IO Graph; save as reference for anomaly detection | NIST 6.2.5 |
| 4.3 | Document all active TCP and UDP ports observed -- compare against expected port list from client | [ ] | Auditor | Unexpected open ports = Phase 4 testing target | SR 7.1 |
| 4.4 | Capture and document ARP table state for each subnet (passive ARP cache inspection only) | [ ] | Auditor | `arp -a` on engineering workstation (with client permission) or from PCAP | NIST 6.2.2 |
| 4.5 | Archive raw PCAP files with cryptographic hash for chain of custody (SHA-256) | [ ] | Auditor | `sha256sum capture.pcap > capture.pcap.sha256` | SR 2.8 |

---

## 5. Safety Verification

| # | Item | Status | Responsible | Notes | Reference |
| :---: | :--- | :---: | :--- | :--- | :--- |
| 5.1 | Verify zero packets were sent to any OT device during the entire capture period | [ ] | Auditor | Search capture for any frame with capture device MAC as source | SR 5.1 |
| 5.2 | Verify capture did not introduce latency or packet loss on the OT network (SPAN port overload check) | [ ] | Client OT Eng. | Monitor switch CPU and SPAN port utilization during capture | SR 5.1 |
| 5.3 | Verify no ARP, DHCP, ICMP, NetBIOS, LLMNR, mDNS, or IPv6 neighbor discovery from capture device | [ ] | Auditor | Filter: `arp or dhcp or icmp or nbns or llmnr or mdns or icmp6` with capture MAC as source | SR 5.1 |
| 5.4 | Confirm all capture equipment can be removed from the OT network without service disruption | [ ] | Auditor + Client | Removal procedure documented and tested in advance | SR 5.1 |
| 5.5 | Verify PCAP files are encrypted at rest on capture device (full disk encryption or file-level encryption) | [ ] | Auditor | PCAPs may contain sensitive operational data -- protect accordingly | SR 4.1 |

---

## Phase 2 Completion Sign-Off

| Field | Details |
| :--- | :--- |
| **All capture activities verified passive (zero packets sent to OT)** | [ ] Yes [ ] No |
| **Asset inventory compared against passive discovery results** | [ ] Yes [ ] No -- list discrepancies below |
| **Protocol map and traffic baseline documented** | [ ] Yes [ ] No |
| **Raw PCAP files archived with SHA-256 hashes** | [ ] Yes [ ] No |
| **Ready to proceed to Phase 3 (Configuration and Hardening Review)** | [ ] Yes [ ] No |
| **Auditor Name / Signature** | |
| **Client Representative Name / Signature** | |
| **Date** | |

**Discrepancies and Notes:**

[Document unknown devices, unexpected protocols, anomalous traffic patterns, or any other observations that require investigation in subsequent phases]

---

*Checklist version: 1.0 | Last reviewed: June 2026 | [ICS-Cybersecurity-Audit](https://github.com/frangelbarrera/ICS-Cybersecurity-Audit)*
