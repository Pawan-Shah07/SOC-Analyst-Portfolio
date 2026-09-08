# Project Overview — Virtual SOC Home Lab with Wazuh

## 1. Introduction

The **Virtual SOC Home Lab with Wazuh** is a virtualized cybersecurity environment designed to simulate the core monitoring and investigation functions of a modern **Security Operations Center (SOC)**.

The project integrates network security, intrusion detection, endpoint monitoring, and Security Information and Event Management (SIEM) capabilities into a single controlled laboratory environment.

The infrastructure is deployed using **VMware Workstation 17 Pro** and is intentionally segmented into an external WAN network and a protected internal LAN. **pfSense** operates as the primary firewall and routing boundary between these networks.

Within the environment, **Kali Linux** represents an external attacker and is used to generate controlled security activity. **Windows 10** represents a monitored endpoint on the protected network. Endpoint telemetry is collected through **Wazuh Agent** and enhanced using **Sysmon**. **Suricata** provides network intrusion detection capabilities, while pfSense contributes firewall and network security telemetry.

**Ubuntu Server** hosts the **Wazuh Manager/SIEM**, which centralizes security telemetry and provides the primary platform for security alert monitoring and investigation.

The project demonstrates the following security operations workflow:

```text
Attack Activity
       ↓
Network / Endpoint Telemetry
       ↓
Firewall / IDS / Endpoint Detection
       ↓
Wazuh Manager / SIEM
       ↓
Security Alert
       ↓
SOC Investigation
       ↓
Analysis and Response
```

---

## 2. Project Purpose

The primary purpose of this project is to develop practical experience with the technologies, processes, and analytical techniques used in defensive cybersecurity operations.

Rather than focusing solely on the installation of individual security tools, the project demonstrates how multiple security controls can work together to provide visibility across different layers of an environment.

The lab provides an opportunity to observe:

* Network activity
* Firewall decisions
* Intrusion detection alerts
* Windows security events
* Process and system activity
* Centralized security telemetry
* SIEM alerts
* Security investigation evidence

This approach reflects an important SOC principle:

> **A security event becomes more useful when it can be investigated using reliable and correlated evidence from multiple telemetry sources.**

---

## 3. Problem Statement

Organizations generate large volumes of security telemetry from firewalls, endpoints, intrusion detection systems, operating systems, and other security controls.

Without centralized monitoring and appropriate analysis, security-relevant activity can be difficult to identify and investigate.

A SOC therefore requires the ability to:

1. Collect security telemetry from different sources.
2. Centralize the collected data.
3. Identify potentially suspicious activity.
4. Generate actionable alerts.
5. Investigate alerts using supporting evidence.
6. Determine the nature and potential impact of the activity.
7. Recommend appropriate response actions.

This project addresses these requirements within a controlled virtual laboratory by integrating network, firewall, IDS, endpoint, and SIEM technologies.

---

# 4. Project Objectives

## 4.1 Primary Objective

To design and implement a virtualized SOC environment capable of collecting, centralizing, monitoring, detecting, and investigating security events across network and endpoint systems.

## 4.2 Specific Objectives

The project aims to:

* Implement a segmented virtual network using VMware Workstation 17 Pro.
* Separate the external WAN network from the protected internal LAN.
* Configure pfSense as the firewall and routing boundary.
* Use Kali Linux to generate controlled security activity.
* Deploy Suricata for network intrusion detection.
* Collect firewall security telemetry from pfSense.
* Configure Windows 10 as a monitored endpoint.
* Deploy Wazuh Agent for endpoint telemetry collection.
* Use Sysmon to enhance Windows endpoint visibility.
* Deploy Ubuntu Server as the Wazuh Manager/SIEM platform.
* Centralize security telemetry within Wazuh.
* Analyze security alerts and supporting evidence.
* Perform controlled SOC investigations.
* Document findings using an evidence-driven methodology.

---

# 5. Project Scope

