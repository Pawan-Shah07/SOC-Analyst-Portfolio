# TCP/IP Model

## 1. Overview

The **TCP/IP model** describes the architecture used by modern IP networking and the Internet Protocol Suite.

The commonly taught model has four layers:

```text
4  Application
3  Transport
2  Internet
1  Network Access
```

## 2. Application Layer

Provides application-level network services.

Common protocols:

- HTTP/HTTPS
- DNS
- DHCP
- SSH
- SMTP/IMAP/POP3
- FTP
- SNMP
- NTP
- SMB

The TCP/IP Application Layer combines functions associated with OSI Application, Presentation, and Session layers.

## 3. Transport Layer

Provides process-to-process communication.

Primary protocols:

- **TCP:** connection-oriented, reliable, ordered transport.
- **UDP:** connectionless transport with low overhead and no built-in reliability.

Transport uses port numbers to identify service endpoints.

## 4. Internet Layer

Provides logical addressing and routing.

Key protocols include:

- IPv4
- IPv6
- ICMP

Routers primarily make forwarding decisions at this layer.

## 5. Network Access Layer

Combines local link and physical functions.

Examples:

- Ethernet
- Wi-Fi
- MAC addressing
- ARP-related local-link operation
- Physical media

## 6. Encapsulation

```text
Application → Data
Transport   → Segment / Datagram
Internet    → Packet
Network     → Frame / Bits
```

Example:

```text
HTTPS
  ↓
TCP/443
  ↓
IP
  ↓
Ethernet/Wi-Fi
```

## 7. TCP/IP vs OSI

| TCP/IP | Approximate OSI Mapping |
|---|---|
| Application | Layers 7, 6, 5 |
| Transport | Layer 4 |
| Internet | Layer 3 |
| Network Access | Layers 2, 1 |

The mapping is conceptual; real protocols do not always fit perfectly within one layer.

## 8. Example: Web Access

A browser accesses a web server:

```text
Application → HTTPS
Transport   → TCP
Internet    → IP
Network     → Ethernet/Wi-Fi
```

## 9. Example: Ping

```text
Ping utility
    ↓
ICMP
    ↓
IP
    ↓
Ethernet/Wi-Fi
```

ICMP does not use TCP or UDP ports.

## 10. Practical Commands

Windows:

```powershell
ipconfig /all
route print
ping 8.8.8.8
tracert 8.8.8.8
nslookup example.com
netstat -ano
```

Linux:

```bash
ip addr
ip route
ping 8.8.8.8
traceroute 8.8.8.8
dig example.com
ss -tuln
```

## Key Takeaways

Think of TCP/IP as:

```text
Application → What service?
Transport   → Which transport and ports?
Internet    → Which IPs and route?
Network     → Which local link?
```
