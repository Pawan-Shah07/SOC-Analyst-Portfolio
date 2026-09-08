# Virtual SOC Home Lab with Wazuh

> **A segmented virtual Security Operations Center (SOC) environment for centralized security monitoring, detection, and investigation.**

---

## 📌 Project Overview

The **Virtual SOC Home Lab with Wazuh** is a virtualized security monitoring environment designed to demonstrate how multiple security controls work together to support the core functions of a Security Operations Center (SOC).

The lab is implemented using **VMware Workstation 17 Pro** and consists of an external WAN network and a protected internal LAN separated by **pfSense**. **Kali Linux** operates as the controlled attacker system, while **Windows 10** represents a monitored endpoint within the protected network.

The environment integrates:

* **pfSense** — Firewall and network gateway
* **Suricata** — Network intrusion detection
* **Wazuh Agent** — Endpoint telemetry collection
* **Sysmon** — Enhanced Windows endpoint telemetry
* **Wazuh Manager/SIEM** — Centralized security monitoring and analysis
* **Windows 10** — Monitored endpoint
* **Ubuntu Server** — Wazuh server infrastructure
* **Kali Linux** — Controlled attack and traffic-generation system
* **VMware Workstation 17 Pro** — Virtualization platform

The primary objective is to demonstrate an end-to-end security monitoring workflow:

```text
Attack Activity
      ↓
Network / Endpoint Telemetry
      ↓
Firewall & IDS Detection
      ↓
Wazuh Manager / SIEM
      ↓
Security Alerts
      ↓
SOC Investigation
      ↓
Analysis & Response
```

---

## 🎯 Project Objectives

The project focuses on developing practical skills in security monitoring, detection, and investigation.

### Primary Objective

To design and implement a virtualized SOC environment capable of collecting, centralizing, detecting, and investigating security telemetry from network and endpoint security controls.

### Specific Objectives

* Design a segmented virtual network representing external and internal security zones.
* Configure pfSense as the network security boundary.
* Generate controlled security activity using Kali Linux.
* Monitor network activity using Suricata.
* Collect firewall security events from pfSense.
* Deploy Wazuh Agent on Windows 10.
* Integrate Sysmon to provide enhanced endpoint telemetry.
* Centralize security telemetry using Wazuh Manager.
* Analyze security events and alerts through the Wazuh platform.
* Investigate security activity using multiple telemetry sources.
* Document findings using a structured SOC investigation methodology.

---

# 🏗️ Architecture

The lab uses a segmented network architecture consisting of an external WAN network and a protected internal LAN.

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
                         Controlled
                       Security Activity
                                │
                                ▼
                    ┌────────────────────┐
                    │      pfSense       │
                    │ Firewall / Router  │
                    └─────────┬──────────┘
                              │
                              │
                    ┌─────────▼─────────┐
                    │     Suricata      │
                    │        IDS        │
                    └─────────┬─────────┘
                              │
                     PROTECTED LAN
                     192.168.10.0/24
                              │
                ┌─────────────┴─────────────┐
                │                           │
        ┌───────▼────────┐         ┌────────▼───────┐
        │   Windows 10   │         │ Ubuntu Server  │
        │                │         │                │
        │ Wazuh Agent    │         │ Wazuh Manager  │
        │ Sysmon         │         │     / SIEM     │
        └────────────────┘         └────────┬───────┘
                                             │
                                             ▼
                                    ┌────────────────┐
                                    │ Wazuh Dashboard│
                                    │ Alerts &       │
                                    │ Investigation  │
                                    └────────────────┘
