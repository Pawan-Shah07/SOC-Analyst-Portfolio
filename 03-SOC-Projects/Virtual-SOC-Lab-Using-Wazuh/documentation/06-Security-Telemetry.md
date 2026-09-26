# Security Telemetry

## 1. Overview

Security telemetry is the foundation of effective SOC monitoring.

The Virtual SOC Home Lab collects telemetry from multiple security controls and endpoint sources to provide visibility into activity occurring across the environment.

The primary telemetry sources are:

* pfSense
* Suricata
* Windows Security Logs
* Sysmon
* Wazuh Agent
* Wazuh Manager

The objective is not simply to collect logs, but to understand **what each source tells the SOC analyst** and how the sources can be correlated during an investigation.

---

# 2. Telemetry Architecture

```text
                  Security Activity
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
     pfSense          Suricata         Windows
     Firewall            IDS           Endpoint
        │                │                │
        │                │        ┌───────┴───────┐
        │                │        │               │
        │                │    Security          Sysmon
        │                │      Logs             │
        │                │        │               │
        └────────────────┴────────┴───────────────┘
                             │
                             ▼
                      Wazuh Manager
                             │
                             ▼
                       Wazuh Alerts
                             │
                             ▼
                        Investigation
```

---

# 3. pfSense Telemetry

pfSense provides firewall and network-related telemetry.

Relevant information may include:

* Timestamp
* Source address
* Destination address
* Source port
* Destination port
* Protocol
* Firewall action

This information can help analysts understand how traffic interacted with the firewall.

For example, a repeated series of blocked connections from a single source may warrant investigation depending on the context.

---

# 4. Suricata Telemetry

Suricata provides network intrusion detection telemetry.

An IDS alert may provide information such as:

* Timestamp
* Source
* Destination
* Protocol
* Detection signature
* Alert classification
* Rule identifier

Suricata telemetry is particularly useful for identifying network activity that matches known detection patterns.

---

# 5. Windows Security Telemetry

Windows Security Event Logs provide operating-system-level security information.

Examples of useful telemetry include:

* Authentication activity
* Failed logins
* Successful logins
* Account-related activity
* Security policy events

This telemetry helps analysts investigate activity involving Windows user accounts and authentication.

---

# 6. Sysmon Telemetry

Sysmon enhances endpoint visibility by generating detailed system activity events.

Depending on the configured rules, useful telemetry may include:

* Process creation
* Process relationships
* Executable information
* Network-related activity
* File activity

Sysmon is valuable because it provides additional context that may not be available through standard Windows Security logs alone.

---

# 7. Wazuh Agent Telemetry

The Wazuh Agent operates on the Windows endpoint and provides a mechanism for collecting and forwarding endpoint telemetry.

The agent allows security events to be centralized so that analysts do not have to manually inspect every endpoint.

---

# 8. Wazuh Manager

The Wazuh Manager acts as the central monitoring component.

Its role includes:

* Receiving endpoint telemetry
* Processing security events
* Applying detection logic
* Generating alerts
* Providing centralized security visibility

This allows security analysts to investigate events from a central location.

---

# 9. Telemetry Comparison

| Source                | Layer    | Primary Visibility             |
| --------------------- | -------- | ------------------------------ |
| pfSense               | Network  | Firewall activity              |
| Suricata              | Network  | IDS detection                  |
| Windows Security Logs | Endpoint | Authentication/security events |
| Sysmon                | Endpoint | Detailed system activity       |
| Wazuh Agent           | Endpoint | Telemetry forwarding           |
| Wazuh Manager         | SIEM     | Centralized analysis           |

---

# 10. Why Multiple Telemetry Sources Matter

No single telemetry source provides complete visibility.

For example:

```text
Firewall
   │
   └── Shows network connection behavior

IDS
   │
   └── Shows potentially suspicious network patterns

Windows Security
   │
   └── Shows authentication/security activity

Sysmon
   │
   └── Shows detailed endpoint activity
```

Combining these sources provides a more complete investigation context.

---

# 11. Telemetry Correlation

Consider a hypothetical investigation involving suspicious network activity.

An analyst may observe:

```text
1. Kali generates network activity
          ↓
2. pfSense records traffic
          ↓
3. Suricata detects suspicious activity
          ↓
4. Windows generates endpoint telemetry
          ↓
5. Wazuh receives endpoint events
          ↓
6. Wazuh produces an alert
          ↓
7. Analyst correlates evidence
```

The analyst can then compare:

* Source
* Destination
* Timestamp
* Protocol
* Activity type
* Endpoint events

This correlation helps establish whether the events are related.

---

# 12. Telemetry Quality

Effective detection depends on telemetry quality.

Important considerations include:

* Correct timestamps
* Accurate host information
* Appropriate log sources
* Sufficient event detail
* Reliable log forwarding
* Correct parsing
* Appropriate detection rules

Poor telemetry can result in:

* Missing events
* Incomplete investigations
* False positives
* False negatives
* Difficulty establishing timelines

---

# 13. SOC Analyst Perspective

A SOC analyst should not treat logs as isolated records.

Instead, telemetry should be viewed as evidence that helps answer:

> **What happened, when did it happen, where did it happen, and what systems were affected?**

This mindset transforms raw logs into useful investigative evidence.

---

# 14. Summary

The laboratory demonstrates a layered telemetry architecture combining network, firewall, IDS, endpoint, and SIEM data.

The combination of these sources enables analysts to move from individual security events toward a broader understanding of potentially suspicious activity.

The core principle is:

**Collect → Centralize → Correlate → Analyze → Investigate**
