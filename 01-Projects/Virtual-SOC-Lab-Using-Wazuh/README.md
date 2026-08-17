# 🛡️ Enterprise-Style Virtual SOC with Wazuh

A hands-on virtual Security Operations Center (SOC) environment built to practice security monitoring, log analysis, threat detection, alert triage, and incident investigation.

The lab simulates a small enterprise security environment using virtual machines and security tools. Kali Linux is used to generate controlled
security events, pfSense provides network segmentation and firewall capabilities, Windows 10 acts as a monitored endpoint, and Ubuntu Server hosts the Wazuh Manager.

---

## 🎯 Project Objective

The objective of this project is to build a controlled SOC environment that allows me to practice the activities performed by a Junior SOC Analyst.

The lab focuses on:

- Security monitoring
- SIEM operations
- Log collection and analysis
- Alert triage
- Endpoint monitoring
- Network security monitoring
- Attack simulation
- Detection engineering
- IOC investigation
- MITRE ATT&CK mapping
- Incident investigation
- Security documentation

---

## 🏗️ Architecture

The lab is built using VMware Workstation 17 Pro and consists of separate WAN and LAN networks.

```text
                           Internet
                              │
                              ▼
                     ┌─────────────────┐
                     │ VMware vmnet8    │
                     │ NAT / WAN        │
                     │ 172.16.10.0/24   │
                     └────────┬────────┘
                              │
               ┌──────────────┴──────────────┐
               │                             │
               ▼                             ▼
       ┌───────────────┐             ┌───────────────┐
       │   Kali Linux  │             │    pfSense    │
       │   Attacker    │             │   Firewall    │
       │ 172.16.10.130 │             │ WAN: .128     │
       └───────────────┘             └───────┬───────┘
                                             │
                                             │
                              ┌──────────────┴──────────────┐
                              │ VMware vmnet2               │
                              │ Host-only / Internal LAN    │
                              │ 192.168.10.0/24             │
                              └──────────────┬──────────────┘
                                             │
                         ┌───────────────────┴──────────────────┐
                         │                                      │
                         ▼                                      ▼
                ┌─────────────────┐                    ┌─────────────────┐
                │    Windows 10   │                    │ Ubuntu Server   │
                │    Victim       │                    │ Wazuh Manager  │
                │ 192.168.10.100  │                    │ 192.168.10.101 │
                │  Wazuh Agent    │                    │                 │
                └─────────────────┘                    └─────────────────┘
