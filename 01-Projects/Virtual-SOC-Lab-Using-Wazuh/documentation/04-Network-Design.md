# Network Design

## 1. Overview

Network segmentation is a fundamental component of the Virtual SOC Home Lab.

The environment separates the external attacker network from the protected internal network using **pfSense** as the routing and firewall boundary.

This design allows controlled security activity to originate from the external network while protecting the internal systems and providing opportunities to observe, log, and investigate network activity.

---

# 2. Network Topology

```text
                    EXTERNAL / WAN
                    172.16.10.0/24
                           │
                           │
                    ┌──────▼──────┐
                    │ Kali Linux  │
                    │  Attacker   │
                    └──────┬──────┘
                           │
                           │
                    ┌──────▼──────┐
                    │   pfSense   │
                    │             │
                    │ WAN + LAN    │
                    └──────┬──────┘
                           │
                           │
                    PROTECTED LAN
                    192.168.10.0/24
                           │
              ┌────────────┴────────────┐
              │                         │
       ┌──────▼───────┐         ┌───────▼────────┐
       │   Windows 10 │         │ Ubuntu Server  │
       │              │         │                │
       │ Wazuh Agent  │         │ Wazuh Manager  │
       │ Sysmon       │         │     / SIEM     │
       └──────────────┘         └────────────────┘
```

---

# 3. Network Segments

| Network Segment | CIDR              | Purpose                           |
| --------------- | ----------------- | --------------------------------- |
| WAN / External  | `172.16.10.0/24`  | External or attacker-side network |
| LAN / Internal  | `192.168.10.0/24` | Protected monitoring environment  |

The two networks are intentionally separated to establish a clear security boundary.

---

# 4. WAN Network

The WAN network represents the external side of the environment.

Kali Linux is connected to this network and is used to generate controlled activity.

From a security monitoring perspective, this network represents a source from which potentially untrusted traffic may originate.

Typical activity generated from this segment may include:

* Network discovery
* Port scanning
* Connection attempts
* Other controlled security testing

All activity must remain within the authorized laboratory environment.

---

# 5. LAN Network

The LAN network represents the protected internal environment.

The primary systems include:

* Windows 10
* Ubuntu Server
* Wazuh monitoring infrastructure

The internal network is protected by pfSense and is intentionally separated from the external network.

---

# 6. pfSense as the Security Boundary

pfSense performs several critical network functions:

* Routing between network segments
* Firewall enforcement
* Network traffic filtering
* Security event logging
* Segmentation between external and internal networks

The firewall therefore represents an important point of visibility within the SOC architecture.

---

# 7. Network Security Flow

Network traffic follows the general path:

```text
Kali Linux
    │
    │ Traffic
    ▼
pfSense WAN
    │
    │ Firewall Processing
    ▼
pfSense LAN
    │
    ▼
Protected Network
    │
    ├── Windows 10
    │
    └── Ubuntu / Wazuh
```

The exact behavior of traffic depends on the configured firewall policies and routing.

---

# 8. Network Telemetry

The network architecture supports multiple sources of network-related telemetry.

### pfSense

Provides visibility into firewall activity and network connection decisions.

### Suricata

Provides network intrusion detection telemetry based on observed traffic and configured detection rules.

### Wazuh

Provides centralized visibility into security data that has been successfully integrated into the monitoring platform.

---

# 9. Why Segmentation Matters

Segmentation provides several security benefits within the laboratory.

### Isolation

The protected environment is separated from the external attacker system.

### Controlled Testing

Security activity can be generated without intentionally targeting external systems.

### Visibility

Traffic crossing the security boundary provides opportunities for observation and detection.

### Investigation

The separation makes it easier to establish relationships between source and destination systems.

---

# 10. Network Design Considerations

The network was designed with simplicity and observability in mind.

A small number of networks makes the environment easier to understand and troubleshoot while still demonstrating important enterprise security concepts.

The design also establishes clear roles:

```text
External Zone
     ↓
Attacker / Traffic Generation
     ↓
Security Boundary
     ↓
Protected Zone
     ↓
Monitored Systems
```

---

# 11. Validation

Network configuration should be validated before conducting security testing.

Recommended validation checks include:

* Confirming each system is connected to the correct virtual network.
* Verifying IP addressing.
* Confirming the correct default gateway.
* Testing connectivity between permitted systems.
* Confirming firewall policies behave as intended.
* Confirming relevant traffic is visible to monitoring controls.

Actual IP addresses and test results should be documented using evidence collected from the laboratory.

---

# 12. Summary

The network design establishes a controlled environment in which external activity can be generated and monitored against a protected internal network.

The use of separate WAN and LAN segments, combined with pfSense firewall enforcement and security monitoring, provides the foundation for the project's SOC detection and investigation workflows.
