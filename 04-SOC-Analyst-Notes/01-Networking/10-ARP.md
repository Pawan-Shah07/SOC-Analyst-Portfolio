# ARP

## 1. Overview

**Address Resolution Protocol (ARP)** is used by IPv4 hosts on local networks to determine the MAC address associated with a known IPv4 address.

ARP is relevant when a host needs to place an IPv4 packet into an Ethernet frame for a local next hop.

## 2. Why ARP is Needed

IP uses logical addresses, while Ethernet uses MAC addresses.

A host may know:

```text
Destination IP: 192.168.10.50
```

but need the corresponding MAC address before sending the Ethernet frame.

## 3. ARP Request

The sender broadcasts an ARP request:

```text
Who has 192.168.10.50?
```

## 4. ARP Reply

The owner replies with its MAC address:

```text
192.168.10.50 is at AA:BB:CC:DD:EE:FF
```

## 5. ARP Cache

Hosts store learned mappings in an ARP cache for a period of time.

Example concept:

```text
192.168.10.50 → AA:BB:CC:DD:EE:FF
```

## 6. ARP and the Default Gateway

If a host needs to reach a remote IP network, it usually resolves the MAC address of the **default gateway**, not the remote server's MAC address.

```text
Host → Gateway MAC → Router → Remote Network
```

## 7. ARP Commands

Windows:

```powershell
arp -a
```

Linux:

```bash
ip neigh
```

## 8. ARP Spoofing

In **ARP spoofing/poisoning**, an attacker sends forged ARP information to influence a victim's IP-to-MAC mapping.

Potential consequences include:

- Man-in-the-middle positioning
- Traffic interception
- Traffic disruption
- Redirection

## 9. Limitations of ARP

ARP is an IPv4 mechanism. IPv6 uses **Neighbor Discovery Protocol (NDP)** instead.

## 10. Security Controls

Managed switches may provide controls such as:

- DHCP snooping
- Dynamic ARP Inspection
- Port security
- VLAN segmentation

The exact implementation depends on the vendor and network architecture.

## Key Takeaways

Remember:

```text
IPv4 address → ARP → MAC address
```

ARP is local-link behavior. Routers do not normally forward ARP broadcasts between networks.
