# Routing

## 1. Overview

**Routing** is the process of determining how IP packets move between networks.

A router uses a **routing table** to choose a next hop or outgoing interface.

## 2. Local vs Remote Destinations

A host first determines whether the destination is on its local network. If the destination is remote, the host normally forwards traffic to its default gateway.

```text
Local destination → local link
Remote destination → default gateway
```

## 3. Routing Table

A route generally contains information such as:

- Destination prefix
- Next hop
- Outgoing interface
- Metric/cost
- Route source

Example concept:

```text
Destination      Next Hop      Interface
192.168.10.0/24  On-link       LAN
0.0.0.0/0        192.168.10.1  LAN
```

## 4. Default Route

A default IPv4 route is commonly represented as:

```text
0.0.0.0/0
```

It matches destinations that do not have a more specific route.

## 5. Longest Prefix Match

When multiple routes match a destination, routers generally choose the route with the **longest matching prefix**.

Example:

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```

For `10.10.10.25`, the `/24` route is the most specific match.

## 6. Static Routing

A static route is manually configured.

Advantages:

- Predictable
- Simple for small designs
- No routing protocol overhead

Disadvantages:

- Manual maintenance
- Poor scalability
- Higher risk of configuration errors in large networks

## 7. Dynamic Routing

Dynamic routing protocols exchange route information automatically.

Examples:

- OSPF
- BGP
- RIP
- EIGRP in environments that support it

## 8. Interior vs Exterior Routing

### IGP
Used within an administrative domain.

Examples:

- OSPF
- IS-IS
- RIP

### EGP
Used between administrative domains. **BGP** is the major inter-domain routing protocol on the Internet.

## 9. Administrative Distance and Metrics

Routing platforms use protocol-specific metrics and selection rules to determine preferred routes. Administrative distance is commonly used by many vendors to compare routes learned from different routing sources.

These values are implementation-specific; always consult vendor documentation for exact behavior.

## 10. Routing Example

```text
LAN A
192.168.10.0/24
    │
    ▼
Router R1
    │
    ▼
Router R2
    │
    ▼
LAN B
192.168.20.0/24
```

R1 needs a route toward `192.168.20.0/24`, and R2 needs a return route toward `192.168.10.0/24`.

## 11. Asymmetric Routing

Traffic can travel through different paths in each direction.

```text
A → B: Path 1
B → A: Path 2
```

This is called **asymmetric routing** and can affect troubleshooting, stateful firewalls, and traffic monitoring.

## 12. Useful Commands

Windows:

```powershell
route print
tracert 8.8.8.8
```

Linux:

```bash
ip route
traceroute 8.8.8.8
```

## Key Takeaways

Understand routing tables, default routes, longest-prefix matching, static vs dynamic routing, route selection, and the need for a return path.
