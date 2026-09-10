# Requirements and Scope

## 1. Overview

This document defines the technical requirements, functional requirements, security monitoring requirements, and scope of the **Virtual SOC Home Lab with Wazuh**.

The project is designed as a controlled virtual environment for demonstrating an end-to-end Security Operations Center (SOC) workflow.

The environment integrates network segmentation, firewall monitoring, network intrusion detection, endpoint telemetry, centralized security event management, alerting, and investigation.

The intended workflow is:

```text
Controlled Security Activity
            ↓
 Firewall / IDS / Endpoint Telemetry
            ↓
       Wazuh Manager
            ↓
           Alerts
            ↓
 Security Investigation
```

---

# 2. Project Scope

The project covers the design and implementation of a segmented virtual SOC monitoring environment.

The primary scope includes:

* Virtualized infrastructure
* Network segmentation
* Firewall and routing
* Controlled attacker activity
* Network intrusion detection
* Windows endpoint monitoring
* Sysmon-based endpoint telemetry
* Wazuh Agent deployment
* Wazuh Manager/SIEM deployment
* Security event collection
* Alert monitoring
* Security investigation
* Validation of the monitoring workflow
* Technical documentation

---

# 3. In-Scope Components

The following components are within the project scope.

| Component                 | Scope                                   |
| ------------------------- | --------------------------------------- |
| VMware Workstation 17 Pro | Virtual infrastructure                  |
| pfSense                   | Firewall, routing, and network boundary |
| Kali Linux                | Controlled security activity generation |
| Suricata                  | Network intrusion detection             |
| Windows 10                | Monitored endpoint                      |
| Sysmon                    | Windows endpoint telemetry              |
| Wazuh Agent               | Endpoint telemetry collection           |
| Ubuntu Server             | Wazuh Manager/SIEM host                 |
| Wazuh Manager             | Centralized security monitoring         |
| Wazuh Dashboard           | Alert and event visibility              |

---

# 4. Network Requirements

The environment requires two logically separated network segments.

| Network         | CIDR              | Purpose                           |
| --------------- | ----------------- | --------------------------------- |
| WAN / External  | `172.16.10.0/24`  | External or attacker-side segment |
| LAN / Protected | `192.168.10.0/24` | Internal monitored segment        |

The network architecture must ensure that the external and internal segments are separated through pfSense.

The segmentation provides a defined security boundary through which network activity can be controlled and monitored.

---

# 5. Virtualization Requirements

The project requires a virtualization platform capable of hosting multiple virtual machines and providing separate virtual network segments.

The environment uses **VMware Workstation 17 Pro**.

The virtualization platform must support:

* Multiple concurrent virtual machines
* Multiple virtual network adapters
* Separate virtual networks
* NAT-based networking
* Host-only or isolated networking
* Configurable virtual hardware
* VM snapshots or equivalent recovery mechanisms

---

# 6. System Requirements

The laboratory requires the following virtual systems.

| System        | Primary Role                  | Network Placement |
| ------------- | ----------------------------- | ----------------- |
| Kali Linux    | Attacker / activity generator | WAN               |
| pfSense       | Firewall / router             | WAN + LAN         |
| Windows 10    | Monitored endpoint            | LAN               |
| Ubuntu Server | Wazuh Manager/SIEM            | LAN               |

The exact CPU, memory, storage, and operating-system version requirements should be documented according to the actual environment rather than assumed values.

---

# 7. Functional Requirements

The laboratory must provide the following core functionality.

### FR-01 — Network Segmentation

The environment must separate the external WAN network from the protected LAN.

### FR-02 — Firewall Enforcement

pfSense must provide routing and firewall enforcement between the network segments.

### FR-03 — Controlled Security Activity

Kali Linux must be capable of generating authorized security activity within the laboratory.

### FR-04 — Network Monitoring

Suricata must monitor relevant network traffic for detectable suspicious activity.

### FR-05 — Endpoint Monitoring

