# Firewalls

## 1. Overview

A **firewall** is a security control that monitors and controls network traffic according to defined policy.

Firewalls can be implemented as:

- Network appliances
- Host-based software
- Cloud security controls
- Virtual appliances
- Next-generation platforms

## 2. Core Firewall Concepts

Typical rule attributes include:

- Source address
- Destination address
- Protocol
- Source port
- Destination port
- Interface/zone
- Direction
- Connection state
- Application identity, depending on the product

## 3. Example Rule

```text
Source:      LAN
Destination: Internet
Protocol:    TCP
Port:        443
Action:      Allow
```

## 4. Default Policy

A secure design generally defines explicit allowed traffic and rejects traffic that is not permitted by policy.

A common concept is:

```text
Default Deny
      ↓
Explicitly Allow Required Traffic
```

The exact policy should be based on business requirements.

## 5. Stateless vs Stateful

### Stateless Firewall
Evaluates each packet independently according to the rule set.

### Stateful Firewall
Tracks connection state and can make decisions based on established flows.

## 6. Common Firewall Actions

- Allow
- Deny
- Reject
- Log
- Rate-limit, depending on platform
- Inspect/forward through a security service

## 7. Network Zones

Firewalls may separate zones such as:

```text
Internet
   ↓
WAN
   ↓
DMZ
   ↓
Internal LAN
   ↓
Management
```

Each zone can have different policies.

## 8. Inbound vs Outbound Rules

### Inbound
Controls traffic entering a protected interface or zone.

### Outbound
Controls traffic leaving a protected interface or zone.

Direction must always be interpreted from the firewall/interface perspective.

## 9. Stateful Example

```text
Client → Server: TCP SYN
Server → Client: SYN/ACK
Client → Server: ACK
```

A stateful firewall tracks the flow and may allow return traffic as part of the established session.

## 10. Logging

Useful firewall logs can include:

- Timestamp
- Action
- Source IP/port
- Destination IP/port
- Protocol
- Interface
- Rule ID
- NAT information
- Packet/byte counts

## 11. Common Mistakes

- Overly broad `any/any` rules
- Rules without logging where logs are required
- Incorrect rule order
- Overlapping rules
- Forgetting return-path requirements
- Allowing administrative ports from untrusted networks

## 12. Practical Example

```text
Internet
   ↓
WAN Firewall
   ↓
LAN 192.168.10.0/24
```

A least-privilege approach might allow only required outbound services and specifically authorized administrative connections.

## Key Takeaways

Firewalls enforce policy. Learn rule matching, state tracking, zones, default policy, least privilege, rule order, and firewall logging.
