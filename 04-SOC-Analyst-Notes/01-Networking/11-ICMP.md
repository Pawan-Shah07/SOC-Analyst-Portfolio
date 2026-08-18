# ICMP

## 1. Overview

**Internet Control Message Protocol (ICMP)** provides error reporting, diagnostics, and network control messages for IP networks.

ICMP is carried within IP packets and does not use TCP or UDP ports.

## 2. Common Uses

ICMP is used for:

- Connectivity testing
- Error reporting
- Path diagnostics
- Path MTU-related messaging

## 3. Echo Request and Echo Reply

The familiar `ping` utility commonly uses ICMP Echo Request and Echo Reply messages.

```text
Host A ── Echo Request ──→ Host B
Host A ←── Echo Reply ──── Host B
```

## 4. Common IPv4 ICMP Types

Important examples include:

- Type 0 — Echo Reply
- Type 3 — Destination Unreachable
- Type 5 — Redirect
- Type 8 — Echo Request
- Type 11 — Time Exceeded

## 5. Destination Unreachable

A destination-unreachable message may indicate conditions such as:

- Network unreachable
- Host unreachable
- Protocol unreachable
- Port unreachable
- Fragmentation-related conditions in some cases

## 6. Time Exceeded

Routers decrement the IP TTL. If a packet's TTL reaches zero, an ICMP Time Exceeded message can be generated.

This mechanism is used by tools such as `traceroute` and `tracert`.

## 7. ICMP and Traceroute

A typical traceroute technique relies on deliberately varying TTL values to identify intermediate hops.

```text
TTL 1 → Router 1 responds
TTL 2 → Router 2 responds
TTL 3 → Router 3 responds
```

Exact behavior differs by operating system and traceroute implementation.

## 8. ICMPv6

IPv6 uses **ICMPv6** for diagnostics and important control functions, including Neighbor Discovery.

## 9. Security Considerations

ICMP can be abused for:

- Reconnaissance
- Flooding
- Tunneling
- Covert communication
- Network mapping

However, blocking all ICMP is not generally a sound design. Some ICMP/ICMPv6 messages are important for correct network operation.

## 10. Useful Commands

Windows:

```powershell
ping 8.8.8.8
tracert 8.8.8.8
```

Linux:

```bash
ping 8.8.8.8
traceroute 8.8.8.8
```

## Key Takeaways

ICMP supports IP diagnostics and control. Learn the common message types, understand why ping and traceroute work, and avoid treating ICMP as a transport protocol with ports.
