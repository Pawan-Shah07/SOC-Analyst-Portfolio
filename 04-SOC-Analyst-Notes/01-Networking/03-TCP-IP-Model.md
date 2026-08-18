# TCP/IP Model

The **TCP/IP model** is a conceptual and practical framework used to describe how devices communicate across modern IP-based networks, including the Internet.

TCP/IP stands for **Transmission Control Protocol / Internet Protocol**.

Unlike the OSI model, which contains seven layers, the commonly taught TCP/IP model contains **four layers**:

```text
+-----------------------------+
| 4. Application              |
+-----------------------------+
| 3. Transport                |
+-----------------------------+
| 2. Internet                 |
+-----------------------------+
| 1. Network Access           |
+-----------------------------+
```

The four layers are:

1. **Application Layer**
2. **Transport Layer**
3. **Internet Layer**
4. **Network Access Layer**

The TCP/IP model is closely associated with the actual protocols used to communicate across IP networks.

---

# Table of Contents

* [What is the TCP/IP Model?](#what-is-the-tcpip-model)
* [Why is the TCP/IP Model Important?](#why-is-the-tcpip-model-important)
* [TCP/IP Model Layers](#tcpip-model-layers)

  * [Layer 4 — Application](#layer-4--application)
  * [Layer 3 — Transport](#layer-3--transport)
  * [Layer 2 — Internet](#layer-2--internet)
  * [Layer 1 — Network Access](#layer-1--network-access)
* [TCP/IP Layer Summary](#tcpip-layer-summary)
* [Application Layer](#application-layer)
* [Transport Layer](#transport-layer)
* [Internet Layer](#internet-layer)
* [Network Access Layer](#network-access-layer)
* [TCP](#tcp)
* [UDP](#udp)
* [TCP Three-Way Handshake](#tcp-three-way-handshake)
* [TCP Connection Termination](#tcp-connection-termination)
* [Ports and Sockets](#ports-and-sockets)
* [IP and the Internet Layer](#ip-and-the-internet-layer)
* [IPv4](#ipv4)
* [IPv6](#ipv6)
* [ICMP](#icmp)
* [ARP and Neighbor Discovery](#arp-and-neighbor-discovery)
* [Ethernet and Wi-Fi](#ethernet-and-wi-fi)
* [Encapsulation in TCP/IP](#encapsulation-in-tcpip)
* [De-encapsulation](#de-encapsulation)
* [Example: Accessing a Website](#example-accessing-a-website)
* [Example: DNS Resolution](#example-dns-resolution)
* [Example: Ping](#example-ping)
* [TCP/IP Model and OSI Model](#tcpip-model-and-osi-model)
* [TCP/IP vs OSI Layer Mapping](#tcpip-vs-osi-layer-mapping)
* [Network Devices and TCP/IP Layers](#network-devices-and-tcpip-layers)
* [Network Traffic Flow](#network-traffic-flow)
* [Layer-by-Layer Troubleshooting](#layer-by-layer-troubleshooting)
* [Common Protocols by TCP/IP Layer](#common-protocols-by-tcpip-layer)
* [Common Beginner Mistakes](#common-beginner-mistakes)
* [Practical Examples](#practical-examples)
* [Useful Commands](#useful-commands)
* [Key Takeaways](#key-takeaways)

---

# What is the TCP/IP Model?

The **TCP/IP model** is a framework used to explain how network communication occurs between devices using the Internet Protocol Suite.

It organizes communication into four broad layers.

```text
Sender                                      Receiver

Application  ────────────────────────────  Application
Transport    ────────────────────────────  Transport
Internet     ────────────────────────────  Internet
Network Access      ────────────────────────────  Network Access
                                      
```

The data does not physically travel directly from one layer to the same layer on another system.

Instead:

```text
Sender
   ↓
Application
   ↓
Transport
   ↓
Internet
   ↓
Network Access
   ↓
Network
   ↓
Network Access
   ↓
Internet
   ↓
Transport
   ↓
Application
Receiver
```

Each layer performs specific functions and relies on the layer below it.

---

# Why is the TCP/IP Model Important?

The TCP/IP model is important because it describes the architecture behind modern IP networking.

It helps explain:

* How applications communicate
* How data is transported
* How IP addresses are used
* How routers forward packets
* How hosts communicate on local networks
* How different protocols work together
* How data is encapsulated
* How network problems can be isolated

The Internet itself relies on the **Internet Protocol Suite**, which includes protocols such as:

* IP
* TCP
* UDP
* ICMP
* DNS
* HTTP
* HTTPS
* DHCP
* ARP
* BGP
* SMTP

The TCP/IP model groups these protocols according to their functions.

---

# TCP/IP Model Layers

The four commonly taught layers are:

| Layer | Name           | Main Function                                |
| ----: | -------------- | -------------------------------------------- |
|     4 | Application    | Provides network services to applications    |
|     3 | Transport      | Provides process-to-process transport        |
|     2 | Internet       | Provides logical addressing and routing      |
|     1 | Network Access | Provides local network and physical delivery |

A useful way to remember the order from top to bottom is:

> **Application → Transport → Internet → Network Access**

---

# Layer 4 — Application

## Overview

The **Application Layer** is the top layer of the TCP/IP model.

It provides network services used directly by applications.

The TCP/IP Application Layer combines functions that are represented by three layers in the OSI model:

```text
OSI Layer 7 → Application
OSI Layer 6 → Presentation
OSI Layer 5 → Session
                ↓
        TCP/IP Application
```

This means that application-level communication, data representation, and session-related functions are generally handled within the broader TCP/IP Application Layer.

---

## Common Application Layer Protocols

| Protocol | Purpose                          |
| -------- | -------------------------------- |
| HTTP     | Web communication                |
| HTTPS    | Secure web communication         |
| DNS      | Domain name resolution           |
| DHCP     | Dynamic network configuration    |
| SMTP     | Sending email                    |
| IMAP     | Accessing email                  |
| POP3     | Retrieving email                 |
| FTP      | File transfer                    |
| SSH      | Secure remote access             |
| Telnet   | Remote access without encryption |
| SNMP     | Network management               |
| NTP      | Time synchronization             |
| SMB      | File and printer sharing         |

---

## Example

When a user opens:

```text
https://example.com
```

the browser uses an application-layer protocol such as HTTPS.

Conceptually:

```text
Web Browser
     │
     │ HTTPS
     ▼
Web Server
```

The Application Layer is responsible for the communication rules used by the application.

---

# Layer 3 — Transport

## Overview

The **Transport Layer** provides communication between processes running on systems.

Its major protocols are:

* TCP
* UDP

Transport protocols use **port numbers** to identify application or service endpoints.

For example:

```text
192.168.10.20:443
```

Here:

* `192.168.10.20` = IP address
* `443` = destination port

---

## Main Functions of the Transport Layer

The Transport Layer may provide:

* Process-to-process communication
* Segmentation
* Reassembly
* Port addressing
* Reliability
* Flow control
* Error recovery
* Multiplexing

The exact services depend on whether TCP or UDP is used.

---

# TCP

**TCP (Transmission Control Protocol)** is a connection-oriented transport protocol.

TCP provides reliable, ordered delivery.

### Important TCP features

* Connection establishment
* Sequence numbers
* Acknowledgments
* Retransmission
* Flow control
* Ordered delivery
* Connection termination

TCP is commonly used by:

* HTTPS
* HTTP/1.1 and HTTP/2
* SSH
* FTP
* SMTP
* IMAP

---

# UDP

**UDP (User Datagram Protocol)** is a connectionless transport protocol.

UDP has lower overhead than TCP and does not provide TCP-style reliability.

### UDP characteristics

* Connectionless
* No TCP-style handshake
* No built-in retransmission
* No guaranteed ordering
* Lower overhead

UDP is commonly used by:

* DNS
* DHCP
* NTP
* VoIP
* Streaming applications
* Some modern protocols such as QUIC, which runs over UDP

---

# TCP vs UDP

| Feature             | TCP             | UDP                        |
| ------------------- | --------------- | -------------------------- |
| Connection-oriented | Yes             | No                         |
| Reliable delivery   | Yes             | No built-in reliability    |
| Ordered delivery    | Yes             | No guarantee               |
| Retransmission      | Yes             | No built-in retransmission |
| Flow control        | Yes             | No TCP-style flow control  |
| Handshake           | Yes             | No TCP-style handshake     |
| Overhead            | Higher          | Lower                      |
| Typical use         | Web, SSH, email | DNS, DHCP, VoIP, streaming |

---

# TCP Three-Way Handshake

Before TCP normally transfers application data, it establishes a connection using the three-way handshake.

The process is:

```text
Client                                Server

   SYN  ─────────────────────────────→

        ←──────────────────── SYN/ACK

   ACK  ─────────────────────────────→

          Connection Established
```

### Step 1 — SYN

The client sends a **SYN** segment.

It indicates that the client wants to establish a TCP connection.

### Step 2 — SYN/ACK

The server responds with **SYN/ACK**.

This indicates that:

* The server received the SYN.
* The server is willing to establish the connection.

### Step 3 — ACK

The client sends an **ACK**.

The TCP connection is now established.

---

# TCP Flags

TCP uses control flags to manage connections.

Common flags include:

| Flag | Purpose                                         |
| ---- | ----------------------------------------------- |
| SYN  | Initiates a connection                          |
| ACK  | Acknowledges received data                      |
| FIN  | Gracefully closes a connection                  |
| RST  | Resets a connection                             |
| PSH  | Requests that data be pushed to the application |
| URG  | Indicates urgent data                           |

Example:

```text
SYN
SYN/ACK
ACK
```

represents the normal three-way handshake.

---

# TCP Connection Termination

A TCP connection can normally be closed using FIN and ACK exchanges.

A simplified process is:

```text
Client                                Server

   FIN  ─────────────────────────────→

        ←──────────────────────── ACK

        ←──────────────────────── FIN

   ACK  ─────────────────────────────→
```

The exact exchange can vary depending on which side initiates closure and the state of the connection.

---

# Ports and Sockets

## Port Number

A port identifies a logical service endpoint at the Transport Layer.

Examples:

```text
22    → SSH
53    → DNS
80    → HTTP
443   → HTTPS
3389  → RDP
```

---

## Socket

A **socket** can be thought of as an endpoint used by a process for network communication.

A simplified TCP endpoint can be represented as:

```text
IP Address + Port + Protocol
```

Example:

```text
192.168.10.20:51542/TCP
```

A complete TCP connection can be identified using the combination of:

```text
Source IP
Source Port
Destination IP
Destination Port
Protocol
```

For example:

```text
192.168.10.20:51542
        │
        │ TCP
        ▼
203.0.113.50:443
```

---

# Layer 2 — Internet

## Overview

The **Internet Layer** is responsible for logical addressing and routing between networks.

The main protocol is:

**Internet Protocol (IP)**

The Internet Layer corresponds approximately to **Layer 3 of the OSI model**.

---

# IP and the Internet Layer

IP provides:

* Logical addressing
* Packet delivery
* Routing between networks
* Best-effort delivery

The two major versions are:

* IPv4
* IPv6

---

# IPv4

IPv4 uses **32-bit addresses**.

Example:

```text
192.168.10.20
```

An IPv4 address contains four octets:

```text
192 . 168 . 10 . 20
```

Each octet contains 8 bits.

Therefore:

```text
8 + 8 + 8 + 8 = 32 bits
```

---

## IPv4 Packet

A simplified IPv4 packet can be represented as:

```text
+-----------------------------+
| Source IP Address           |
+-----------------------------+
| Destination IP Address      |
+-----------------------------+
| Protocol                    |
+-----------------------------+
| TTL                         |
+-----------------------------+
| Payload                     |
+-----------------------------+
```

### Important fields

#### Source IP

Identifies the source address.

#### Destination IP

Identifies the destination address.

#### Protocol

Identifies the encapsulated upper-layer protocol.

Examples:

* TCP
* UDP
* ICMP

#### TTL

**Time To Live** limits how many Layer 3 hops a packet can traverse.

Each router normally decrements the TTL.

When TTL reaches zero, the packet is discarded.

---

# IPv6

IPv6 uses **128-bit addresses**.

Example:

```text
2001:db8::1
```

IPv6 provides a much larger address space than IPv4.

Important IPv6 features include:

* 128-bit addressing
* Simplified base header
* Neighbor Discovery
* Stateless Address Autoconfiguration
* Multicast support

---

# ICMP

**ICMP (Internet Control Message Protocol)** is used for network diagnostics and control messaging.

A common example is:

```bash
ping 8.8.8.8
```

Ping commonly uses:

* ICMP Echo Request
* ICMP Echo Reply

Conceptually:

```text
Host A ── ICMP Echo Request ──→ Host B

Host A ←── ICMP Echo Reply ─── Host B
```

ICMP does **not use TCP or UDP ports**.

This is an important point.

---

# Routing

Routing is the process of determining where packets should be forwarded.

A router examines the destination IP address and uses its routing table to determine the appropriate next hop or outgoing interface.

Example:

```text
Network A
192.168.10.0/24
      │
      ▼
   Router
      │
      ▼
Network B
192.168.20.0/24
```

A simplified routing decision:

```text
Destination IP
      ↓
Routing Table
      ↓
Next Hop / Interface
      ↓
Forward Packet
```

---

# Default Gateway

A **default gateway** is usually the router that a host uses to reach destinations outside its local network.

Example:

```text
PC
192.168.10.20
Gateway: 192.168.10.1
       │
       ▼
    Router
       │
       ▼
   Internet
```

If the destination is not on the local subnet, the host generally sends the packet to the default gateway.

---

# ARP and Neighbor Discovery

## ARP

**Address Resolution Protocol (ARP)** is used by IPv4 hosts to determine the MAC address associated with a local IPv4 address.

Example:

```text
Host A:
Who has 192.168.10.50?

Host B:
192.168.10.50 is at
AA:BB:CC:DD:EE:FF
```

ARP operates at the boundary between IP and link-layer networking and is commonly associated with local network communication.

---

## IPv6 Neighbor Discovery

IPv6 does not use ARP.

Instead, IPv6 uses **Neighbor Discovery Protocol (NDP)**, which uses ICMPv6 messages.

NDP provides functionality related to:

* Neighbor discovery
* Router discovery
* Address resolution
* Prefix discovery

---

# Layer 1 — Network Access

## Overview

The **Network Access Layer** is the lowest layer of the commonly taught TCP/IP model.

It is responsible for communication over the local network link and includes functions associated with the OSI:

* Data Link Layer
* Physical Layer

```text
TCP/IP Network Access
          ↓
+----------------------+
| OSI Data Link        |
+----------------------+
| OSI Physical         |
+----------------------+
```

This layer handles:

* Local network delivery
* Frames
* MAC addresses
* Media access
* Physical transmission
* Electrical, optical, or radio signaling

---

# Ethernet

**Ethernet** is one of the most widely used local networking technologies.

Ethernet frames contain information such as:

```text
+-----------------------------+
| Destination MAC             |
+-----------------------------+
| Source MAC                  |
+-----------------------------+
| EtherType / Length          |
+-----------------------------+
| Payload                     |
+-----------------------------+
| Frame Check Sequence        |
+-----------------------------+
```

Ethernet uses MAC addressing for local frame delivery.

---

# Wi-Fi

Wi-Fi is based on IEEE 802.11 wireless networking technologies.

A simplified model is:

```text
Laptop
   │
   │ Wireless
   ▼
Access Point
   │
   ▼
Switch
```

The wireless portion uses radio communication instead of Ethernet cable.

Wi-Fi still uses Layer 2 concepts such as MAC addressing and Layer 3 IP networking above it.

---

# MAC Address

A MAC address is associated with a network interface.

Example:

```text
00:1A:2B:3C:4D:5E
```

MAC addresses are primarily used for local link-layer communication.

For example:

```text
Source MAC
AA:AA:AA:AA:AA:AA

Destination MAC
BB:BB:BB:BB:BB:BB
```

---

# Encapsulation in TCP/IP

**Encapsulation** is the process of adding protocol information as data moves down the TCP/IP stack.

Suppose an application creates data.

```text
Application Data
        ↓
TCP Header + Application Data
        ↓
IP Header + TCP Segment
        ↓
Ethernet Header + IP Packet + Trailer
        ↓
Bits / Signals
```

The result at each layer is commonly described as:

```text
Application → Data
Transport → Segment / Datagram
Internet → Packet
Network Access → Frame / Bits
```

---

# De-encapsulation

At the receiving system, the process is reversed.

```text
Bits
  ↓
Frame
  ↓
Packet
  ↓
Segment / Datagram
  ↓
Application Data
```

The receiving host removes and processes the appropriate headers as the data moves upward through the stack.

---

# Example: Accessing a Website

Suppose a user enters:

```text
https://example.com
```

A simplified TCP/IP flow is:

```text
Application
    │
    │ HTTPS
    ▼
Transport
    │
    │ TCP
    ▼
Internet
    │
    │ IP
    ▼
Network Access
    │
    │ Ethernet / Wi-Fi
    ▼
Network
```

Let's examine each layer.

---

## Application Layer

The browser creates an HTTPS request.

```text
GET / HTTP...
```

The application uses HTTPS to communicate with the web server.

---

## Transport Layer

TCP is commonly used for HTTPS.

Example:

```text
Source Port:      51542
Destination Port: 443
Protocol:         TCP
```

TCP establishes the connection and transports the application data reliably.

---

## Internet Layer

IP adds logical addressing.

```text
Source IP:      192.168.10.20
Destination IP: <Web Server IP>
```

The packet can then be routed across networks.

---

## Network Access Layer

The IP packet is encapsulated in a local-link frame.

For Ethernet:

```text
Source MAC
Destination MAC
IP Packet
```

The frame is transmitted across the local medium.

---

# Example: DNS Resolution

Before connecting to a website, a client may need to determine the IP address associated with a domain name.

For example:

```text
google.com
    ↓
DNS Query
    ↓
DNS Server
    ↓
IP Address
```

A simplified query may use:

```text
Protocol: UDP
Destination Port: 53
```

DNS can also use TCP, and modern DNS deployments may use additional transports such as TLS or HTTPS.

---

## TCP/IP View of DNS

```text
Application
    ↓
DNS
    ↓
Transport
    ↓
UDP/TCP
    ↓
Internet
    ↓
IP
    ↓
Network Access
    ↓
Ethernet/Wi-Fi
```

---

# Example: Ping

When a user executes:

```bash
ping 8.8.8.8
```

the system commonly sends an ICMP Echo Request.

A simplified stack is:

```text
Application
    ↓
ICMP
    ↓
IP
    ↓
Ethernet / Wi-Fi
    ↓
Physical Network
```

Important:

> ICMP does not use TCP or UDP port numbers.

---

# TCP/IP Model and OSI Model

The OSI model and TCP/IP model describe similar networking concepts, but they organize them differently.

### OSI

The OSI model contains seven layers:

```text
7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

### TCP/IP

The commonly taught TCP/IP model contains four layers:

```text
4 Application
3 Transport
2 Internet
1 Network Access
```

The TCP/IP Application Layer combines the functions represented by OSI Layers 5–7.

The TCP/IP Network Access Layer combines functions represented by OSI Layers 1–2.

---

# TCP/IP vs OSI Layer Mapping

| OSI Model    | TCP/IP Model   |
| ------------ | -------------- |
| Application  | Application    |
| Presentation | Application    |
| Session      | Application    |
| Transport    | Transport      |
| Network      | Internet       |
| Data Link    | Network Access |
| Physical     | Network Access |

Visual representation:

```text
OSI                         TCP/IP

Application ────────┐
Presentation ───────┼──── Application
Session ────────────┘

Transport ───────────────── Transport

Network ────────────────── Internet

Data Link ──────────┐
Physical ───────────┴──── Network Access
```

---

# OSI vs TCP/IP

| Feature                    | OSI                        | TCP/IP                          |
| -------------------------- | -------------------------- | ------------------------------- |
| Number of layers           | 7                          | Commonly 4                      |
| Type                       | Reference model            | Practical protocol architecture |
| Main purpose               | Conceptual standardization | Real-world Internet networking  |
| Application representation | 3 layers                   | 1 layer                         |
| Physical/Data Link         | Separate                   | Usually combined                |
| Common protocols           | Not a protocol suite       | IP, TCP, UDP, etc.              |

### Important distinction

The OSI model is primarily a **reference framework**.

TCP/IP is both a model and a **protocol suite/architecture** associated with protocols actually used on IP networks.

---

# Network Devices and TCP/IP Layers

Different devices are commonly associated with different TCP/IP layers.

| Device                | Main TCP/IP Layer         |
| --------------------- | ------------------------- |
| Network cable         | Network Access            |
| Hub                   | Network Access            |
| Switch                | Network Access            |
| Wireless Access Point | Network Access            |
| Router                | Internet                  |
| Layer 3 Switch        | Internet + Network Access |
| Firewall              | Multiple layers           |
| Proxy                 | Application               |

Modern security and network devices can operate across multiple layers.

---

# Network Traffic Flow

A typical web communication can be simplified as:

```text
Client
  │
  ▼
Application
  │
  ▼
TCP
  │
  ▼
IP
  │
  ▼
Ethernet / Wi-Fi
  │
  ▼
Switch
  │
  ▼
Router
  │
  ▼
Internet
  │
  ▼
Remote Router
  │
  ▼
Server
```

The server processes the information in reverse order.

```text
Network Access
      ↓
Internet
      ↓
Transport
      ↓
Application
```

---

# Layer-by-Layer Troubleshooting

The TCP/IP model provides a useful way to isolate network problems.

## Network Access Layer

Check:

* Cable
* Network interface
* Wi-Fi signal
* Switch connection
* VLAN
* Local link

Useful commands:

```bash
ip link
```

Windows:

```powershell
ipconfig /all
```

---

## Internet Layer

Check:

* IP address
* Subnet mask/prefix
* Default gateway
* Routing table
* Destination reachability

Linux:

```bash
ip addr
ip route
```

Windows:

```powershell
ipconfig
route print
```

---

## Transport Layer

Check:

* TCP connectivity
* Destination port
* Listening services
* UDP behavior
* Firewall filtering

Examples:

```bash
ss -tuln
```

or:

```powershell
netstat -ano
```

---

## Application Layer

Check:

* DNS resolution
* Web application response
* Authentication
* Application errors
* Protocol configuration
* Service availability

Examples:

```bash
nslookup example.com
```

```bash
curl https://example.com
```

---

# Common Protocols by TCP/IP Layer

| TCP/IP Layer   | Protocols / Technologies                                     |
| -------------- | ------------------------------------------------------------ |
| Application    | HTTP, HTTPS, DNS, DHCP, SSH, FTP, SMTP, IMAP, SNMP, NTP, SMB |
| Transport      | TCP, UDP                                                     |
| Internet       | IPv4, IPv6, ICMP                                             |
| Network Access | Ethernet, Wi-Fi, ARP, physical media                         |

This table is simplified because some protocols operate across boundaries or have functions that do not map cleanly to a single model layer.

---

# Practical Example 1 — HTTPS Connection

Consider:

```text
192.168.10.20:51542
        │
        │ TCP
        ▼
203.0.113.50:443
```

The stack can be represented as:

```text
Application → HTTPS
Transport   → TCP / 443
Internet    → IP
Network     → Ethernet/Wi-Fi
```

---

# Practical Example 2 — DNS Query

```text
192.168.10.20:53000
        │
        │ UDP
        ▼
192.168.10.1:53
```

Stack:

```text
Application → DNS
Transport   → UDP / 53
Internet    → IP
Network     → Ethernet/Wi-Fi
```

---

# Practical Example 3 — SSH

```text
192.168.10.20:51550
        │
        │ TCP
        ▼
192.168.10.50:22
```

Stack:

```text
Application → SSH
Transport   → TCP / 22
Internet    → IP
Network     → Ethernet/Wi-Fi
```

---

# Practical Example 4 — Ping

```text
192.168.10.20
      │
      │ ICMP Echo Request
      ▼
8.8.8.8
```

Stack:

```text
Application → Ping utility
Internet    → ICMP + IP
Network     → Ethernet/Wi-Fi
```

There is no TCP or UDP port involved.

---

# Common Beginner Mistakes

## Mistake 1: Thinking TCP/IP means only TCP and IP

TCP/IP refers to the broader **Internet Protocol Suite**, not just two protocols.

It includes many protocols:

```text
TCP
UDP
IP
ICMP
DNS
DHCP
HTTP
HTTPS
SSH
SMTP
...
```

---

## Mistake 2: Thinking TCP is more secure than UDP

TCP provides reliability and ordering.

It does **not** automatically provide encryption.

Security depends on the higher-level protocols and controls being used.

For example:

```text
HTTP over TCP
```

does not provide the same encryption protections as:

```text
HTTPS over TCP
```

---

## Mistake 3: Thinking all DNS traffic uses UDP

DNS commonly uses UDP port 53, but DNS can also use TCP and newer encrypted transports depending on the deployment.

---

## Mistake 4: Thinking every communication uses TCP

Some protocols use UDP or other IP transport mechanisms.

Example:

```text
DNS
DHCP
VoIP
```

may use UDP.

---

## Mistake 5: Thinking IP guarantees delivery

IP provides **best-effort packet delivery**.

It does not itself guarantee:

* Delivery
* Ordering
* Retransmission

TCP can provide these reliability mechanisms above IP.

---

## Mistake 6: Confusing IP addresses and ports

Remember:

```text
IP Address → identifies the network endpoint/address
Port       → identifies a transport service endpoint
```

Example:

```text
192.168.10.20:443
```

means:

```text
IP address = 192.168.10.20
Port       = 443
```

---

## Mistake 7: Thinking routers forward based on MAC addresses across the Internet

Routers primarily make Layer 3 forwarding decisions using IP information.

The Layer 2 frame changes as traffic moves from one local link to another.

---

# Useful Commands

## Windows

### Display IP configuration

```powershell
ipconfig
```

Detailed configuration:

```powershell
ipconfig /all
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

### DNS query

```powershell
nslookup google.com
```

---

### View network connections

```powershell
netstat -ano
```

---

## Linux

### Display network interfaces

```bash
ip addr
```

---

### Display routes

```bash
ip route
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
nslookup google.com
```

or:

```bash
dig google.com
```

---

### View listening sockets

```bash
ss -tuln
```

---

### View active connections

```bash
ss -tunap
```

---

# Practical Learning Exercise

Use your own lab or computer to inspect the TCP/IP configuration.

### Windows

Run:

```powershell
ipconfig /all
```

Identify:

```text
IPv4 Address
Subnet Mask
Default Gateway
DNS Servers
MAC Address
```

Then run:

```powershell
ping 8.8.8.8
```

and:

```powershell
nslookup google.com
```

Observe how the different commands provide information about different parts of the TCP/IP architecture.

### Linux

Run:

```bash
ip addr
ip route
```

Then:

```bash
ping 8.8.8.8
```

and:

```bash
dig google.com
```

Finally:

```bash
ss -tuln
```

Observe:

* IP configuration
* Routing
* Connectivity
* DNS resolution
* Listening ports

---

# TCP/IP Model Cheat Sheet

```text
+------------------------------------------------+
| Layer 4 — APPLICATION                          |
| HTTP | HTTPS | DNS | DHCP | SSH | SMTP | FTP |
+------------------------------------------------+
| Layer 3 — TRANSPORT                            |
| TCP | UDP | Ports                              |
+------------------------------------------------+
| Layer 2 — INTERNET                             |
| IPv4 | IPv6 | ICMP | Routing                  |
+------------------------------------------------+
| Layer 1 — NETWORK ACCESS                       |
| Ethernet | Wi-Fi | MAC | ARP | Physical Media |
+------------------------------------------------+
```

---

# Key Concepts to Remember

### Application

```text
What service is being used?
```

Examples:

```text
HTTP
HTTPS
DNS
SSH
SMTP
DHCP
```

### Transport

```text
How is application data transported?
```

Examples:

```text
TCP
UDP
Ports
```

### Internet

```text
Where should the packet go?
```

Examples:

```text
IPv4
IPv6
Routing
ICMP
```

### Network Access

```text
How is the data delivered over the local network?
```

Examples:

```text
Ethernet
Wi-Fi
MAC
ARP
Physical media
```

---

# TCP/IP Model — Complete Example

Consider this communication:

```text
Client:
192.168.10.20:51542

Destination:
203.0.113.50:443

Protocol:
TCP
```

The communication can be represented as:

```text
Application
    │
    │ HTTPS
    ▼
Transport
    │
    │ TCP
    │
    │ Source Port: 51542
    │ Destination Port: 443
    ▼
Internet
    │
    │ Source IP: 192.168.10.20
    │ Destination IP: 203.0.113.50
    ▼
Network Access
    │
    │ Ethernet / Wi-Fi
    ▼
Network
```

At the receiving system:

```text
Network Access
      ↓
Internet
      ↓
Transport
      ↓
Application
```

---

# Final Mental Model

When analyzing any network communication, think from top to bottom:

```text
APPLICATION
What service?
    ↓
TRANSPORT
TCP or UDP?
Which ports?
    ↓
INTERNET
Which IP addresses?
Which route?
    ↓
NETWORK ACCESS
Which local network?
Which MAC address?
How is it physically transmitted?
```

A compact memory model is:

```text
Application → Services
Transport   → Ports
Internet    → IP
Network     → MAC / Local Link
```

---

# Key Takeaways

1. The TCP/IP model commonly contains **four layers**.
2. The layers are:

   * Application
   * Transport
   * Internet
   * Network Access
3. The TCP/IP model is closely associated with the **Internet Protocol Suite**.
4. The Application Layer provides network services used by applications.
5. The Transport Layer provides process-to-process communication using protocols such as TCP and UDP.
6. TCP provides reliable, ordered, connection-oriented transport.
7. UDP provides connectionless transport with lower protocol overhead.
8. Port numbers identify transport-layer service endpoints.
9. TCP commonly uses a three-way handshake to establish connections.
10. The Internet Layer is responsible for IP addressing and routing.
11. IPv4 uses 32-bit addresses.
12. IPv6 uses 128-bit addresses.
13. ICMP is used for network diagnostics and control messaging.
14. ARP is used by IPv4 hosts to resolve local IPv4 addresses to MAC addresses.
15. IPv6 uses Neighbor Discovery instead of ARP.
16. The Network Access Layer covers local-link and physical networking functions.
17. Ethernet and Wi-Fi operate primarily within the Network Access portion of the TCP/IP model.
18. Encapsulation occurs as data moves down the stack.
19. De-encapsulation occurs as data moves up the stack.
20. The TCP/IP model and OSI model describe similar concepts using different layer structures.
21. TCP/IP is more closely aligned with the protocols used in real-world IP networking.
22. Understanding TCP/IP is essential for learning **IP addressing, subnetting, routing, DNS, DHCP, TCP/UDP, NAT, firewalls, packet analysis, and network troubleshooting**.
