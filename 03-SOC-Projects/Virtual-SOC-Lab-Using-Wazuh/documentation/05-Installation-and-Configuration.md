# Installation and Configuration

## 1. Overview

This document describes the installation and configuration approach used to build the Virtual SOC Home Lab.

The environment is deployed using **VMware Workstation 17 Pro** and consists of multiple virtual machines connected through separate virtual network segments.

The configuration process focuses on establishing:

1. Virtual infrastructure
2. Network segmentation
3. Firewall and routing
4. Endpoint monitoring
5. Network intrusion detection
6. Wazuh SIEM infrastructure
7. Security telemetry collection

> **Important:** Commands, IP addresses, screenshots, and configuration values should reflect the actual laboratory implementation. Placeholder values should not be presented as verified configuration.

---

# 2. Virtualization Platform

The laboratory uses VMware Workstation 17 Pro to host the virtual machines.

The virtualization layer provides:

* Isolated virtual machines
* Virtual network interfaces
* Separate network segments
* Controlled testing environment
* Snapshot and recovery capabilities

The laboratory is intentionally isolated to prevent controlled security testing from affecting unauthorized systems.

---

# 3. Virtual Machines

The environment contains the following primary virtual systems:

| System        | Purpose             |
| ------------- | ------------------- |
| Kali Linux    | Controlled attacker |
| pfSense       | Firewall and router |
| Windows 10    | Monitored endpoint  |
| Ubuntu Server | Wazuh Manager/SIEM  |

---

# 4. Virtual Network Configuration

Two logical network segments are configured:

| Virtual Network | Purpose                     | Address Space     |
| --------------- | --------------------------- | ----------------- |
| WAN             | External / attacker network | `172.16.10.0/24`  |
| LAN             | Protected internal network  | `192.168.10.0/24` |

The WAN network connects Kali Linux to the external side of pfSense.

The LAN network connects pfSense to the protected Windows and Ubuntu systems.

---

# 5. pfSense Installation

pfSense is deployed as the virtual firewall and router.

The virtual firewall is configured with two network interfaces:

```text
WAN Interface
     │
     └── 172.16.10.0/24

LAN Interface
     │
     └── 192.168.10.0/24
```

The interface configuration establishes the routing boundary between the two network segments.

---

# 6. Firewall Configuration

Firewall policies are configured to control traffic between the network zones.

The configuration should follow the principle of:

> **Allow only required traffic and explicitly control unnecessary traffic.**

Firewall configuration should be validated using controlled connectivity tests.

Relevant firewall events should also be confirmed in the pfSense logging interface.

---

# 7. Windows Endpoint Configuration

Windows 10 is deployed as the monitored endpoint.

The endpoint is connected to the protected LAN.

The monitoring stack consists of:

* Windows Security Event Logging
* Wazuh Agent
* Sysmon

The purpose of this configuration is to provide endpoint telemetry that can be centralized within Wazuh.

---

# 8. Sysmon Configuration

Sysmon is used to enhance Windows endpoint visibility.

It can provide detailed telemetry related to system activity, including process creation and other endpoint events depending on the configuration.

The Sysmon configuration should be selected based on the monitoring objectives of the laboratory.

The report should document:

* Installation procedure
* Configuration used
* Event channels monitored
* Important event types
* Validation evidence

---

# 9. Wazuh Agent Configuration

The Wazuh Agent is installed on the Windows endpoint.

Its primary function is to collect and forward relevant endpoint telemetry to the Wazuh Manager.

The configuration should identify:

* Wazuh Manager destination
* Monitored log sources
* Windows event channels
* Agent status
* Connectivity status

The agent should be validated before beginning security testing.

---

# 10. Ubuntu Server and Wazuh

Ubuntu Server hosts the Wazuh Manager/SIEM infrastructure.

The Wazuh deployment provides centralized security monitoring and analysis.

The deployment should be validated by confirming:

* Wazuh services are operational.
* The Windows endpoint is registered.
* The endpoint reports an active status.
* Security events are received.
* Events are visible within the monitoring interface.

---

# 11. Suricata Configuration

Suricata provides network intrusion detection capabilities.

The configuration process should identify:

* Monitored interface
* Detection rules
* Alert configuration
* Logging configuration
* Service status

After configuration, controlled network activity should be generated to validate whether Suricata observes and detects the expected activity.

---

# 12. pfSense Logging

Firewall logging provides network-level security evidence.

Relevant logs can contain information about:

* Source
* Destination
* Protocol
* Port
* Action
* Timestamp

These fields can be useful during security investigations.

---

# 13. Telemetry Validation

After configuring the individual components, telemetry should be validated in stages.

```text
Endpoint
   ↓
Wazuh Agent
   ↓
Wazuh Manager
   ↓
Wazuh Dashboard
```

Network monitoring can be validated separately:

```text
Controlled Traffic
       ↓
    pfSense
       ↓
   Suricata
       ↓
   Security Event
```

---

# 14. Configuration Validation Checklist

| Component     | Validation                          |
| ------------- | ----------------------------------- |
| VMware        | Virtual machines operational        |
| Network       | Correct virtual networks assigned   |
| pfSense       | WAN/LAN interfaces operational      |
| Firewall      | Expected traffic behavior confirmed |
| Windows       | Endpoint connected to LAN           |
| Sysmon        | Endpoint telemetry generated        |
| Wazuh Agent   | Agent connected to Manager          |
| Wazuh Manager | Security events received            |
| Suricata      | Monitoring interface operational    |
| Dashboard     | Alerts/events visible               |

---

# 15. Evidence Collection

Screenshots should be captured during important configuration and validation stages.

Recommended evidence includes:

* VMware virtual network configuration
* pfSense interface configuration
* pfSense firewall rules
* pfSense firewall logs
* Windows Event Viewer
* Sysmon events
* Wazuh Agent status
* Wazuh Dashboard
* Suricata configuration
* Suricata alerts

Each screenshot should include a short explanation describing what it proves.

---

# 16. Security Considerations

The laboratory should remain isolated from unauthorized systems.

Security testing must only be performed against systems that are owned by the tester or explicitly authorized for testing.

The Kali Linux machine should be treated as a controlled attack simulation system rather than an unrestricted attack platform.

---

# 17. Summary

The installation and configuration process establishes the technical foundation required for the SOC monitoring workflow.

The final environment provides:

**Network Segmentation → Security Controls → Endpoint Telemetry → SIEM → Detection → Investigation**

Configuration evidence should be maintained throughout the project to make the implementation reproducible and auditable.