```

### Network Segmentation

| Network           | Purpose                |
| ----------------- | ---------------------- |
| `172.16.10.0/24`  | External/WAN network   |
| `192.168.10.0/24` | Protected internal LAN |

The segmentation provides a controlled environment in which security activity can be generated from an external zone and observed as it interacts with the protected network.

---

# 🖥️ Lab Components

| Component                 | Role                                              |
| ------------------------- | ------------------------------------------------- |
| VMware Workstation 17 Pro | Virtualization platform                           |
| pfSense                   | Firewall, router, and network security boundary   |
| Kali Linux                | Controlled attacker and traffic-generation system |
| Suricata                  | Network intrusion detection                       |
| Windows 10                | Monitored endpoint                                |
| Wazuh Agent               | Endpoint telemetry collection                     |
| Sysmon                    | Enhanced Windows system telemetry                 |
| Ubuntu Server             | Wazuh Manager/SIEM host                           |
| Wazuh                     | Centralized security monitoring and analysis      |

> **Note:** Software versions are intentionally not listed unless they have been verified from the actual implementation.

---

# 🔐 Security Monitoring Architecture

The lab provides visibility across multiple security layers.

## 1. Network Layer

Network activity generated by the attacker system can be observed as it traverses the security boundary.

**Primary technologies:**

* pfSense
* Suricata

These components provide visibility into network connections, firewall decisions, and potentially suspicious network activity.

---

## 2. Firewall Layer

pfSense acts as the primary security boundary between the external and internal networks.

Its responsibilities include:

* Network routing
* Traffic filtering
* Firewall enforcement
* Network segmentation
* Security event logging

Firewall logs provide valuable evidence regarding permitted and blocked network activity.

---

## 3. Network Detection Layer

**Suricata** provides network-based intrusion detection capabilities.

It monitors network traffic and can generate security alerts when traffic matches configured detection signatures or rules.

This provides the SOC analyst with network-level visibility that complements endpoint telemetry.

---

## 4. Endpoint Layer

Windows 10 represents a monitored enterprise endpoint.

The endpoint monitoring stack consists of:

### Wazuh Agent

The Wazuh Agent collects relevant endpoint telemetry and forwards it to the Wazuh Manager for centralized analysis.

### Sysmon

Sysmon enhances native Windows telemetry by providing additional information about endpoint activity, including process-related events.

Together, Wazuh Agent and Sysmon provide greater visibility into activity occurring on the monitored endpoint.

---

# 📊 Telemetry Sources

One of the primary objectives of this project is to demonstrate that security investigations become more effective when multiple telemetry sources are available.

| Telemetry Source      | Visibility Provided                       |
| --------------------- | ----------------------------------------- |
| pfSense               | Firewall and network security events      |
| Suricata              | Network intrusion detection alerts        |
| Windows Security Logs | Authentication and security events        |
| Sysmon                | Detailed endpoint/system activity         |
| Wazuh Agent           | Endpoint telemetry forwarding             |
| Wazuh Manager         | Centralized event processing and alerting |
| Wazuh Dashboard       | Security monitoring and investigation     |

---

# 🔄 SOC Detection Workflow

The laboratory simulates the following SOC workflow:

```text
┌──────────────────┐
│  Attack Activity │
│   Kali Linux     │
└────────┬─────────┘
         │
         ▼
┌─────────────────────────┐
│ Network Security Layer  │
│                         │
│ pfSense + Suricata      │
└──────────┬──────────────┘
           │
           │ Network / IDS
           │ Telemetry
           ▼
┌─────────────────────────┐
│     Windows Endpoint    │
│                         │
│ Wazuh Agent + Sysmon    │
└──────────┬──────────────┘
           │
           │ Endpoint
           │ Telemetry
           ▼
┌─────────────────────────┐
│    Wazuh Manager/SIEM   │
│                         │
│ Centralized Monitoring  │
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│       Alerting          │
│                         │
│ Detection & Correlation │
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│   SOC Investigation     │
│                         │
│ Evidence → Analysis     │
│ → Conclusion → Response │
└─────────────────────────┘
```

---

# 🧪 Security Testing

The environment is designed to generate controlled security activity for detection validation.

Testing focuses on observing how different security controls respond to activity and how the resulting telemetry reaches the SIEM.

Examples of activities that can be investigated include:

* Network scanning activity
* Repeated authentication failures
* Suspicious process activity
* Firewall-blocked connections
* IDS-triggered network activity
* Endpoint security events

All testing should be performed within the isolated laboratory environment.

---

# 🔎 Security Investigation Methodology

Security alerts are investigated using an evidence-driven approach.

The investigation process follows:

```text
Alert
  ↓
