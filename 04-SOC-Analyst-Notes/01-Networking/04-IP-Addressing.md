# IP Addressing

An **IP (Internet Protocol) address** is a logical address assigned to a network interface for communication over an IP network.

IP addressing allows devices to:

* Identify communication endpoints
* Send and receive IP packets
* Communicate within a local network
* Communicate between different networks
* Participate in routed network communication

The two major versions of IP are:

* **IPv4**
* **IPv6**

This lesson focuses on the fundamentals of IP addressing. Detailed **subnetting calculations and subnet design are covered separately in the next lesson**.

---

# Table of Contents

* [What is an IP Address?](#what-is-an-ip-address)
* [Why IP Addressing is Needed](#why-ip-addressing-is-needed)
* [IPv4 and IPv6](#ipv4-and-ipv6)
* [IPv4 Address](#ipv4-address)
* [IPv4 Address Structure](#ipv4-address-structure)
* [Bits and Bytes](#bits-and-bytes)
* [IPv4 Dotted-Decimal Notation](#ipv4-dotted-decimal-notation)
* [IPv4 Binary Representation](#ipv4-binary-representation)
* [Network Portion and Host Portion](#network-portion-and-host-portion)
* [Subnet Mask](#subnet-mask)
* [CIDR Notation](#cidr-notation)
* [Prefix Length](#prefix-length)
* [Network Address](#network-address)
* [Host Address](#host-address)
* [Broadcast Address](#broadcast-address)
* [Default Gateway](#default-gateway)
* [Private IP Addresses](#private-ip-addresses)
* [Public IP Addresses](#public-ip-addresses)
* [Private vs Public IP Addresses](#private-vs-public-ip-addresses)
* [Special IPv4 Addresses](#special-ipv4-addresses)
* [Loopback Address](#loopback-address)
* [IPv4 Link-Local Address](#ipv4-link-local-address)
* [Unspecified Address](#unspecified-address)
* [Multicast Addresses](#multicast-addresses)
* [Unicast, Broadcast and Multicast](#unicast-broadcast-and-multicast)
* [Static IP Address](#static-ip-address)
* [Dynamic IP Address](#dynamic-ip-address)
* [DHCP](#dhcp)
* [IP Address Assignment Example](#ip-address-assignment-example)
* [Default Gateway and Internet Communication](#default-gateway-and-internet-communication)
* [IP Address and MAC Address](#ip-address-and-mac-address)
* [IPv4 Address Classes](#ipv4-address-classes)
* [Classful vs Classless Addressing](#classful-vs-classless-addressing)
* [IPv6 Addressing](#ipv6-addressing)
* [IPv6 Address Types](#ipv6-address-types)
* [IPv4 vs IPv6](#ipv4-vs-ipv6)
* [IP Address Information in Network Traffic](#ip-address-information-in-network-traffic)
* [Practical Examples](#practical-examples)
* [Useful Commands](#useful-commands)
* [Common Beginner Mistakes](#common-beginner-mistakes)
* [Key Takeaways](#key-takeaways)

---

# What is an IP Address?

An **IP address** is a logical address used to identify a network interface for communication over an IP network.

For example:

```text
192.168.10.20
```

A device can use its IP address to communicate with other devices.

Example:

```text
Computer A
192.168.10.20
      │
      │ IP Communication
      ▼
Computer B
192.168.10.50
```

Here:

* `192.168.10.20` is the source IP address.
* `192.168.10.50` is the destination IP address.

An IP address identifies a logical network endpoint. It is not the same as a physical MAC address.

---

# Why IP Addressing is Needed

Devices need addresses so that network traffic can be directed to the correct destination.

For example:

```text
Source:
192.168.10.20

Destination:
192.168.20.30
```

A router can examine the destination IP address and use its routing information to determine where the packet should be forwarded.

IP addressing therefore provides the foundation for:

* Logical addressing
* Packet delivery
* Routing
* Communication between networks
* Identifying source and destination endpoints

---

# IPv4 and IPv6

There are two major versions of the Internet Protocol.

## IPv4

IPv4 uses **32-bit addresses**.

Example:

```text
192.168.10.20
```

IPv4 addresses are normally written using dotted-decimal notation.

---

## IPv6

IPv6 uses **128-bit addresses**.

Example:

```text
2001:db8::1
```

IPv6 uses hexadecimal notation and provides a much larger address space than IPv4.

---

# IPv4 Address

An IPv4 address contains **32 bits**.

The 32 bits are divided into four groups of 8 bits called **octets**.

Example:

```text
192.168.10.20
```

The four octets are:

```text
192
168
10
20
```

Each octet contains 8 bits:

```text
8 + 8 + 8 + 8 = 32 bits
```

---

# IPv4 Address Structure

IPv4 addresses are written in dotted-decimal notation:

```text
192 . 168 . 10 . 20
```

Each octet can contain a value from:

```text
0 to 255
```

The reason is that an octet contains 8 bits:

```text
2^8 = 256 possible values
```

These values range from:

```text
0 through 255
```

---

# Bits and Bytes

A **bit** is the smallest unit of digital information.

It has one of two values:

```text
0
1
```

Eight bits make one byte:

```text
8 bits = 1 byte
```

An IPv4 address contains:

```text
32 bits
=
4 bytes
```

Example:

```text
192.168.10.20
```

Binary representation:

```text
11000000.10101000.00001010.00010100
```

---

# IPv4 Dotted-Decimal Notation

Humans normally use decimal notation rather than binary when working with IPv4 addresses.

Example:

```text
192.168.10.20
```

The binary equivalent is:

```text
11000000.10101000.00001010.00010100
```

Each octet represents 8 binary bits.

---

# IPv4 Binary Representation

Each IPv4 octet uses these binary place values:

```text
128 64 32 16 8 4 2 1
```

### Example: 192

```text
128 + 64 = 192
```

Binary:

```text
11000000
```

### Example: 168

```text
128 + 32 + 8 = 168
```

Binary:

```text
10101000
```

### Example: 10

```text
8 + 2 = 10
```

Binary:

```text
00001010
```

### Example: 20

```text
16 + 4 = 20
```

Binary:

```text
00010100
```

Therefore:

```text
192.168.10.20

=

11000000.10101000.00001010.00010100
```

Understanding binary notation will become important when learning subnetting.

---

# Network Portion and Host Portion

An IPv4 address is conceptually divided into:

```text
Network Portion + Host Portion
```

The **network portion** identifies the network.

The **host portion** identifies an interface within that network.

For example:

```text
192.168.10.20/24
```

The `/24` prefix indicates that the first 24 bits belong to the network portion.

Conceptually:

```text
Network Portion          Host Portion
192.168.10               .20
```

The exact boundaries are determined by the subnet mask or prefix length.

> Detailed subnetting and host calculations are covered in the next lesson.

---

# Subnet Mask

A **subnet mask** indicates which bits of an IPv4 address belong to the network portion and which belong to the host portion.

A common example is:

```text
255.255.255.0
```

This corresponds to:

```text
/24
```

In binary:

```text
11111111.11111111.11111111.00000000
```

The `1` bits indicate the network portion.

The `0` bits indicate the host portion.

```text
11111111.11111111.11111111.00000000
<----------- Network -----------><Host>
```

At this stage, remember only the purpose of a subnet mask. Detailed subnet calculations are covered separately.

---

# CIDR Notation

**CIDR (Classless Inter-Domain Routing)** notation represents an IP network using a prefix length.

Example:

```text
192.168.10.20/24
```

The `/24` means:

```text
24 bits = network prefix
```

Another example:

```text
10.0.0.10/8
```

means:

```text
8 bits = network prefix
```

CIDR notation is commonly used when writing:

* Host addresses
* Network addresses
* Routes
* Network ranges

---

# Prefix Length

The number after `/` is called the **prefix length**.

Examples:

```text
10.0.0.5/8
172.16.10.20/16
192.168.10.20/24
```

The prefix length tells us how many bits belong to the network portion.

For example:

```text
/24
```

means:

```text
24 network bits
```

and the remaining bits belong to the host portion.

Detailed calculations involving prefixes are intentionally covered in the subnetting lesson.

---

# Network Address

The **network address** identifies the network itself rather than a particular host.

For example:

```text
192.168.10.0/24
```

Here:

```text
192.168.10.0
```

represents the network.

It is not normally assigned to an individual host in a traditional IPv4 subnet.

The relationship can be visualized as:

```text
Network
192.168.10.0/24
    │
    ├── Host
    ├── Host
    ├── Host
    └── Host
```

---

# Host Address

A **host address** identifies an individual interface within a network.

Example:

```text
192.168.10.20
```

If the network is:

```text
192.168.10.0/24
```

then:

```text
192.168.10.20
```

can be assigned to a host.

Examples:

```text
192.168.10.20 → Workstation
192.168.10.30 → Laptop
192.168.10.50 → Server
```

---

# Broadcast Address

An IPv4 **broadcast address** is used to send traffic to all hosts within the relevant broadcast domain.

For:

```text
192.168.10.0/24
```

the broadcast address is:

```text
192.168.10.255
```

For a traditional `/24` IPv4 subnet:

```text
Network Address:
192.168.10.0

Host Addresses:
192.168.10.1 - 192.168.10.254

Broadcast Address:
192.168.10.255
```

The detailed process for calculating network and broadcast addresses will be covered in subnetting.

---

# Default Gateway

A **default gateway** is normally the router interface that a host uses to reach destinations outside its local IP network.

Example:

```text
PC
IP:      192.168.10.20
Gateway: 192.168.10.1
```

Network:

```text
          Router
       192.168.10.1
             │
             ▼
        Local Network
             │
        ┌────┼────┐
        │    │    │
       PC   PC  Server
```

When a host needs to communicate with a destination outside its local network, it normally sends the packet toward the default gateway.

---

# Private IP Addresses

Private IPv4 addresses are reserved for use within private networks.

The three RFC 1918 private address ranges are:

### 10.0.0.0/8

```text
10.0.0.0 - 10.255.255.255
```

### 172.16.0.0/12

```text
172.16.0.0 - 172.31.255.255
```

### 192.168.0.0/16

```text
192.168.0.0 - 192.168.255.255
```

Examples:

```text
10.10.10.10
172.16.10.20
192.168.1.50
```

Private IP addresses are commonly used in:

* Home networks
* Office networks
* Enterprise networks
* Data centers
* Virtual labs

Private IPv4 addresses are not directly routed across the public Internet.

---

# Public IP Addresses

A **public IP address** is an address that can be used for communication across the public Internet when properly routed.

Examples include publicly assigned addresses such as:

```text
8.8.8.8
```

Public addresses may be assigned to:

* Internet-facing servers
* Routers
* Cloud services
* Public applications
* Other Internet-connected infrastructure

---

# Private vs Public IP Addresses

| Feature                        | Private IP                          | Public IP                                                 |
| ------------------------------ | ----------------------------------- | --------------------------------------------------------- |
| Main use                       | Internal networks                   | Public Internet communication                             |
| Direct public Internet routing | No                                  | Yes, when globally routable                               |
| Common examples                | `192.168.1.10`                      | `8.8.8.8`                                                 |
| Common environment             | Home / enterprise LAN               | Internet-facing systems                                   |
| NAT                            | Commonly used at network boundaries | May be used with or without NAT depending on architecture |

---

# Special IPv4 Addresses

IPv4 contains several special-purpose address ranges.

Important examples include:

* Loopback
* Link-local
* Unspecified
* Multicast
* Broadcast
* Private addresses

These addresses have specific meanings and should not be treated as ordinary host addresses.

---

# Loopback Address

The IPv4 loopback range is:

```text
127.0.0.0/8
```

The most commonly used loopback address is:

```text
127.0.0.1
```

The hostname:

```text
localhost
```

commonly resolves to a loopback address.

Loopback allows a system to communicate with itself.

Example:

```text
Application A
     │
     ▼
127.0.0.1:8080
     │
     ▼
Application B
```

Loopback communication does not require communication with another host on the physical network.

---

# IPv4 Link-Local Address

The IPv4 link-local range is:

```text
169.254.0.0/16
```

Example:

```text
169.254.20.10
```

On Windows, automatic assignment from this range is commonly known as **APIPA (Automatic Private IP Addressing)**.

This can occur when a host configured to use DHCP does not obtain a DHCP lease.

A link-local address is intended for communication on the local network link and is not used for normal Internet routing.

Possible causes of a DHCP failure include:

* DHCP server unavailable
* Network connectivity problem
* Incorrect VLAN configuration
* DHCP configuration issue
* Interface or cable problem

---

# Unspecified Address

The IPv4 unspecified address is:

```text
0.0.0.0
```

It does not represent a specific host.

Its meaning depends on context.

Examples:

### Default route

```text
0.0.0.0/0
```

represents the default IPv4 route.

### Service binding

A service may listen on:

```text
0.0.0.0
```

meaning it accepts connections on all IPv4 interfaces, depending on the application.

---

# Multicast Addresses

IPv4 multicast addresses belong to:

```text
224.0.0.0/4
```

Range:

```text
224.0.0.0 - 239.255.255.255
```

Multicast allows a sender to transmit traffic to multiple subscribed receivers.

Conceptually:

```text
             ┌── Host A
             │
Sender ──────┼── Host B
             │
             └── Host C
```

Multicast is used for applications such as:

* Streaming
* Routing protocols
* Service discovery
* Group communication

---

# Unicast, Broadcast and Multicast

These terms describe traffic delivery patterns.

## Unicast

One sender communicates with one receiver.

```text
Host A ─────→ Host B
```

Example:

```text
192.168.10.20 ─────→ 192.168.10.50
```

---

## Broadcast

One sender communicates with all hosts within the relevant broadcast domain.

```text
         ┌── Host B
         │
Host A ──┼── Host C
         │
         └── Host D
```

The limited IPv4 broadcast address is:

```text
255.255.255.255
```

A subnet-directed broadcast address also exists for individual IPv4 subnets.

---

## Multicast

One sender communicates with multiple subscribed receivers.

```text
             ┌── Host B
             │
Host A ──────┼── Host C
             │
             └── Host D
```

### Comparison

| Type      | Communication                        |
| --------- | ------------------------------------ |
| Unicast   | One-to-one                           |
| Broadcast | One-to-all within a broadcast domain |
| Multicast | One-to-many subscribed receivers     |

---

# Static IP Address

A **static IP address** is manually configured or deliberately reserved so that a host normally keeps the same address.

Example:

```text
IP Address:
192.168.10.20

Subnet Mask:
255.255.255.0

Default Gateway:
192.168.10.1

DNS:
192.168.10.1
```

Static addressing is commonly used for:

* Servers
* Routers
* Firewalls
* Printers
* Network infrastructure
* Management interfaces

### Advantages

* Predictable addressing
* Easier identification of infrastructure
* Useful for services that need a stable address

### Disadvantages

* Manual administration
* Configuration errors are possible
* Requires address management

---

# Dynamic IP Address

A **dynamic IP address** is assigned automatically, commonly through DHCP.

Example:

```text
Computer starts
      ↓
DHCP process
      ↓
IP address assigned
      ↓
192.168.10.25
```

Dynamic addressing is commonly used for:

* Workstations
* Laptops
* Smartphones
* Guest devices
* IoT devices

### Advantages

* Automatic configuration
* Easier administration
* Reduced manual configuration

---

# DHCP

**DHCP (Dynamic Host Configuration Protocol)** automatically provides network configuration to clients.

A DHCP server may provide:

* IP address
* Subnet mask
* Default gateway
* DNS server addresses
* Lease duration
* Other network parameters

A common way to remember the DHCP process is:

```text
D — Discover
O — Offer
R — Request
A — Acknowledge
```

### DHCP process

```text
Client                         DHCP Server

DHCP Discover ───────────────→

          ←────────────── DHCP Offer

DHCP Request ─────────────────→

          ←──────────── DHCP ACK
```

The client can then configure itself using the supplied settings.

---

# IP Address Assignment Example

Suppose a local network uses:

```text
Network:
192.168.10.0/24
```

A router uses:

```text
192.168.10.1
```

A workstation is configured as:

```text
IP Address:
192.168.10.20

Subnet Mask:
255.255.255.0

Default Gateway:
192.168.10.1

DNS Server:
192.168.10.1
```

A simplified topology is:

```text
              Router
           192.168.10.1
                  │
          ┌───────┼───────┐
          │       │       │
        PC-1     PC-2   Server
        .10.20   .10.30  .10.50
```

The devices shown belong to the same `/24` network.

---

# Default Gateway and Internet Communication

Consider:

```text
Host:
192.168.10.20/24

Default Gateway:
192.168.10.1

Destination:
8.8.8.8
```

The host determines that `8.8.8.8` is outside its local network.

It therefore sends the traffic toward its default gateway.

```text
PC
192.168.10.20
      │
      ▼
Gateway
192.168.10.1
      │
      ▼
Internet
      │
      ▼
8.8.8.8
```

The router then uses its routing information to forward the packet toward the destination.

---

# IP Address and MAC Address

IP addresses and MAC addresses perform different functions.

## IP Address

Used for logical addressing and routing.

Example:

```text
192.168.10.20
```

## MAC Address

Associated with a network interface and used for local link-layer communication.

Example:

```text
00:1A:2B:3C:4D:5E
```

A simplified relationship is:

```text
Application
    ↓
TCP / UDP
    ↓
IP Address
    ↓
MAC Address
    ↓
Physical Network
```

When traffic passes through a router, the Layer 2 MAC addresses normally change for each local link, while the IP packet continues toward its destination.

---

# IPv4 Address Classes

IPv4 addresses were historically divided into classes.

Although modern networks use CIDR rather than classful addressing, understanding the historical classes is useful.

## Class A

Traditional first-octet range:

```text
1 - 126
```

Traditional default mask:

```text
255.0.0.0
```

or:

```text
/8
```

---

## Class B

Traditional first-octet range:

```text
128 - 191
```

Traditional default mask:

```text
255.255.0.0
```

or:

```text
/16
```

---

## Class C

Traditional first-octet range:

```text
192 - 223
```

Traditional default mask:

```text
255.255.255.0
```

or:

```text
/24
```

---

## Class D

Range:

```text
224 - 239
```

Used for multicast.

---

## Class E

Range:

```text
240 - 255
```

Historically associated with experimental or reserved use.

### Important

Classful addressing is now largely historical. Modern IP networks primarily use **classless addressing and CIDR**.

---

# Classful vs Classless Addressing

## Classful Addressing

Historically, IPv4 networks were associated with fixed class boundaries:

```text
Class A → /8
Class B → /16
Class C → /24
```

This approach was inefficient because networks often needed sizes that did not match these fixed boundaries.

---

## Classless Addressing

Modern networking uses **CIDR**, which allows variable prefix lengths.

Examples:

```text
192.168.10.0/24
192.168.10.0/25
192.168.10.0/26
192.168.10.0/27
```

CIDR provides flexible network allocation and route aggregation.

> Detailed CIDR calculations are covered in the subnetting lesson.

---

# IPv6 Addressing

IPv6 uses **128-bit addresses**.

Example:

```text
2001:db8:0000:0000:0000:0000:0000:0001
```

This can be shortened to:

```text
2001:db8::1
```

IPv6 addresses are written in hexadecimal.

---

# IPv6 Address Types

## Global Unicast

Global unicast addresses are used for globally routable IPv6 communication.

Example:

```text
2001:db8::1
```

`2001:db8::/32` is reserved for documentation and examples, rather than real public addressing.

---

## Link-Local

IPv6 link-local addresses use:

```text
FE80::/10
```

They are used for communication on the local link.

Example:

```text
fe80::1
```

Link-local addresses are important for IPv6 neighbor and router discovery processes.

---

## Unique Local Address

IPv6 unique-local addresses use:

```text
FC00::/7
```

In practice, locally assigned addresses commonly begin with:

```text
FD
```

These are intended for private internal communication.

---

## Multicast

IPv6 multicast addresses use:

```text
FF00::/8
```

IPv6 does not use IPv4-style broadcast addressing.

---

# IPv4 vs IPv6

| Feature            | IPv4             | IPv6            |
| ------------------ | ---------------- | --------------- |
| Address size       | 32 bits          | 128 bits        |
| Example            | `192.168.10.20`  | `2001:db8::1`   |
| Notation           | Dotted decimal   | Hexadecimal     |
| Broadcast          | Supported        | Not used        |
| ARP                | Used             | Not used        |
| Neighbor Discovery | No               | Yes             |
| Address space      | Smaller          | Extremely large |
| Link-local range   | `169.254.0.0/16` | `FE80::/10`     |

---

# IP Address Information in Network Traffic

Network events often contain source and destination IP information.

Example:

```text
Source IP:        192.168.10.20
Destination IP:   203.0.113.50
Protocol:         TCP
Source Port:      51542
Destination Port: 443
```

The IP information tells us:

```text
Source:
192.168.10.20

Destination:
203.0.113.50
```

The transport information tells us:

```text
Protocol:
TCP

Destination Port:
443
```

The combination provides a basic description of the communication.

---

# Practical Examples

## Example 1 — Same Network

Consider:

```text
PC1:
192.168.10.20/24

PC2:
192.168.10.50/24
```

Both use the same `/24` network:

```text
192.168.10.0/24
```

A simplified topology:

```text
PC1
192.168.10.20
     │
     ▼
  Switch
     │
     ▼
PC2
192.168.10.50
```

---

## Example 2 — Different Networks

Consider:

```text
PC1:
192.168.10.20/24

Server:
192.168.20.50/24
```

The addresses belong to different IP networks.

A router is required to route traffic between them.

```text
PC1
192.168.10.20
     │
     ▼
  Router
     │
     ▼
Server
192.168.20.50
```

The detailed process of determining network boundaries will be covered in subnetting.

---

## Example 3 — Private IP to Public IP

A workstation uses:

```text
192.168.10.20
```

and communicates with:

```text
8.8.8.8
```

The private address is not directly routed across the public Internet.

A NAT device can translate the private address to a public address.

```text
192.168.10.20
      │
      ▼
   NAT Router
      │
      ▼
Public IP
      │
      ▼
Internet
      │
      ▼
8.8.8.8
```

NAT will be covered later.

---

## Example 4 — Loopback

An application connects to:

```text
127.0.0.1:8080
```

The traffic is addressed to the local host.

```text
Application A
     │
     ▼
127.0.0.1:8080
     │
     ▼
Application B
```

This is commonly used for local application testing and inter-process network communication.

---

## Example 5 — Link-Local Address

A computer configured to use DHCP fails to obtain a normal IPv4 address and receives:

```text
169.254.20.10
```

This indicates that the host has assigned itself an IPv4 link-local address.

A possible troubleshooting direction is to investigate why DHCP configuration was not successfully obtained.

---

# Useful Commands

## Windows

### Display IP configuration

```powershell
ipconfig
```

Detailed information:

```powershell
ipconfig /all
```

These commands can display:

* IPv4 address
* IPv6 address
* Subnet mask
* Default gateway
* DNS servers
* Physical address

---

### Release DHCP lease

```powershell
ipconfig /release
```

---

### Request DHCP lease

```powershell
ipconfig /renew
```

---

### View ARP cache

```powershell
arp -a
```

---

### View routing table

```powershell
route print
```

---

### Test connectivity

```powershell
ping 8.8.8.8
```

---

### Trace route

```powershell
tracert 8.8.8.8
```

---

### Perform DNS lookup

```powershell
nslookup google.com
```

---

## Linux

### View IP addresses

```bash
ip addr
```

---

### View routing table

```bash
ip route
```

---

### View neighbor information

```bash
ip neigh
```

---

### Test connectivity

```bash
ping 8.8.8.8
```

---

### Trace route

```bash
traceroute 8.8.8.8
```

---

### DNS lookup

```bash
dig google.com
```

---

# Common Beginner Mistakes

## Mistake 1: Thinking an IP address permanently identifies a physical device

An IP address is a logical address and can change.

It may change because of:

* DHCP
* Network relocation
* Configuration changes
* Virtual networking

---

## Mistake 2: Thinking every device has only one IP address

A device can have multiple:

* Network interfaces
* IPv4 addresses
* IPv6 addresses
* Virtual interfaces

Example:

```text
Physical NIC
├── IPv4: 192.168.10.20
└── IPv6: 2001:db8::20

Virtual NIC
└── IPv4: 172.16.0.10
```

---

## Mistake 3: Thinking private IP addresses are globally unique

Private IP addresses can be reused by different organizations.

For example:

```text
192.168.1.10
```

can exist in thousands of independent networks.

---

## Mistake 4: Thinking 192.168.x.x is the only private range

The RFC 1918 private ranges are:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

---

## Mistake 5: Confusing link-local addresses with private addresses

This:

```text
169.254.x.x
```

is IPv4 link-local addressing.

It is not part of the RFC 1918 private ranges.

---

## Mistake 6: Thinking 0.0.0.0 identifies a specific host

`0.0.0.0` has special meanings depending on context.

For example:

```text
0.0.0.0/0
```

represents a default route.

---

## Mistake 7: Assuming public IP means malicious

An IP being public does not make it malicious.

Likewise, a private IP does not automatically mean a system is trustworthy.

Address type describes how the address is used, not whether the activity is safe or unsafe.

---

# Quick Reference

## IPv4

```text
32 bits
4 octets
Dotted-decimal notation
```

Example:

```text
192.168.10.20
```

---

## IPv6

```text
128 bits
Hexadecimal notation
```

Example:

```text
2001:db8::1
```

---

## Private IPv4 Ranges

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

---

## Special IPv4 Addresses

```text
127.0.0.1       → Loopback
169.254.x.x     → IPv4 link-local
0.0.0.0         → Unspecified / special use
224.0.0.0/4     → Multicast
255.255.255.255 → Limited broadcast
```

---

## Address Components

```text
IP Address
    │
    ├── Network Portion
    │
    └── Host Portion
```

Example:

```text
192.168.10.20/24
────────────    ──
Network         Host
```

The exact calculations for determining the network and host boundaries are covered in subnetting.

---

# IP Addressing Cheat Sheet

| Concept         | Example          | Meaning                              |
| --------------- | ---------------- | ------------------------------------ |
| IPv4            | `192.168.10.20`  | 32-bit IP address                    |
| IPv6            | `2001:db8::1`    | 128-bit IP address                   |
| Subnet mask     | `255.255.255.0`  | Defines network/host boundary        |
| CIDR            | `/24`            | Prefix length                        |
| Network address | `192.168.10.0`   | Identifies the network               |
| Host address    | `192.168.10.20`  | Identifies an interface              |
| Broadcast       | `192.168.10.255` | IPv4 broadcast for a `/24` example   |
| Gateway         | `192.168.10.1`   | Router used to reach remote networks |
| Loopback        | `127.0.0.1`      | Local host                           |
| Link-local      | `169.254.10.20`  | IPv4 link-local address              |
| Private IP      | `192.168.1.10`   | RFC 1918 internal address            |
| Multicast       | `224.0.0.1`      | IPv4 multicast                       |

---

# Practical Learning Exercise

Use your Windows or Linux system to identify your IP configuration.

## Windows

Run:

```powershell
ipconfig /all
```

Identify:

```text
IPv4 Address:
IPv6 Address:
Subnet Mask:
Default Gateway:
DNS Server:
MAC Address:
```

Then run:

```powershell
arp -a
```

Observe the relationship between:

```text
IP Address
MAC Address
```

Next:

```powershell
route print
```

Identify:

* Local network route
* Default route
* Gateway

---

## Linux

Run:

```bash
ip addr
```

Then:

```bash
ip route
```

Then:

```bash
ip neigh
```

Identify:

```text
IP address
Prefix
Default gateway
Neighbor IP
Neighbor MAC
```

---

# Key Takeaways

1. An IP address is a **logical address** used for IP communication.
2. IPv4 uses **32-bit addresses**.
3. IPv6 uses **128-bit addresses**.
4. IPv4 addresses use **dotted-decimal notation**.
5. An IPv4 address contains four **8-bit octets**.
6. Each IPv4 octet can contain a value from `0` to `255`.
7. An IPv4 address is logically divided into a **network portion** and a **host portion**.
8. A subnet mask identifies the boundary between the network and host portions.
9. CIDR notation represents the prefix length using `/number`.
10. A network address identifies the subnet itself.
11. A host address identifies a network interface.
12. A broadcast address is used for IPv4 broadcast communication.
13. A default gateway is normally the router used to reach remote networks.
14. RFC 1918 defines three private IPv4 ranges:

* `10.0.0.0/8`
* `172.16.0.0/12`
* `192.168.0.0/16`

15. `127.0.0.1` is the commonly used IPv4 loopback address.
16. `169.254.0.0/16` is the IPv4 link-local range.
17. `224.0.0.0/4` is the IPv4 multicast range.
18. `0.0.0.0` has special meanings depending on context.
19. Static IP addresses are manually or deliberately configured.
20. Dynamic IP addresses are commonly assigned through DHCP.
21. IP addresses and MAC addresses perform different functions.
22. IPv4 classful addressing is largely historical.
23. Modern networks use classless addressing and CIDR.
24. IPv6 uses 128-bit hexadecimal addresses.
25. Detailed **subnetting calculations and subnet design belong to the next lesson**, not this one.

---

# Final Mental Model

When looking at an IP configuration, think:

```text
IP Address
     │
     ├── What network?
     │
     ├── What host?
     │
     ├── What prefix?
     │
     ├── What gateway?
     │
     └── Private or public?
```

For network communication:

```text
Source IP
     │
     ▼
Local Network
     │
     ▼
Default Gateway
     │
     ▼
Remote Network
     │
     ▼
Destination IP
```

A typical local network can be visualized as:

```text
                     Internet
                         │
                         ▼
                  Router / Gateway
                    192.168.10.1
                         │
              ┌──────────┼──────────┐
              │          │          │
            PC-1        PC-2      Server
        .192.168.10.20  .10.30   .10.50
```

IP addressing provides the logical foundation required to understand **subnetting, routing, NAT, DHCP, DNS, firewall rules, and network traffic analysis**.

## Next Lesson

**05 — Subnetting**

The next lesson covers:

* Binary subnetting
* Subnet masks in detail
* CIDR calculations
* Network and broadcast calculation
* Usable host ranges
* Number of subnets
* Number of hosts
* `/25` through `/30`
* Subnetting practice
* VLSM
* Real-world subnet design
