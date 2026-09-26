# NAT

## 1. Overview

**Network Address Translation (NAT)** changes IP address and, in some forms, transport-port information as traffic crosses a network boundary.

NAT is commonly used at IPv4 network edges, especially where private addresses communicate with the public Internet.

## 2. Why NAT is Used

Common reasons include:

- Allowing private addresses to access the Internet
- Conserving public IPv4 addresses
- Hiding internal addressing details from direct Internet routing
- Publishing selected internal services

NAT is not, by itself, a complete security control.

## 3. Common NAT Types

### Static NAT
One private address maps to one public address.

### Dynamic NAT
Private addresses are translated to an address from a public pool.

### PAT / NAT Overload
Many internal hosts share one or a small number of public addresses using different transport ports.

## 4. PAT Example

```text
192.168.10.20:51542 ─┐
                     ├─ NAT ─→ Public-IP:40001
192.168.10.30:51543 ─┘          Public-IP:40002
```

The NAT device maintains a translation state so replies can be associated with the correct internal flow.

## 5. Source NAT

**SNAT** changes the source address of a connection.

Typical outbound example:

```text
Private Host → NAT Gateway → Internet
```

## 6. Destination NAT

**DNAT** changes the destination address.

It is commonly used to publish an internal service through a public address/port.

```text
Internet → Public IP:443 → DNAT → Internal Server:443
```

## 7. Port Forwarding

Port forwarding is a common DNAT use.

Example:

```text
203.0.113.10:443
        ↓
192.168.10.50:443
```

## 8. NAT and Logging

A useful NAT log can contain:

- Original source IP/port
- Translated source IP/port
- Destination IP/port
- Protocol
- Timestamp

Translation logs are important when correlating external activity to an internal host.

## 9. NAT Limitations

NAT can complicate:

- End-to-end addressing
- Troubleshooting
- Some peer-to-peer applications
- Certain protocols that embed IP addresses or ports in payloads

## 10. NAT vs Firewall

NAT changes addressing. A firewall applies traffic policy. A device can perform both functions, but they are conceptually different.

## 11. NAT in a Home/Virtual Lab

Typical flow:

```text
Private LAN
192.168.10.0/24
        ↓
Firewall/NAT
        ↓
Public/Upstream Network
```

## Key Takeaways

Know **SNAT, DNAT, PAT, port forwarding, translation state, and NAT logs**. Do not treat NAT as equivalent to firewall security.