Windows 10 must generate security telemetry through Windows event logging and Sysmon.

### FR-06 — Endpoint Telemetry Collection

Wazuh Agent must collect selected endpoint telemetry and forward it to the Wazuh Manager.

### FR-07 — Centralized Monitoring

Wazuh Manager must receive and process security telemetry.

### FR-08 — Alert Generation

The monitoring infrastructure must provide security alerts for applicable detected activity.

### FR-09 — Security Investigation

Collected telemetry must support investigation of detected activity.

### FR-10 — Validation

The integrated monitoring workflow must be validated using controlled test activity.

---

# 8. Security Monitoring Requirements

The monitoring architecture should provide visibility across multiple security layers.

## 8.1 Network Layer

Network monitoring should provide visibility into relevant traffic and suspicious network activity.

Primary source:

* Suricata

---

## 8.2 Firewall Layer

Firewall monitoring should provide visibility into traffic decisions and relevant network events.

Primary source:

* pfSense

---

## 8.3 Endpoint Layer

Endpoint monitoring should provide visibility into Windows security activity.

Primary sources:

* Windows Security Events
* Sysmon

---

## 8.4 SIEM Layer

The SIEM layer should centralize and analyze available security telemetry.

Primary platform:

* Wazuh Manager
* Wazuh Dashboard

---

# 9. Telemetry Requirements

The environment should collect sufficient telemetry to support basic SOC investigation.

The intended telemetry includes:

| Telemetry Source      | Expected Visibility                |
| --------------------- | ---------------------------------- |
| pfSense               | Firewall/network events            |
| Suricata              | IDS alerts                         |
| Windows Security Logs | Authentication and security events |
| Sysmon                | Detailed endpoint activity         |
| Wazuh Agent           | Endpoint telemetry forwarding      |
| Wazuh Manager         | Centralized event processing       |

The telemetry collected should be relevant to the monitoring objectives and should avoid unnecessary collection where practical.

---

# 10. Detection Requirements

The environment should support detection of controlled security activity.

Representative detection scenarios may include:

* Network scanning
* Repeated connection attempts
* Failed authentication activity
* Suspicious process activity
* Other controlled behaviors supported by the configured telemetry and detection rules

Detection scenarios should only be considered successful when the expected telemetry and alerting behavior are actually observed.

---

# 11. Investigation Requirements

The project should provide sufficient evidence for a SOC analyst to investigate detected activity.

An investigation should be capable of identifying, where available:

* Source
* Destination
* Timestamp
* Protocol
* Port
* Host
* User
* Process
* Detection rule or signature
* Related events

The available evidence should support development of an event timeline and an evidence-based conclusion.

---

# 12. Documentation Requirements

The project documentation must clearly describe:

* Project architecture
* Network design
* Installation and configuration
* Security telemetry
* Detection and monitoring
* Investigation methodology
* Validation results
* Limitations
* Lessons learned
* Future improvements

The documentation should use actual implementation details and evidence wherever possible.

---

# 13. Evidence Requirements

Important implementation and validation activities should be supported by evidence.

Evidence may include:

* Architecture diagrams
* Network configuration screenshots
* Firewall configuration screenshots
* Firewall logs
* Suricata alerts
* Windows Event Viewer screenshots
* Sysmon events
* Wazuh Agent status
* Wazuh alerts
* Investigation timelines

Each screenshot should have sufficient context to demonstrate what is being validated.

---

# 14. Security Requirements

The laboratory must remain within an authorized and controlled environment.

Security testing must:

* Target only laboratory systems.
* Use controlled test activity.
* Avoid unauthorized external targets.
* Avoid exposing intentionally vulnerable systems to untrusted networks.
* Maintain isolation between the laboratory and unrelated systems.
* Preserve the confidentiality of credentials and sensitive configuration data.

Any credentials, tokens, private keys, or other secrets must be excluded from the GitHub repository.

---

