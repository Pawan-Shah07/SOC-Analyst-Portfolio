# Detection and Monitoring

## 1. Overview

Detection and monitoring are core functions of the Virtual SOC Home Lab.

The environment is designed to identify security-relevant activity using multiple detection sources and centralize the resulting telemetry within Wazuh.

The monitoring strategy combines:

* Firewall monitoring
* Network intrusion detection
* Windows security monitoring
* Sysmon endpoint monitoring
* SIEM alerting

---

# 2. Detection Architecture

```text
                  Security Activity
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
     pfSense          Suricata         Windows
     Firewall            IDS           Endpoint
        │                │                │
        │                │        ┌───────┴──────┐
        │                │        │              │
        │                │    Windows          Sysmon
        │                │    Events
        │                │        │              │
        └────────────────┴────────┴──────────────┘
                             │
                             ▼
                       Wazuh Manager
                             │
                             ▼
                           Alerts
                             │
                             ▼
                        SOC Analyst
```

---

# 3. Detection Sources

## 3.1 Firewall Detection

pfSense provides visibility into traffic that interacts with configured firewall policies.

Firewall events can assist analysts in identifying:

* Blocked connections
* Unexpected traffic
* Repeated connection attempts
* Suspicious source activity

Firewall logs should always be interpreted in context.

A blocked connection alone does not necessarily indicate malicious activity.

---

## 3.2 Network IDS Detection

Suricata provides network-level detection.

Its detection engine can identify traffic patterns that match configured signatures and rules.

An analyst should examine:

* Signature
* Source
* Destination
* Protocol
* Port
* Timestamp
* Alert classification

---

## 3.3 Endpoint Detection

Windows endpoint monitoring provides host-level visibility.

Useful detection sources include:

* Windows Security Events
* Sysmon events
* Wazuh Agent telemetry

This allows the analyst to investigate activity occurring directly on the endpoint.

---

# 4. Example Detection Use Cases

The following use cases are suitable for validating the monitoring environment.

## Use Case 1 — Network Scanning

### Objective

Identify controlled network scanning activity.

### Potential Evidence

* Repeated connection attempts
* Multiple destination ports
* Firewall events
* Suricata alerts

### Investigation

The analyst should determine:

* Source system
* Target system
* Ports targeted
* Time of activity
* Whether the behavior is expected

---

## Use Case 2 — Failed Authentication

### Objective

Identify repeated failed authentication attempts.

### Potential Evidence

* Windows Security Event
* Username
* Source address
* Timestamp
* Number of attempts

### Investigation

The analyst should determine whether the behavior represents:

* User error
* Misconfiguration
* Credential testing
* Brute-force behavior

---

## Use Case 3 — Suspicious Process Activity

### Objective

Identify potentially suspicious endpoint process activity.

### Potential Evidence

* Sysmon process events
* Process name
* Parent process
* Command line
* User context
* Timestamp

### Investigation

The analyst should determine whether the process behavior is legitimate or potentially malicious.

---

# 5. Alert Triage

When an alert is generated, the analyst should initially validate the event before assigning a verdict.

Recommended triage process:

```text
Alert Received
      ↓
Validate Alert
      ↓
Identify Source
      ↓
Review Context
      ↓
Collect Supporting Evidence
      ↓
Determine Severity
      ↓
Investigate
```

---

# 6. Alert Validation

The analyst should verify:

* Is the alert based on a real event?
* Is the source known?
* Is the destination expected?
* Is the behavior normal?
* Is there supporting telemetry?
* Is there evidence of malicious intent?

This prevents analysts from immediately treating every alert as a confirmed incident.

---

# 7. Detection Severity

Severity should be determined based on the available evidence and potential impact.

Possible classifications include:

| Classification | Meaning                                                     |
| -------------- | ----------------------------------------------------------- |
| Informational  | Activity observed without immediate security concern        |
| Low            | Suspicious or unusual activity with limited impact          |
| Medium         | Activity requiring investigation                            |
| High           | Strong indication of malicious activity or significant risk |
| Critical       | Severe or confirmed activity requiring immediate response   |

The exact severity assigned should depend on the detection logic and investigation context.

---

# 8. False Positives

Detection systems can generate alerts for legitimate activity.

Examples may include:

* Administrative activity
* Authorized security testing
* Normal software behavior
* Automated system processes
* User authentication mistakes

Therefore:

> **An alert is an investigation starting point, not automatically proof of compromise.**

---

# 9. Detection Validation

Each detection should be tested using controlled activity.

A validation process should include:

1. Define the detection objective.
2. Generate controlled activity.
3. Confirm the expected telemetry.
4. Verify the alert.
5. Record timestamps.
6. Compare detection evidence with expected behavior.
7. Document the result.

---

# 10. Detection Engineering Considerations

A strong detection should ideally provide:

* Clear detection logic
* Reliable telemetry source
* Useful context
* Low unnecessary noise
* Appropriate severity
* Investigation value

Detection quality should be evaluated based on whether the resulting alert helps an analyst make a decision.

---

# 11. Monitoring Workflow

The SOC monitoring workflow can be summarized as:

```text
Monitor
   ↓
Detect
   ↓
Triage
   ↓
Validate
   ↓
Investigate
   ↓
Classify
   ↓
Respond
```

---

# 12. Summary

The monitoring architecture combines multiple security controls to provide visibility across network and endpoint layers.

The project demonstrates that effective SOC detection requires more than generating alerts. Analysts must validate alerts, understand their context, correlate evidence, and determine whether the observed behavior represents a genuine security concern.