The scope of the project covers the design, implementation, testing, and documentation of a small-scale virtual SOC environment.

### In Scope

| Area                | Scope                                                                 |
| ------------------- | --------------------------------------------------------------------- |
| Virtualization      | Deployment of security infrastructure using VMware Workstation 17 Pro |
| Network Security    | Network segmentation and firewall enforcement using pfSense           |
| Network Monitoring  | Network traffic monitoring and IDS capabilities using Suricata        |
| Endpoint Monitoring | Windows 10 monitoring using Wazuh Agent and Sysmon                    |
| SIEM                | Centralized telemetry collection and analysis using Wazuh             |
| Security Testing    | Controlled generation of security-related activity                    |
| Detection           | Identification and analysis of security alerts                        |
| Investigation       | Evidence-based investigation of detected activity                     |
| Documentation       | Technical documentation and SOC investigation reports                 |

### Out of Scope

The laboratory does not attempt to reproduce the scale or operational complexity of a production enterprise SOC.

The following areas are outside the primary scope:

* Production-scale infrastructure
* High-availability SIEM deployment
* Large-scale endpoint management
* Enterprise-wide log retention
* Production incident response
* Real-world unauthorized attack activity
* Full SOAR automation
* Production cloud security monitoring

---

# 6. Lab Environment

The environment consists of multiple virtual machines and security components, each serving a specific security monitoring function.

| Component                 | Function                                           |
| ------------------------- | -------------------------------------------------- |
| VMware Workstation 17 Pro | Hosts and isolates the virtual laboratory          |
| Kali Linux                | Controlled attacker and traffic-generation system  |
| pfSense                   | Firewall, router, and network security boundary    |
| Suricata                  | Network intrusion detection                        |
| Windows 10                | Monitored endpoint                                 |
| Wazuh Agent               | Endpoint telemetry collection                      |
| Sysmon                    | Enhanced Windows endpoint telemetry                |
| Ubuntu Server             | Wazuh Manager/SIEM host                            |
| Wazuh                     | Centralized security monitoring and alert analysis |

> **Version Note:** Software versions are intentionally excluded unless verified from the actual laboratory implementation.

---

# 7. Network Environment

The laboratory uses two primary network segments.

| Network           | Security Role          |
| ----------------- | ---------------------- |
| `172.16.10.0/24`  | External / WAN segment |
| `192.168.10.0/24` | Protected internal LAN |

The external network represents an untrusted or less-trusted zone where controlled attack activity originates.

The internal network contains the monitored endpoint and Wazuh infrastructure.

pfSense provides the security boundary between these two environments.

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
                         │ Controlled
                         │ Security Activity
                         ▼
                ┌──────────────────┐
                │     pfSense      │
                │ Firewall / Router│
                └────────┬─────────┘
                         │
                         │
                  PROTECTED LAN
                  192.168.10.0/24
                         │
              ┌──────────┴──────────┐
              │                     │
       ┌──────▼───────┐     ┌───────▼────────┐
       │   Windows 10 │     │ Ubuntu Server  │
       │              │     │                │
       │ Wazuh Agent  │     │ Wazuh Manager  │
       │ Sysmon       │     │     / SIEM     │
       └──────────────┘     └────────────────┘
