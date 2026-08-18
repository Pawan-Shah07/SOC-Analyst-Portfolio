# TCP vs UDP

## 1. Overview

**TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)** are the two most important general-purpose transport protocols used with IP networks.

Both operate at the Transport Layer, but they provide different services.

## 2. TCP

TCP is **connection-oriented** and provides reliable, ordered byte-stream delivery.

### TCP provides

- Connection establishment
- Sequence numbers
- Acknowledgments
- Retransmission
- Flow control
- Congestion control
- Ordered delivery
- Graceful connection termination

## 3. UDP

UDP is **connectionless** and provides a lightweight datagram service.

UDP does not provide TCP-style:

- Connection establishment
- Retransmission
- Ordering
- Delivery guarantees
- Congestion control

Applications can implement their own reliability or control mechanisms when required.

## 4. Comparison

| Feature | TCP | UDP |
|---|---|---|
| Connection model | Connection-oriented | Connectionless |
| Reliability | Built in | Not built in |
| Ordering | Yes | No guarantee |
| Retransmission | Yes | No built-in retransmission |
| Flow control | Yes | No TCP-style mechanism |
| Congestion control | Yes | No TCP-style mechanism |
| Header overhead | Higher | Lower |
| Typical examples | HTTPS, SSH, SMTP | DNS, DHCP, NTP, RTP |

## 5. TCP Three-Way Handshake

```text
Client                    Server
  SYN  ─────────────────→
       ←──────────── SYN/ACK
  ACK  ─────────────────→
```

The handshake establishes initial TCP state before normal application data exchange.

## 6. TCP Flags

Common flags:

- **SYN:** synchronize sequence numbers / initiate a connection
- **ACK:** acknowledgement
- **FIN:** graceful close
- **RST:** reset
- **PSH:** request prompt delivery to the receiving application
- **URG:** urgent pointer is valid

## 7. TCP Connection Termination

A normal close uses FIN/ACK exchanges. The exact sequence depends on which endpoint initiates closure and the connection state.

## 8. UDP Datagram

UDP carries independent datagrams with minimal transport-layer overhead.

```text
Application Data
      ↓
UDP Header
      ↓
IP Packet
```

## 9. When TCP is Appropriate

TCP is useful when the application requires reliable and ordered delivery.

Examples:

- SSH
- File transfer
- Traditional web traffic
- Email protocols

## 10. When UDP is Appropriate

UDP is useful when low overhead, low latency, multicast, or application-managed reliability is preferred.

Examples:

- DNS queries
- DHCP
- NTP
- Real-time voice/video
- Some modern protocols such as QUIC

## 11. Security Considerations

Neither TCP nor UDP is inherently secure.

Security comes from higher-level protocols and controls such as:

- TLS
- Authentication
- Firewalls
- Network segmentation
- Application security

## 12. Network Analysis

For a flow such as:

```text
192.168.10.20:51542 → 203.0.113.50:443/TCP
```

TCP tells you about the transport behavior; it does not by itself tell you whether the application activity is legitimate.

## Key Takeaways

Remember:

```text
TCP → reliable, ordered, connection-oriented
UDP → lightweight, connectionless, application-managed reliability
```

Choose the protocol based on the application's communication requirements, not simply on speed or security assumptions.