# 15. Performance Requirements

The laboratory should operate within the available host-system resources.

Performance considerations include:

* CPU utilization
* Memory utilization
* Storage capacity
* Network throughput
* Wazuh event-processing load
* Virtual machine resource allocation

The project does not define enterprise-scale performance requirements because it is designed as a home laboratory.

---

# 16. Operational Requirements

The environment should be maintainable and reproducible.

Operational requirements include:

* Clear system roles
* Documented network configuration
* Documented security controls
* Documented telemetry sources
* Repeatable validation procedures
* Configuration backups where appropriate
* VM snapshots or recovery points where practical

---

# 17. Out of Scope

The following areas are intentionally outside the current project scope.

### Production SOC Deployment

The project does not represent a production enterprise SOC.

### Enterprise High Availability

High-availability SIEM clusters, redundant infrastructure, and enterprise disaster recovery are not implemented.

### Large-Scale Endpoint Monitoring

The environment does not simulate hundreds or thousands of endpoints.

### Cloud Security Monitoring

Cloud-native telemetry and cloud infrastructure monitoring are outside the current scope.

### Advanced SOAR Automation

Automated incident response and enterprise SOAR workflows are not part of the current implementation.

### Enterprise Identity Infrastructure

The project does not require a full enterprise Active Directory or identity-management architecture.

### Production Threat Intelligence Platform

External threat-intelligence infrastructure is not a core requirement of the current implementation.

### Real-World Attack Simulation

The project does not authorize or conduct attacks against external or third-party systems.

---

# 18. Scope Boundaries

The project can be represented using the following boundary:

```text
┌─────────────────────────────────────────────────┐
│              PROJECT SCOPE                      │
│                                                 │
│  VMware Virtual Infrastructure                  │
│        │                                        │
│        ├── WAN / External Network               │
│        │      └── Kali Linux                    │
│        │                                        │
│        └── Protected LAN                        │
│               ├── Windows 10                   │
│               │      ├── Wazuh Agent            │
│               │      └── Sysmon                 │
│               │                                  │
│               └── Ubuntu Server                 │
│                      └── Wazuh Manager/SIEM     │
│                                                 │
│  pfSense + Suricata                             │
│  Detection + Monitoring + Investigation         │
└─────────────────────────────────────────────────┘

              OUTSIDE CURRENT SCOPE

      Production SOC
      Enterprise Scale
      Cloud Monitoring
      Advanced SOAR
      High Availability
```

---

# 19. Acceptance Criteria

The project is considered technically complete when the following objectives have been demonstrated.

| ID    | Acceptance Criteria                                 |
| ----- | --------------------------------------------------- |
| AC-01 | WAN and LAN networks are logically separated        |
| AC-02 | pfSense operates as the network security boundary   |
| AC-03 | Kali can generate controlled laboratory activity    |
| AC-04 | Suricata can observe relevant network activity      |
| AC-05 | Windows generates security telemetry                |
| AC-06 | Sysmon generates endpoint telemetry                 |
| AC-07 | Wazuh Agent communicates with the Wazuh Manager     |
| AC-08 | Wazuh Manager receives security telemetry           |
| AC-09 | Applicable security activity generates alerts       |
| AC-10 | Alerts can be investigated using available evidence |
| AC-11 | The monitoring workflow is validated and documented |

---

# 20. Scope Summary

The Virtual SOC Home Lab focuses on demonstrating an integrated security monitoring workflow within a controlled virtual environment.

The project scope can be summarized as:

```text
Virtual Infrastructure
        ↓
Network Segmentation
        ↓
Firewall + IDS
        ↓
Endpoint Telemetry
        ↓
Centralized SIEM
        ↓
Detection
        ↓
Alert Triage
        ↓
Security Investigation
```

The project intentionally prioritizes **practical SOC visibility, telemetry analysis, detection, and investigation** rather than attempting to reproduce the full complexity of a production enterprise SOC.