```

---

# 8. Security Architecture

The security architecture follows a layered monitoring model.

## 8.1 Network Security

**pfSense** establishes the network security boundary and controls traffic between the external and internal segments.

It provides:

* Firewall enforcement
* Routing
* Network segmentation
* Firewall logging

---

## 8.2 Network Intrusion Detection

**Suricata** provides network-level detection capabilities.

It monitors network traffic and can generate alerts when observed traffic matches configured detection signatures or rules.

This provides visibility into activity that may not be apparent from endpoint logs alone.

---

## 8.3 Endpoint Security Monitoring

The Windows endpoint provides host-level telemetry through:

* Windows Security Events
* Wazuh Agent
* Sysmon

Wazuh Agent provides the mechanism for forwarding relevant endpoint telemetry to the centralized Wazuh infrastructure.

Sysmon supplements native Windows logging with additional endpoint visibility, particularly around system and process activity.

---

## 8.4 SIEM

The **Wazuh Manager/SIEM** provides centralized security monitoring.

Its role within the laboratory includes:

* Receiving security telemetry
* Processing events
* Generating security alerts
* Providing centralized visibility
* Supporting security investigations

The Wazuh Dashboard provides an interface through which collected security information can be reviewed and analyzed.

---

# 9. Telemetry Sources

A key feature of the project is the use of multiple telemetry sources.

```text
                         SECURITY ACTIVITY
                                │
                ┌───────────────┼───────────────┐
                │               │               │
                ▼               ▼               ▼
             pfSense         Suricata        Windows
             Firewall           IDS           Endpoint
                │               │               │
                │               │        ┌──────┴──────┐
                │               │        │             │
                │               │     Security       Sysmon
                │               │       Logs         Events
                │               │        │             │
                └───────────────┴────────┴─────────────┘
                                      │
                                      ▼
                              Wazuh Manager
                                      │
                                      ▼
                                Security Alert
                                      │
                                      ▼
                                Investigation
```

### Primary Telemetry Sources

| Source                | Security Visibility                       |
| --------------------- | ----------------------------------------- |
| pfSense               | Firewall and network events               |
| Suricata              | Network intrusion detection events        |
| Windows Security Logs | Authentication and security activity      |
| Sysmon                | Detailed endpoint/system activity         |
| Wazuh Agent           | Endpoint telemetry forwarding             |
| Wazuh Manager         | Centralized event processing and alerting |

---

# 10. SOC Workflow

The project models a simplified SOC operational workflow.

### Step 1 — Generate Activity

Controlled activity is generated within the isolated laboratory using Kali Linux or through endpoint activity on Windows.

### Step 2 — Capture Telemetry

Security controls observe the activity.

Depending on the activity, telemetry may be generated by:

* pfSense
* Suricata
* Windows Security Logs
* Sysmon

### Step 3 — Centralize Telemetry

Relevant endpoint telemetry is forwarded through the Wazuh Agent to the Wazuh Manager.

The Wazuh environment provides centralized visibility into the collected security data.

### Step 4 — Detect

Security-relevant activity can result in alerts within the Wazuh monitoring environment.

### Step 5 — Investigate

The analyst reviews the alert and examines supporting telemetry to determine:

* What happened
* When it happened
* Which system was involved
* What activity occurred
* Whether the activity appears malicious or benign

### Step 6 — Conclude and Respond

The analyst determines the appropriate conclusion and documents recommended response or remediation actions.

---

# 11. Security Investigation Approach

Investigations within the project follow an evidence-driven methodology.

```text
Alert
  │
  ▼
Alert Validation
  │
  ▼
Evidence Collection
  │
  ▼
Timeline Construction
  │
  ▼
Telemetry Correlation
  │
  ▼
Activity Analysis
  │
  ▼
Verdict
  │
  ▼