Validate
  ↓
Collect Evidence
  ↓
Establish Timeline
  ↓
Correlate Telemetry
  ↓
Analyze Activity
  ↓
Determine Verdict
  ↓
Recommend Response
```

### Investigation Questions

For each alert, the analyst should determine:

1. What happened?
2. When did it happen?
3. Which host generated the activity?
4. What was the source and destination?
5. Which protocol or service was involved?
6. Which security control detected it?
7. What evidence supports the alert?
8. Is the activity malicious, benign, or inconclusive?
9. What is the potential impact?
10. What response or remediation is appropriate?

---

# 🧩 Evidence Correlation

A key objective of the project is demonstrating how different security data sources can complement each other.

For example:

```text
Kali Activity
      │
      ├──────────────► pfSense
      │                  │
      │                  └── Firewall Event
      │
      ├──────────────► Suricata
      │                  │
      │                  └── IDS Alert
      │
      └──────────────► Windows Endpoint
                         │
                         ├── Windows Security Event
                         │
                         └── Sysmon Event
                                  │
                                  ▼
                          Wazuh Manager
                                  │
                                  ▼
                              Alert
                                  │
                                  ▼
                           Investigation
```

Correlating these sources allows the analyst to build a more complete understanding of an event rather than relying on a single log source.

---

# 📁 Repository Structure

```text
Virtual-SOC-Home-Lab/
│
├── README.md
│
├── documentation/
│   ├── 01-Project-Overview.md
│   ├── 02-Requirements-and-Scope.md
│   ├── 03-Architecture.md
│   ├── 04-Network-Design.md
│   ├── 05-Installation-and-Configuration.md
│   ├── 06-Security-Telemetry.md
│   ├── 07-Detection-and-Monitoring.md
│   ├── 08-Security-Investigation.md
│   ├── 09-Results-and-Validation.md
│   ├── 10-Limitations-and-Lessons-Learned.md
│   └── 11-Future-Improvements.md
│
├── investigations/
│   ├── README.md
│   ├── investigation-01-port-scan.md
│   ├── investigation-02-failed-logins.md
│   └── investigation-03-suspicious-process.md
│
├── screenshots/
│   ├── architecture/
│   ├── installation/
│   ├── wazuh/
│   ├── pfsense/
│   ├── suricata/
│   └── sysmon/
│
└── diagrams/
    └── virtual-soc-architecture.png
