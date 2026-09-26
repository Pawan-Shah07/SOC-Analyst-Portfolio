# Architecture

## 1. Overview

The Virtual SOC Home Lab is designed as a segmented security monitoring environment that separates untrusted external activity from protected internal systems.

The architecture uses **pfSense** as the primary network security boundary between the external WAN segment and the protected LAN. **Kali Linux** is positioned on the external network and represents a controlled attacker system used to generate security activity.

The protected network contains the monitored **Windows 10 endpoint** and the **Ubuntu Server** hosting the Wazuh Manager/SIEM infrastructure.

The monitoring architecture combines network-based and endpoint-based telemetry:

* **pfSense** provides firewall and network security events.
* **Suricata** provides network intrusion detection telemetry.
* **Windows Security Logs** provide native endpoint security events.
* **Sysmon** provides enhanced Windows endpoint telemetry.
* **Wazuh Agent** forwards endpoint telemetry.
* **Wazuh Manager** centralizes and analyzes security events.
* **Wazuh Dashboard** provides visibility for monitoring and investigation.

---

# 2. High-Level Architecture

```text
                         EXTERNAL / WAN
                         172.16.10.0/24
                                │
                                │
                        ┌───────▼───────┐
                        │   Kali Linux  │
                        │    Attacker   │
                        └───────┬───────┘
                                │
                                │ Controlled
                                │ Security Activity
                                ▼
                     ┌────────────────────┐
                     │       pfSense      │
                     │ Firewall / Router  │
                     └─────────┬──────────┘
                               │
                               │
                        PROTECTED LAN
                        192.168.10.0/24
                               │
                ┌──────────────┴──────────────┐
                │                             │
        ┌───────▼────────┐            ┌───────▼────────┐
        │   Windows 10   │            │ Ubuntu Server  │
        │                │            │                │
        │ Wazuh Agent    │            │ Wazuh Manager  │
        │ Sysmon         │            │     / SIEM     │
        └────────────────┘            └───────┬────────┘
                                               │
                                               ▼
                                      ┌─────────────────┐
                                      │ Wazuh Dashboard │
                                      │ Monitoring &    │
                                      │ Investigation   │
                                      └─────────────────┘
```

---

# 3. Security Zones

The architecture is divided into two primary security zones.

## 3.1 External WAN Zone

**Network:** `172.16.10.0/24`

This network represents the external or untrusted portion of the environment.

Kali Linux is placed within this segment and is used to generate controlled security activity.

The purpose of this zone is to simulate activity originating from outside the protected environment.

---

## 3.2 Protected LAN Zone

**Network:** `192.168.10.0/24`

The internal LAN contains the systems that require monitoring and protection.

The primary systems within this network are:

* Windows 10 monitored endpoint
* Ubuntu Server hosting Wazuh infrastructure

The protected network is separated from the external network by pfSense.

---

# 4. Component Responsibilities

| Component                 | Primary Responsibility     | Security Function                            |
| ------------------------- | -------------------------- | -------------------------------------------- |
| VMware Workstation 17 Pro | Virtualization             | Provides isolated virtual infrastructure     |
| Kali Linux                | Controlled attack activity | Generates security events                    |
| pfSense                   | Firewall and routing       | Network segmentation and traffic enforcement |
| Suricata                  | Network IDS                | Network threat detection                     |
| Windows 10                | Monitored endpoint         | Endpoint security telemetry                  |
| Wazuh Agent               | Telemetry collection       | Endpoint log forwarding                      |
| Sysmon                    | Endpoint monitoring        | Detailed Windows activity visibility         |
| Ubuntu Server             | SIEM infrastructure        | Hosts Wazuh Manager                          |
| Wazuh Manager             | Security monitoring        | Centralized event processing                 |
| Wazuh Dashboard           | Visualization              | Alert monitoring and investigation           |

---

# 5. Trust Boundaries

The most important trust boundary in the environment is the boundary between the external WAN and protected LAN.

```text
UNTRUSTED / EXTERNAL
        │
        │
        ▼
┌─────────────────┐
│     pfSense     │
│ Trust Boundary  │
└────────┬────────┘
         │
         ▼
PROTECTED / INTERNAL
         │
   ┌─────┴─────┐
   │           │
Windows      Ubuntu
Endpoint     Wazuh
```

The boundary allows network activity to be observed and controlled before reaching protected systems.

From a SOC perspective, this boundary is important because it provides a location where network activity can be:

* Observed
* Logged
* Filtered
* Detected
* Investigated

---

# 6. Telemetry Architecture

The laboratory uses multiple telemetry sources to provide visibility across network and endpoint layers.

```text
                  SECURITY ACTIVITY
                         │
           ┌─────────────┼─────────────┐
           │             │             │
           ▼             ▼             ▼
       pfSense        Suricata       Windows
       Firewall          IDS         Endpoint
           │             │             │
           │             │       ┌─────┴─────┐
           │             │       │           │
           │             │    Security     Sysmon
           │             │      Logs        Events
           │             │       │           │
           └─────────────┴───────┴───────────┘
                                   │
                                   ▼
                           Wazuh Manager
                                   │
                                   ▼
                             Wazuh Alert
                                   │
                                   ▼
                            SOC Investigation
```

Each telemetry source provides a different perspective of the same environment.

This layered visibility is important because an event that appears ambiguous in one log source may become clearer when correlated with another source.

---

# 7. Data Flow

The architecture follows this general data flow:

1. Controlled activity is generated.
2. Network controls observe the activity.
3. Firewall and IDS components generate relevant telemetry.
4. Endpoint systems generate security events.
5. Wazuh Agent collects endpoint telemetry.
6. Telemetry is forwarded to Wazuh Manager.
7. Wazuh processes and evaluates events.
8. Security alerts become available for analyst review.
9. The analyst investigates the activity using available evidence.

---

# 8. Architectural Security Principles

The design demonstrates several fundamental security principles.

### Segmentation

External and internal systems are placed into separate network segments.

### Defense in Depth

Multiple security controls provide visibility at different layers.

### Centralized Monitoring

Security telemetry is centralized within the SIEM.

### Evidence-Based Investigation

Security conclusions should be supported by observable telemetry.

### Controlled Testing

Security activity is generated within an isolated laboratory rather than against unauthorized systems.

---

# 9. Architectural Considerations

This architecture is intentionally designed for learning and demonstration.

It does not attempt to reproduce:

* Enterprise-scale infrastructure
* High-availability SIEM architecture
* Large endpoint deployments
* Production traffic volumes
* Enterprise identity infrastructure
* Full production SOC automation

The architecture should therefore be interpreted as a **small-scale SOC simulation environment**.

---

# 10. Summary

The architecture integrates network security, intrusion detection, endpoint monitoring, and centralized SIEM capabilities.

The resulting architecture demonstrates the relationship between:

**Security Activity → Telemetry → Detection → SIEM → Alert → Investigation**

This provides a practical foundation for developing SOC analyst and Blue Team skills.
