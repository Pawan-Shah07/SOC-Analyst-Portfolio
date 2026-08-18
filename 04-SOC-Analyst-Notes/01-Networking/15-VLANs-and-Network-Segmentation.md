# VLANs and Network Segmentation

## 1. Overview

A **VLAN (Virtual Local Area Network)** logically separates devices into distinct Layer 2 networks on shared switching infrastructure.

VLANs are commonly used to organize users, servers, voice devices, management interfaces, and other systems.

## 2. Why VLANs are Used

VLANs can provide:

- Logical separation
- Smaller broadcast domains
- Better organizational structure
- Easier network policy enforcement
- Support for security segmentation

A VLAN is not automatically a security boundary until traffic between VLANs is controlled.

## 3. Example

```text
VLAN 10 → Users
VLAN 20 → Servers
VLAN 30 → Management
VLAN 40 → Guest
```

```text
             Switch
        ┌──────┼──────┐
       VLAN10 VLAN20 VLAN30
```

## 4. Access Ports

An access port normally carries traffic for one VLAN toward an endpoint.

Example:

```text
PC → Access Port → VLAN 10
```

## 5. Trunk Ports

A trunk carries traffic for multiple VLANs between network devices using VLAN tagging.

802.1Q is the common VLAN tagging standard for Ethernet trunks.

```text
Switch A ===== Trunk ===== Switch B
           VLAN 10,20,30
```

## 6. Inter-VLAN Routing

Devices in different VLANs require Layer 3 routing to communicate.

```text
VLAN 10
   ↓
Layer 3 Gateway
   ↓
VLAN 20
```

Routing can be provided by:

- Router-on-a-stick
- Layer 3 switch
- Firewall

## 7. Segmentation vs VLAN

A VLAN provides logical Layer 2 separation. **Network segmentation** is the broader design practice of limiting communication between systems or groups.

Segmentation can use:

- VLANs
- Firewalls
- Routing policies
- Security groups
- ACLs
- Microsegmentation

## 8. Example Enterprise Segmentation

```text
Internet
   ↓
Firewall
   ├── DMZ
   ├── User VLANs
   ├── Server VLANs
   ├── Management VLAN
   └── Guest VLAN
```

## 9. Security Principles

Good segmentation follows least privilege:

```text
Users → allowed business services only
Servers → required application paths only
Management → restricted administrative access
Guest → Internet only
```

## 10. Common VLAN Problems

- Incorrect VLAN assignment
- Native VLAN mismatch
- Trunk allowed-VLAN mismatch
- Incorrect inter-VLAN gateway
- DHCP scope mismatch
- Routing or firewall policy errors

## Key Takeaways

VLANs separate Layer 2 broadcast domains, while segmentation controls communication between logical groups. Strong designs combine VLANs with Layer 3 routing and security policy.
