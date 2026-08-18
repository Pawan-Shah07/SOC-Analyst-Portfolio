# OSI Model

## 1. Overview

The **Open Systems Interconnection (OSI) Model** is a seven-layer reference model used to describe network communication functions.

```text
7  Application
6  Presentation
5  Session
4  Transport
3  Network
2  Data Link
1  Physical
```

The OSI model is a conceptual framework rather than a protocol suite.

## 2. Why the Model Matters

The OSI model provides a common language for:

- Designing networks
- Explaining protocols
- Troubleshooting
- Isolating faults
- Mapping technologies to network functions

## 3. Layer 7 — Application

Provides network services used by applications.

Examples:

- HTTP/HTTPS
- DNS
- SMTP
- SSH
- FTP
- SNMP

## 4. Layer 6 — Presentation

Conceptually handles:

- Data representation
- Encoding and translation
- Encryption/decryption
- Compression/decompression

Modern protocols do not always map cleanly to this layer. TLS, for example, spans traditional OSI boundaries.

## 5. Layer 5 — Session

Manages logical communication sessions, including establishment, maintenance, synchronization, and termination.

## 6. Layer 4 — Transport

Provides process-to-process communication.

Common protocols:

- TCP
- UDP

Important concepts:

- Ports
- Reliability
- Segmentation/reassembly
- Flow control

## 7. Layer 3 — Network

Provides logical addressing and routing.

Examples:

- IPv4
- IPv6
- ICMP

Typical PDU: **packet**.

## 8. Layer 2 — Data Link

Provides local-link communication using framing and MAC addressing.

Examples:

- Ethernet
- Wi-Fi data-link functions

Typical PDU: **frame**.

## 9. Layer 1 — Physical

Transmits raw bits as electrical, optical, or radio signals.

Examples:

- Copper cable
- Fiber
- Radio
- Connectors
- Repeaters

## 10. PDU Summary

| Layer | PDU |
|---:|---|
| 7-5 | Data |
| 4 | Segment / Datagram |
| 3 | Packet |
| 2 | Frame |
| 1 | Bits |

## 11. Encapsulation

```text
Application Data
      ↓
TCP Header + Data
      ↓
IP Header + Segment
      ↓
Ethernet Header + Packet + Trailer
      ↓
Bits
```

## 12. De-encapsulation

The receiver reverses the process:

```text
Bits → Frame → Packet → Segment/Datagram → Data
```

## 13. Troubleshooting by Layer

```text
Layer 1 → cable, link, signal
Layer 2 → VLAN, MAC, frame, switching
Layer 3 → IP, gateway, route
Layer 4 → ports, TCP/UDP, service reachability
Layer 5-7 → session, encoding, application behavior
```

## 14. OSI vs TCP/IP

| OSI | TCP/IP |
|---|---|
| Application | Application |
| Presentation | Application |
| Session | Application |
| Transport | Transport |
| Network | Internet |
| Data Link | Network Access |
| Physical | Network Access |

## Key Takeaways

Remember the functional association:

```text
L4 → Ports / TCP / UDP
L3 → IP / Routing
L2 → MAC / Frames
L1 → Bits / Signals
```
