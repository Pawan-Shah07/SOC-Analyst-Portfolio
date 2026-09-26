# DHCP

## 1. Overview

**Dynamic Host Configuration Protocol (DHCP)** automatically provides network configuration to clients.

A DHCP service can provide:

- IP address
- Subnet mask/prefix
- Default gateway
- DNS servers
- Lease duration
- Other DHCP options

## 2. DHCP Lease Concept

A client normally receives an address for a defined lease period rather than owning the address permanently.

```text
Client requests configuration
        ↓
DHCP server offers a lease
        ↓
Client requests the offer
        ↓
Server acknowledges
```

## 3. DORA Process

The classic IPv4 DHCP exchange is remembered as **DORA**:

```text
Discover
Offer
Request
Acknowledge
```

```text
Client                     Server
  │
  │ DHCP Discover
  ├───────────────────────→
  │
  │        DHCP Offer
  │←───────────────────────
  │
  │ DHCP Request
  ├───────────────────────→
  │
  │        DHCP ACK
  │←───────────────────────
```

## 4. DHCP Ports

DHCP for IPv4 uses:

```text
UDP 67 → Server
UDP 68 → Client
```

The initial exchange can use broadcast traffic because the client may not yet have a usable IP address.

## 5. Lease Renewal

DHCP clients renew leases before they expire. The exact renewal behavior follows the DHCP lease timers and protocol state machine.

## 6. DHCP Scope

A DHCP scope is the pool of addresses a server can allocate, along with associated options and policies.

Example concept:

```text
Scope: 192.168.10.0/24
Pool: 192.168.10.100 – 192.168.10.200
Gateway: 192.168.10.1
DNS: 192.168.10.1
```

## 7. Reservations

A DHCP reservation associates a specific client identifier, commonly a MAC address in simple environments, with a predictable IP lease.

Reservations are useful for devices that should use DHCP but still receive stable addressing.

## 8. DHCP Relay

Routers normally do not forward local DHCP broadcasts. A **DHCP relay** forwards DHCP messages between clients and a DHCP server on another network.

```text
Client LAN
   ↓
DHCP Relay / Router
   ↓
DHCP Server
```

## 9. APIPA / IPv4 Link-Local

If a Windows client using DHCP cannot obtain a lease, it may automatically assign an IPv4 link-local address in:

```text
169.254.0.0/16
```

This is a useful troubleshooting clue.

## 10. DHCP Security Concerns

Common threats include:

- Rogue DHCP server
- DHCP starvation
- Malicious configuration
- Unauthorized network access

Switch protections such as DHCP snooping can help in managed environments.

## 11. Troubleshooting Commands

Windows:

```powershell
ipconfig /all
ipconfig /release
ipconfig /renew
```

Linux:

```bash
ip addr
ip route
journalctl -u NetworkManager
```

The exact DHCP client tools vary by Linux distribution.

## Key Takeaways

DHCP automates network configuration. Know **DORA, UDP 67/68, scopes, leases, reservations, relay, link-local addressing, and common DHCP failures**.
