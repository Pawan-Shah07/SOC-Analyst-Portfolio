# Limitations and Lessons Learned

## 1. Overview

Every cybersecurity laboratory has limitations.

Documenting these limitations is important because it demonstrates an understanding of the difference between a controlled learning environment and a production enterprise SOC.

The Virtual SOC Home Lab provides practical experience with security monitoring and investigation, but it does not reproduce the scale, complexity, or operational constraints of a production environment.

---

# 2. Project Limitations

## 2.1 Limited Scale

The environment contains a small number of virtual machines compared with a production enterprise environment.

A production SOC may monitor:

* Hundreds or thousands of endpoints
* Multiple network segments
* Cloud workloads
* Servers
* Applications
* Identity systems
* Security appliances

The laboratory therefore provides limited data volume and diversity.

---

## 2.2 Controlled Attack Activity

Security activity is intentionally generated for testing.

This differs from real-world attacks, where adversaries may:

* Adapt their behavior
* Attempt to evade detection
* Maintain persistence
* Use multiple compromised systems
* Modify tactics based on defensive controls

Therefore, laboratory detection results should not be interpreted as representative of all real-world attacks.

---

## 2.3 Limited Endpoint Diversity

The environment primarily focuses on Windows endpoint monitoring.

Enterprise SOCs typically monitor multiple operating systems and platforms.

Future versions of the lab could include:

* Additional Windows endpoints
* Linux servers
* Network devices
* Cloud workloads

---

## 2.4 Limited High Availability

The laboratory does not represent a production high-availability architecture.

Production environments may require:

* Redundant SIEM infrastructure
* Backup systems
* Failover
* Load balancing
* Disaster recovery

The home lab prioritizes learning and experimentation instead.

---

## 2.5 Limited Automation

The current environment focuses primarily on monitoring, detection, and investigation.

Production SOCs may integrate:

* SOAR platforms
* Automated containment
* Automated enrichment
* Ticketing systems
* Case management
* Threat intelligence automation

---

# 3. Detection Limitations

Detection quality depends on:

* Available telemetry
* Detection rules
* Configuration
* Log quality
* Event visibility

A security event that does not generate appropriate telemetry may not be detected.

Similarly, broad detection rules may produce false positives.

Therefore:

> **Detection coverage is dependent on the quality and completeness of the underlying telemetry.**

---

# 4. Investigation Limitations

Investigations are constrained by the evidence available within the laboratory.

For example, if a required telemetry source is not collected, an analyst may not be able to establish:

* Full attack timeline
* Complete process lineage
* Initial access method
* Lateral movement
* Data access

This demonstrates the importance of designing telemetry collection around investigative requirements.

---

# 5. Lessons Learned

## 5.1 Telemetry Is Fundamental

A SIEM is only as useful as the data it receives.

Deploying Wazuh alone does not automatically provide complete security visibility.

Effective monitoring requires appropriate:

* Log sources
* Event collection
* Parsing
* Detection logic
* Retention

---

## 5.2 Multiple Data Sources Improve Investigation

Firewall, IDS, Windows, and Sysmon telemetry provide different perspectives.

Correlating them can improve confidence during an investigation.

```text
Network Evidence
       +
Firewall Evidence
       +
Endpoint Evidence
       +
SIEM Alert
       ↓
Improved Investigation Context
```

---

## 5.3 Alerts Require Investigation

An alert should not automatically be treated as a confirmed incident.

The analyst must determine whether the event is:

* Malicious
* Benign
* False positive
* Inconclusive

This is a critical SOC analyst skill.

---

## 5.4 Context Matters

The same event can have different security significance depending on context.

For example, a network scan performed by an authorized security tester has a different interpretation from an unexpected scan originating from an unknown system.

Therefore, analysts should always consider:

* Asset
* User
* Time
* Source
* Destination
* Expected behavior
* Business context

---

## 5.5 Documentation Is a Security Skill

A technically correct investigation has limited value if the findings cannot be communicated clearly.

Professional documentation should explain:

* What happened
* What evidence was observed
* What the evidence means
* What conclusion was reached
* What action is recommended

---

# 6. Professional SOC Lessons

The project reinforced several important SOC principles:

### Principle 1

**Visibility must precede effective detection.**

### Principle 2

**Detection without investigation is incomplete.**

### Principle 3

**Evidence should support conclusions.**

### Principle 4

**Multiple telemetry sources improve analytical context.**

### Principle 5

**Security monitoring requires continuous tuning.**

### Principle 6

**Documentation is part of the incident response process.**

---

# 7. Areas for Improvement

Based on the implementation, future iterations can improve:

* Telemetry coverage
* Detection rules
* Endpoint diversity
* Threat intelligence
* Automation
* Threat hunting
* Detection engineering
* Incident response workflows

These improvements are documented separately in the Future Improvements section.

---

# 8. Summary

The limitations identified in this project do not reduce its value as a learning environment.

Instead, they demonstrate an important professional principle:

> **A security control should always be evaluated within the context of its coverage, telemetry, configuration, and operational environment.**

The project provides a practical foundation for continuing development in SOC operations, Blue Team engineering, detection engineering, threat hunting, and incident response.
