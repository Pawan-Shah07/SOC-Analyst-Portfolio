# Network Attacks

## 1. Overview

Network attacks target communication paths, network services, protocols, or the availability of networked systems.

This lesson introduces common attack categories and the network indicators associated with them.

## 2. Port Scanning

An attacker probes hosts and ports to identify reachable services.

Example:

```text
Target
 ├── 22
 ├── 80
 ├── 443
 ├── 445
 └── 3389
```

Indicators may include many connection attempts to different ports in a short period.

## 3. Network Discovery

Attackers may enumerate:

- Hosts
- Domains
- Services
- Routes
- Shares
- Network ranges

## 4. Brute-Force Attacks

Repeated authentication attempts target services such as:

- SSH
- RDP
- VPN
- Web applications
- Email

Useful indicators include repeated failures from one or more sources.

## 5. Denial of Service

DoS attacks aim to degrade or deny service availability.

Common categories:

- Volumetric attacks
- Protocol exhaustion
- Application-layer request floods

## 6. ARP Spoofing

An attacker forges ARP mappings to influence local traffic.

Potential impact:

- Traffic interception
- Man-in-the-middle
- Traffic disruption

## 7. DNS Attacks

Examples include:

- DNS spoofing
- Cache poisoning
- DNS tunneling
- Malicious domain infrastructure
- Domain generation algorithms

## 8. Man-in-the-Middle

An attacker positions themselves between endpoints to intercept or manipulate communications.

Defenses include:

- TLS
- Certificate validation
- Secure Wi-Fi
- Network segmentation
- Strong authentication

## 9. Session Hijacking

An attacker attempts to obtain or reuse an authenticated session identifier.

Defenses include:

- TLS
- Secure cookies
- Session rotation
- MFA
- Short session lifetimes

## 10. IP Spoofing

An attacker uses a forged source IP address.

Spoofing can be used in:

- Reflection attacks
- Evasion
- Certain denial-of-service techniques

Source validation and filtering can help reduce spoofing risk.

## 11. Network-Based Command and Control

A compromised endpoint may communicate with attacker infrastructure over:

- HTTP/HTTPS
- DNS
- Custom protocols
- Cloud services

Useful indicators include unusual destinations, periodic beaconing, unexpected domains, and suspicious endpoint processes.

## 12. Defensive Approach

A useful defense strategy combines:

```text
Segmentation
+ Firewall policy
+ DNS monitoring
+ IDS/IPS
+ Endpoint telemetry
+ Authentication controls
+ Logging
+ Threat intelligence
```

## 13. Investigation Model

```text
Detect
  ↓
Validate
  ↓
Scope
  ↓
Identify affected assets
  ↓
Correlate logs
  ↓
Contain
  ↓
Eradicate / remediate
  ↓
Document
```

## Key Takeaways

Learn to recognize the network signatures of scanning, brute force, DoS, spoofing, MITM, DNS abuse, and command-and-control traffic. Always combine network evidence with endpoint and identity context before assigning a verdict.
