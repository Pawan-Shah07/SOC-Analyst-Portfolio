# Subnetting

## 1. Overview

**Subnetting** divides a larger IPv4 network into smaller logical networks called subnets.

Subnetting is based on:

```text
32-bit IPv4 address
+
Subnet mask / prefix
+
Borrowed host bits
=
Smaller networks
```

## 2. Why Subnetting is Used

Subnetting helps organizations:

- Create logical network boundaries
- Reduce broadcast-domain size
- Organize addresses
- Allocate capacity according to requirements
- Support routing design
- Improve network segmentation

## 3. Core Terms

- **Prefix length:** number of network bits.
- **Host bits:** bits available for host addressing.
- **Network address:** first address of a subnet.
- **Broadcast address:** last address of a traditional IPv4 subnet.
- **Usable host range:** addresses between network and broadcast.
- **Block size:** increment used to identify subnet boundaries.

## 4. Core Formulas

```text
Host Bits = 32 - Prefix Length

Total Addresses = 2^Host Bits

Traditional Usable Hosts = 2^Host Bits - 2

Subnets Created = 2^Borrowed Bits

Block Size = 256 - Interesting Mask Octet
```

The `-2` host rule is the traditional calculation for ordinary IPv4 subnets where the network and broadcast addresses are reserved.

## 5. /24 to /25

```text
Borrowed bits = 1
Subnets = 2
Host bits = 7
Total addresses/subnet = 128
Usable hosts/subnet = 126
Mask = 255.255.255.128
```

Subnets:

```text
192.168.10.0/25
192.168.10.128/25
```

## 6. /24 to /26

```text
Borrowed bits = 2
Subnets = 4
Host bits = 6
Total addresses = 64
Usable hosts = 62
Mask = 255.255.255.192
Block size = 64
```

Boundaries:

```text
0, 64, 128, 192
```

## 7. /24 to /27

```text
Borrowed bits = 3
Subnets = 8
Host bits = 5
Total addresses = 32
Usable hosts = 30
Mask = 255.255.255.224
Block size = 32
```

Boundaries:

```text
0, 32, 64, 96, 128, 160, 192, 224
```

## 8. /24 to /28

```text
Borrowed bits = 4
Subnets = 16
Host bits = 4
Total addresses = 16
Usable hosts = 14
Mask = 255.255.255.240
Block size = 16
```

## 9. /24 to /29

```text
Borrowed bits = 5
Subnets = 32
Host bits = 3
Total addresses = 8
Usable hosts = 6
Mask = 255.255.255.248
Block size = 8
```

## 10. /24 to /30

```text
Borrowed bits = 6
Subnets = 64
Host bits = 2
Total addresses = 4
Usable hosts = 2
Mask = 255.255.255.252
Block size = 4
```

## 11. Finding a Subnet from an IP

Example:

```text
192.168.10.77/26
```

Mask:

```text
255.255.255.192
```

Block size:

```text
256 - 192 = 64
```

Boundaries:

```text
0, 64, 128, 192
```

`77` falls in `64–127`.

Therefore:

```text
Network:   192.168.10.64
Broadcast: 192.168.10.127
Hosts:     192.168.10.65–192.168.10.126
```

## 12. Subnetting Beyond the Fourth-Octet Examples

For `172.16.0.0/20`:

```text
Mask = 255.255.240.0
Interesting octet = third octet
Block size = 16
```

The first subnet is:

```text
172.16.0.0/20
```

The next begins at:

```text
172.16.16.0/20
```

The first subnet's broadcast is:

```text
172.16.15.255
```

## 13. Required Hosts

To support a required number of hosts, find the smallest `h` for which:

```text
2^h - 2 >= required hosts
```

Example: 50 hosts.

```text
2^5 - 2 = 30  → insufficient
2^6 - 2 = 62  → sufficient
```

Therefore:

```text
Host bits = 6
Prefix = 32 - 6 = /26
```

## 14. Required Number of Subnets

Find the smallest `n` for which:

```text
2^n >= required subnets
```

Example: 10 subnets.

```text
2^3 = 8   → insufficient
2^4 = 16  → sufficient
```

From `/24`:

```text
24 + 4 = /28
```

## 15. VLSM

**Variable Length Subnet Masking (VLSM)** allows different subnet sizes in one address space.

Example requirements:

```text
100 hosts → /25
50 hosts  → /26
20 hosts  → /27
10 hosts  → /28
```

A good design practice is to allocate the largest requirement first.

## 16. VLSM Example

Starting network:

```text
192.168.10.0/24
```

Allocation:

```text
100 hosts → 192.168.10.0/25
50 hosts  → 192.168.10.128/26
20 hosts  → 192.168.10.192/27
10 hosts  → 192.168.10.224/28
```

The remaining range is reserved for future use.

## 17. Route Summarization

Several contiguous routes can sometimes be represented by a summary prefix.

Example:

```text
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

can summarize to:

```text
192.168.0.0/22
```

when alignment and contiguity requirements are satisfied.

## 18. Quick Reference

| Prefix | Mask | Total | Usable | Block |
|---:|---|---:|---:|---:|
| /24 | 255.255.255.0 | 256 | 254 | 256 |
| /25 | 255.255.255.128 | 128 | 126 | 128 |
| /26 | 255.255.255.192 | 64 | 62 | 64 |
| /27 | 255.255.255.224 | 32 | 30 | 32 |
| /28 | 255.255.255.240 | 16 | 14 | 16 |
| /29 | 255.255.255.248 | 8 | 6 | 8 |
| /30 | 255.255.255.252 | 4 | 2 | 4 |

## 19. Practical Exercises

1. Find the network, broadcast, and host range for `192.168.1.77/26`.
2. Choose a prefix for 100 hosts.
3. Choose a prefix for 12 hosts.
4. Divide `192.168.50.0/24` into 8 equal subnets.
5. Design a VLSM plan for 100, 50, 20, and 10 hosts.

## Key Takeaways

Subnetting is about **prefix length, host bits, address capacity, subnet boundaries, and requirements**. The fastest practical method is to identify the mask, calculate the block size, locate the subnet boundary, and then determine network, broadcast, and usable host addresses.
