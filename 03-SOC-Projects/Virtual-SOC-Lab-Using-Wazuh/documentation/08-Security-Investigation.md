# Security Investigation

## 1. Overview

Security investigation is the primary analytical activity demonstrated by the Virtual SOC Home Lab.

The objective is to move beyond alert identification and determine:

* What happened
* When it happened
* Which systems were involved
* How the activity occurred
* Whether the activity is malicious
* What evidence supports the conclusion
* What response may be appropriate

---

# 2. Investigation Methodology

Investigations follow an evidence-driven process.

```text
Alert
  ↓
Validation
  ↓
Evidence Collection
  ↓
Timeline Construction
  ↓
Telemetry Correlation
  ↓
Activity Analysis
  ↓
Verdict
  ↓
Response Recommendation
```

---

# 3. Phase 1 — Alert Validation

The first step is to determine whether the alert represents an actual event.

The analyst should review:

* Alert timestamp
* Source
* Destination
* Detection source
* Rule/signature
* Event details

The analyst should avoid making a conclusion before reviewing supporting evidence.

---

# 4. Phase 2 — Evidence Collection

Evidence should be collected from all relevant sources.

Potential sources include:

* Wazuh alerts
* pfSense logs
* Suricata alerts
* Windows Security Events
* Sysmon events

The objective is to establish sufficient context to understand the activity.

---

# 5. Phase 3 — Timeline Construction

Time correlation is important during an investigation.

A basic timeline can be structured as:

| Time | Source   | Event              | Significance          |
| ---- | -------- | ------------------ | --------------------- |
| T1   | Kali     | Activity generated | Initial activity      |
| T2   | pfSense  | Firewall event     | Network observation   |
| T3   | Suricata | IDS alert          | Detection             |
| T4   | Windows  | Endpoint event     | Host activity         |
| T5   | Wazuh    | SIEM alert         | Centralized detection |

Actual timestamps should be taken directly from collected logs.

---

# 6. Phase 4 — Telemetry Correlation

The analyst should correlate events using common attributes.

Useful correlation fields include:

* Timestamp
* Source IP
* Destination IP
* Host
* Username
* Process
* Port
* Protocol
* Event identifier

For example:

```text
Source IP
    +
Destination IP
    +
Timestamp
    +
Port
    +
Endpoint Event
    ↓
Correlated Activity
```

---

# 7. Phase 5 — Activity Analysis

The analyst should determine whether the observed behavior is consistent with the alert.

Questions include:

1. Is the source system authorized?
2. Is the destination expected?
3. Was the activity repeated?
4. Was the activity successful?
5. Was endpoint activity observed?
6. Is there evidence of persistence or execution?
7. Is there a legitimate explanation?

---

# 8. Phase 6 — MITRE ATT&CK Mapping

Where applicable, observed adversary behavior can be mapped to the **MITRE ATT&CK** framework.

The mapping should be evidence-based.

Do not assign a technique merely because a tool was used.

Instead, map the observed behavior.

For example:

```text
Observed Behavior
       ↓
Technical Analysis
       ↓
Adversary Technique
       ↓
MITRE ATT&CK Mapping
```

The specific technique should be documented only after validating the observed behavior.

---

# 9. Phase 7 — Verdict

The investigation should result in a clear classification.

Possible verdicts include:

### True Positive

The evidence supports that the detected behavior is genuinely malicious or unauthorized.

### Benign Positive

The detection is valid, but the activity is legitimate or authorized.

### False Positive

The detection was triggered incorrectly or the event does not represent the behavior described by the detection.

### Inconclusive

Available evidence is insufficient to determine the nature of the activity.

---

# 10. Phase 8 — Response Recommendation

The recommended response should be proportional to the evidence.

Potential response actions include:

* Continue monitoring
* Block source activity
* Isolate endpoint
* Disable compromised account
* Investigate related events
* Remove malicious artifacts
* Reset credentials
* Escalate the incident

For the home lab, response actions should remain within the controlled environment.

---

# 11. Investigation Documentation Template

Each investigation in the repository should use a consistent structure.

```markdown
# Investigation Title

## 1. Incident Summary

## 2. Detection

## 3. Initial Observations

## 4. Evidence

## 5. Timeline

## 6. Telemetry Correlation

## 7. Technical Analysis

## 8. MITRE ATT&CK Mapping

## 9. Impact Assessment

## 10. Verdict

## 11. Recommended Response

## 12. Lessons Learned
```

---

# 12. Evidence Handling

Evidence should be documented accurately.

The analyst should distinguish between:

**Observed Evidence**

and

**Analyst Interpretation**

For example:

> Observed: Multiple failed authentication events were recorded within a short period.

versus:

> Interpretation: The activity may indicate credential testing.

This distinction prevents assumptions from being presented as facts.

---

# 13. Investigation Quality

A professional investigation should be:

* Evidence-driven
* Reproducible
* Chronological
* Technically accurate
* Clear
* Concise
* Actionable

A good investigation should allow another analyst to understand how the conclusion was reached.

---

# 14. Summary

The investigation methodology provides a structured approach for transforming SIEM alerts into actionable security findings.

The key principle is:

> **Do not investigate the alert in isolation. Investigate the activity represented by the alert.**

By correlating network, firewall, IDS, Windows, Sysmon, and Wazuh telemetry, the analyst can develop a more complete understanding of the event.