```

---

# 📸 Screenshots and Evidence

Screenshots should be used to demonstrate implementation and validation rather than simply filling the report.

Recommended evidence includes:

### Architecture

* Complete network topology
* VMware virtual network configuration
* Network segmentation

### pfSense

* Interface configuration
* Firewall rules
* Firewall logs

### Suricata

* Interface configuration
* Detection configuration
* IDS alerts

### Windows

* Wazuh Agent
* Windows Event Viewer
* Sysmon events

### Wazuh

* Agent registration
* Log ingestion
* Security alerts
* Dashboard
* Investigation evidence

Each screenshot should include a short explanation describing **what the evidence demonstrates**.

---

# 📈 Validation and Results

The implementation should be validated by generating controlled security activity and confirming that the expected telemetry reaches the monitoring platform.

| Test                       | Expected Observation             | Result          |
| -------------------------- | -------------------------------- | --------------- |
| Network activity generated | Network telemetry available      | To be validated |
| Firewall event generated   | pfSense event recorded           | To be validated |
| IDS activity generated     | Suricata alert generated         | To be validated |
| Failed authentication      | Windows security event generated | To be validated |
| Process activity           | Sysmon event generated           | To be validated |
| Endpoint telemetry         | Wazuh Agent forwards events      | To be validated |
| SIEM monitoring            | Events visible in Wazuh          | To be validated |
| Alert investigation        | Evidence supports analysis       | To be validated |

> Replace the validation status with the actual results obtained during testing. Do not mark a test as successful unless it has been observed and verified.

---

# 🧠 Skills Demonstrated

This project demonstrates practical experience in:

### Network Security

* Network segmentation
* Firewall configuration
* Routing
* Network monitoring
* IDS concepts
* Security telemetry

### Endpoint Security

* Windows event monitoring
* Sysmon
* Wazuh Agent
* Endpoint telemetry analysis

### SIEM

* Centralized log collection
* Security alert analysis
* Event investigation
* Multi-source telemetry analysis

### SOC Operations

* Alert triage
* Evidence collection
* Event correlation
* Security investigation
* Incident documentation
* Detection validation

### Documentation

* Technical documentation
* Architecture documentation
* Investigation reports
* Evidence-based analysis
* Security findings and recommendations

---

# ⚠️ Limitations

This project is implemented as a controlled virtual laboratory and does not represent the scale or operational complexity of a production enterprise SOC.

Key limitations include:

* Limited number of endpoints
* Limited network traffic volume
* Single virtualized environment
* Controlled attack scenarios
* No production-scale log retention
* No high-availability architecture
* Limited automation
* Limited number of external threat intelligence sources

The results therefore demonstrate **technical capability and methodology**, rather than production-level SOC performance.

---

# 🚀 Future Improvements

The environment can be extended to provide additional SOC capabilities.

### Planned Enhancements

* Add additional Windows and Linux endpoints
* Develop custom Wazuh detection rules
* Integrate threat intelligence
* Implement automated response
* Add additional network sensors
* Develop threat-hunting workflows
* Implement centralized log retention
* Add SOAR capabilities
* Introduce additional attack scenarios
* Map detections to MITRE ATT&CK
* Develop detection engineering use cases
* Introduce cloud security telemetry

A potential future architecture could evolve toward:

```text
                 Multiple Endpoints
                         │
              ┌──────────┴──────────┐
              │                     │
          Windows                 Linux
              │                     │
              └──────────┬──────────┘
                         │
                         ▼
                  Wazuh SIEM
                         │
            ┌────────────┼────────────┐
            │            │            │
            ▼            ▼            ▼
        Network       Threat       Endpoint
        Telemetry   Intelligence   Telemetry
            │            │            │
            └────────────┼────────────┘
                         ▼
                  Detection Layer
                         │
                         ▼
                       SOC
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
         Investigation         Response
```

---

# 📚 Key Takeaways

The Virtual SOC Home Lab demonstrates that effective security monitoring requires visibility across multiple layers of an environment.

The project combines:

**Network Security**

→ pfSense + Suricata

**Endpoint Security**

→ Windows + Wazuh Agent + Sysmon

**SIEM**

→ Wazuh Manager

**Investigation**

→ Centralized security telemetry and evidence correlation

The resulting architecture provides a practical demonstration of how a SOC can move from **security event generation to detection, investigation, and response**.

---

# 🏁 Conclusion

The **Virtual SOC Home Lab with Wazuh** provides a controlled environment for developing practical Blue Team and SOC analyst capabilities.

By integrating network security controls, endpoint telemetry, IDS monitoring, firewall logging, and centralized SIEM capabilities, the project demonstrates an end-to-end security monitoring workflow.

The primary value of the project is not the deployment of individual security tools, but the ability to **collect meaningful telemetry, identify security-relevant activity, correlate evidence, investigate alerts, and communicate findings clearly**.

This project therefore serves as a practical foundation for further development in **SOC operations, Blue Team engineering, detection engineering, threat hunting, and incident response**.

---

## 👤 Project Author

**https://github.com/Pawan-Shah07/SOC-Analyst-Portfolio/blob/main/01-Projects/Virtual-SOC-Lab-Using-Wazuh**

This project was developed as a hands-on cybersecurity laboratory to demonstrate practical security monitoring, detection, investigation, and technical documentation capabilities.

---

## ⚠️ Disclaimer

This project is intended for **educational and defensive security purposes only**.

All security testing should be performed within an authorized and isolated laboratory environment. Do not perform security testing against systems or networks without explicit authorization.