Response Recommendation
```

The investigation should avoid relying on assumptions.

Instead, conclusions should be supported by available evidence such as:

* Source and destination addresses
* Timestamps
* Network activity
* Firewall events
* IDS alerts
* Authentication events
* Process activity
* Wazuh alerts
* Relevant event identifiers

---

# 12. Project Deliverables

The project produces several forms of technical and analytical documentation.

### Technical Documentation

* Project overview
* Architecture documentation
* Network design
* Installation and configuration procedures
* Security telemetry documentation
* Detection and monitoring documentation

### SOC Documentation

* Security investigation reports
* Evidence analysis
* Detection validation
* Findings
* Conclusions
* Recommended response actions

### Supporting Evidence

* Network architecture diagrams
* Configuration screenshots
* Wazuh alerts
* Firewall events
* Suricata alerts
* Windows Event Logs
* Sysmon events

---

# 13. Skills Demonstrated

This project demonstrates practical capabilities across several cybersecurity domains.

## Network Security

* Network segmentation
* Firewall concepts
* Routing
* Network monitoring
* IDS concepts
* Security event analysis

## Endpoint Security

* Windows security logging
* Sysmon
* Wazuh Agent
* Endpoint telemetry analysis

## SIEM Operations

* Centralized log collection
* Event analysis
* Alert monitoring
* Security investigation

## SOC Operations

* Alert triage
* Evidence collection
* Event correlation
* Investigation
* Security documentation
* Detection validation

## Technical Documentation

* Architecture documentation
* Configuration documentation
* Evidence-based reporting
* Investigation write-ups
* Security findings and recommendations

---

# 14. Expected Outcomes

The project is designed to demonstrate the following outcomes:

1. A functional segmented virtual security environment.
2. Controlled security activity generated within the laboratory.
3. Visibility into network and endpoint activity.
4. Centralized security telemetry through Wazuh.
5. Detection of security-relevant events.
6. Ability to investigate alerts using supporting evidence.
7. Demonstration of an end-to-end SOC monitoring workflow.
8. Development of practical Blue Team and SOC analyst skills.

Actual results should be documented separately based on observed testing evidence.

---

# 15. Project Limitations

This laboratory is intentionally designed as a small-scale educational environment.

Its limitations include:

* Limited number of endpoints
* Limited network traffic volume
* Virtualized infrastructure
* Controlled attack scenarios
* Limited production-scale log volume
* No high-availability architecture
* Limited automation
* No production operational constraints

Therefore, the project should be considered a **practical SOC learning and demonstration environment**, rather than a production-ready enterprise SOC.

---

# 16. Future Development

The environment can be expanded to provide additional detection and investigation capabilities.

Potential enhancements include:

* Additional Windows endpoints
* Linux endpoint monitoring
* Custom Wazuh detection rules
* Threat intelligence integration
* Advanced threat hunting
* Additional IDS sensors
* Automated response
* SOAR integration
* Cloud security telemetry
* Expanded MITRE ATT&CK coverage
* Detection engineering use cases
* Larger-scale security scenarios

These improvements would allow the laboratory to evolve from a basic SOC monitoring environment toward a more comprehensive Blue Team training platform.

---

# 17. Conclusion

The **Virtual SOC Home Lab with Wazuh** demonstrates how multiple security technologies can be integrated to provide layered visibility across a controlled network environment.

The architecture combines:

```text
Network Security
      │
      ├── pfSense
      └── Suricata
            │
            ▼
Endpoint Security
      │
      ├── Windows Security Logs
      ├── Wazuh Agent
      └── Sysmon
            │
            ▼
Centralized Monitoring
      │
      └── Wazuh Manager / SIEM
            │
            ▼
Detection
      │
      ▼
Investigation
      │
      ▼
Analysis & Response
```

The primary learning outcome is not simply the deployment of individual cybersecurity tools. The project demonstrates the ability to understand **how security telemetry is generated, collected, centralized, analyzed, and used during a security investigation**.

This provides a practical foundation for further development in:

* SOC Operations
* Blue Team Engineering
* Detection Engineering
* Threat Hunting
* Incident Response
* SIEM Administration
* Security Monitoring
* Cybersecurity Technical Documentation

---

## Related Documentation

The following documents provide additional technical details:

* [Architecture](03-Architecture.md)
* [Network Design](04-Network-Design.md)
* [Installation and Configuration](05-Installation-and-Configuration.md)
* [Security Telemetry](06-Security-Telemetry.md)
* [Detection and Monitoring](07-Detection-and-Monitoring.md)
* [Security Investigation](08-Security-Investigation.md)
* [Results and Validation](09-Results-and-Validation.md)
* [Limitations and Lessons Learned](10-Limitations-and-Lessons-Learned.md)
* [Future Improvements](11-Future-Improvements.md)
