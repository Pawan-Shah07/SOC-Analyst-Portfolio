# IP Addressing

## 1. Overview

An **IP address** is a logical address associated with a network interface for communication over an IP network.

This lesson introduces IPv4 and IPv6 addressing concepts. Detailed subnet calculations are covered separately in `05-Subnetting.md`.

## 2. IPv4

IPv4 uses 32-bit addresses written as four decimal octets.

Example:

```text
192.168.10.20
```

Each octet is 8 bits and ranges from 0 to 255.

## 3. IPv6

IPv6 uses 128-bit hexadecimal addresses.

Example:

```text
2001:db8::1
```

## 4. Network and Host Portions

An IPv4 address is conceptually divided into a network portion and a host portion. The boundary is defined by the subnet mask or CIDR prefix.

Example:

```text
192.168.10.20/24
```

The `/24` means the first 24 bits form the network prefix.

> Detailed subnetting calculations and subnet design are covered in `05-Subnetting.md`.

## 5. Subnet Mask

A subnet mask identifies the network/host boundary.

Example:

```text
255.255.255.0 = /24
```

The binary representation is:

```text
11111111.11111111.11111111.00000000
```

## 6. CIDR and Prefix Length

CIDR writes the network prefix as `/number`.

Examples:

```text
10.0.0.5/8
172.16.10.20/16
192.168.10.20/24
```

The detailed mathematics of prefix lengths belongs to subnetting.

## 7. Network, Host, and Broadcast Addresses

A **network address** identifies the subnet. A **host address** identifies a specific interface. A traditional IPv4 subnet also has a **broadcast address** used to reach all hosts in the broadcast domain.

Example for `192.168.10.0/24`:

```text
Network:   192.168.10.0
Host:      192.168.10.20
Broadcast: 192.168.10.255
```

## 8. Default Gateway

A default gateway is normally the router used to reach destinations outside the local IP network.

Example:

```text
Host:    192.168.10.20
Gateway: 192.168.10.1
```

## 9. Private IPv4 Ranges

RFC 1918 private ranges are:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

They are intended for private networks and are not directly routed on the public Internet.

## 10. Public IP Addresses

Publicly routable IP addresses are used for Internet communication when properly allocated and routed.

## 11. Special IPv4 Addresses

- `127.0.0.0/8` — loopback
- `169.254.0.0/16` — IPv4 link-local
- `0.0.0.0` — unspecified/special context
- `224.0.0.0/4` — multicast
- `255.255.255.255` — limited broadcast

## 12. Static vs Dynamic Addressing

### Static
Manually configured or reserved so the host normally retains the same address.

### Dynamic
Automatically assigned, commonly by DHCP.

## 13. DHCP Relationship

DHCP can provide:

- IP address
- Subnet mask
- Default gateway
- DNS servers
- Lease information

Detailed DHCP behavior is covered in `09-DHCP.md`.

## 14. IP vs MAC

```text
IP  → logical, routed addressing
MAC → local-link addressing
```

## 15. IPv4 Classes

Traditional classes are useful historically:

| Class | First Octet | Default Prefix |
|---|---|---:|
| A | 1–126 | /8 |
| B | 128–191 | /16 |
| C | 192–223 | /24 |
| D | 224–239 | Multicast |
| E | 240–255 | Reserved/experimental |

Modern networks use classless addressing and CIDR.

## 16. IPv6 Address Types

Common IPv6 concepts include:

- Global unicast
- Link-local `FE80::/10`
- Unique local `FC00::/7`
- Multicast `FF00::/8`

IPv6 does not use IPv4-style broadcast addressing.

## 17. Useful Commands

Windows:

```powershell
ipconfig /all
arp -a
route print
ping 8.8.8.8
```

Linux:

```bash
ip addr
ip route
ip neigh
ping 8.8.8.8
```

## Key Takeaways

Understand what an IP address is, how IPv4 and IPv6 are represented, the purpose of prefixes and gateways, the difference between private and public addressing, and the major special address ranges. Save all detailed subnet mathematics for the next lesson.
