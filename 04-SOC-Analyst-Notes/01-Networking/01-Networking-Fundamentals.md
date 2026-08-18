# Networking Fundamentals

> Practical networking fundamentals for a Junior SOC Analyst.

## Overview

This note covers the fundamental networking concepts required for
security monitoring, alert triage, network investigation, and incident response.

## Contents

- [What is a Computer Network?](#what-is-a-computer-network)
- [Why Networking Matters in SOC](#why-networking-matters-in-soc)
- [Network Components](#network-components)
- [How Network Communication Works](#how-network-communication-works)
- [Network Types](#network-types)
- [Client-Server vs Peer-to-Peer](#client-server-vs-peer-to-peer)
- [Network Addressing](#network-addressing)
- [MAC Address vs IP Address](#mac-address-vs-ip-address)
- [Ports and Protocols](#ports-and-protocols)
- [Packets and Frames](#packets-and-frames)
- [Inbound vs Outbound Traffic](#inbound-vs-outbound-traffic)
- [Internal vs External Traffic](#internal-vs-external-traffic)
- [Unicast, Broadcast and Multicast](#unicast-broadcast-and-multicast)
- [Basic Network Traffic Flow](#basic-network-traffic-flow)
- [SOC-Relevant Network Concepts](#soc-relevant-network-concepts)
- [Common Network Security Threats](#common-network-security-threats)
- [Useful Networking Commands](#useful-networking-commands)
- [SOC Analyst Takeaways](#soc-analyst-takeaways)

---

## What is a Computer Network?

# Lesson 1 — Computer Network Fundamentals

## 1. What is a Computer Network?

A **computer network** is a collection of two or more computing devices that are connected so they can communicate, exchange data, and share resources.

Examples of network-connected devices include:

* Computers
* Laptops
* Servers
* Smartphones
* Printers
* Routers
* Switches
* Firewalls
* Access points
* IoT devices

### Example

```text
Computer A ───┐
              │
Computer B ───┼─── Switch ─── Router ─── Internet
              │
Server ───────┘
```

### Main purposes of a network

A computer network allows devices to:

1. Communicate with one another
2. Share files
3. Share hardware, such as printers
4. Access applications and services
5. Access the Internet
6. Share resources
7. Exchange information

---

## 2. How Network Communication Works

When one device wants to communicate with another device, information is transmitted through the network.

For example, a computer may communicate with a web server:

```text
Client Computer
192.168.10.10
      │
      │ Request
      ▼
   Network
      │
      ▼
Web Server
192.168.10.50
      │
      │ Response
      ▼
Client Computer
```

The client sends a request, and the server sends a response.

This communication is controlled by a set of rules called **network protocols**.

---

## 3. Network Devices

Different devices perform different functions within a network.

### 3.1 Host

A **host** is any device connected to a network that can communicate over that network.

Examples:

* Desktop computer
* Laptop
* Server
* Smartphone
* Network printer
* Virtual machine

Example:

```text
Windows PC
    │
    └── Network
```

The Windows PC is a host.

A host normally has a network identity, such as an IP address, that allows it to communicate with other devices.

---

## 4. Client

A **client** is a device or application that requests a service from another system.

Example:

```text
Web Browser ───────→ Web Server
   Client             Server
```

The web browser acts as the client because it requests information from the web server.

Examples of clients include:

* Web browsers
* Email applications
* FTP clients
* SSH clients
* Mobile applications

A client does not necessarily have to be a physical computer. An application running on a computer can also function as a client.

---

## 5. Server

A **server** is a system that provides services or resources to other systems called clients.

Example:

```text
Client 1 ───┐
Client 2 ───┼──→ Web Server
Client 3 ───┘
```

The web server receives requests from clients and provides the requested content.

### Examples of servers

| Server                | Main purpose                           |
| --------------------- | -------------------------------------- |
| Web Server            | Provides websites and web applications |
| DNS Server            | Resolves domain names to IP addresses  |
| DHCP Server           | Assigns network configuration          |
| File Server           | Provides files                         |
| Mail Server           | Handles email services                 |
| Database Server       | Provides database services             |
| Authentication Server | Handles authentication                 |

A server can provide services to one client or many clients simultaneously.

---

## 6. Client-Server Communication

A basic client-server communication process looks like this:

```text
Client
  │
  │ Request
  ▼
Server
  │
  │ Response
  ▼
Client
```

### Example

When a user visits a website, the browser acts as the client and requests content from the web server.

```text
Browser
(Client)
   │
   │ HTTP/HTTPS Request
   ▼
Web Server
   │
   │ HTTP/HTTPS Response
   ▼
Browser
```

This request-response model is fundamental to many network applications.

---

## 7. Router

A **router** is a networking device that connects different networks and forwards packets between them.

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

The router allows devices on Network A to communicate with devices on Network B.

### Router functions

A router can:

* Connect different networks
* Forward packets
* Select paths for traffic
* Separate broadcast domains
* Provide routing between networks
* Often perform NAT
* Often provide basic network services

Example:

```text
Home Network
192.168.1.0/24
       │
       ▼
     Router
       │
       ▼
    Internet
```

The router acts as the connection point between the internal network and the external network.

---

## 8. Switch

A **network switch** is a device used to connect multiple devices within a local network.

Example:

```text
PC 1 ───┐
PC 2 ───┤
PC 3 ───┼── Switch
Server ──┤
Printer ─┘
```

A switch forwards Ethernet frames to the appropriate device.

Switches primarily operate at **Layer 2 of the OSI model**, although modern switches can also provide Layer 3 functionality.

### Important characteristic

A switch uses **MAC addresses** to determine where Ethernet frames should be forwarded.

MAC addresses will be studied in a later lesson.

---

## 9. Router vs Switch

Router and switch are different networking devices.

| Feature           | Switch                           | Router                                     |
| ----------------- | -------------------------------- | ------------------------------------------ |
| Main purpose      | Connect devices within a network | Connect different networks                 |
| Main addressing   | MAC address                      | IP address                                 |
| Typical OSI layer | Layer 2                          | Layer 3                                    |
| Example           | Connect PCs to a LAN             | Connect LAN to another network or Internet |

Example:

```text
PC1 ──┐
PC2 ──┼── Switch ─── Router ─── Internet
PC3 ──┘
```

The switch connects local devices.

The router connects the local network to another network.

---

## 10. Firewall

A **firewall** is a security device or software that controls network traffic based on defined rules.

Example:

```text
Internet
   │
   ▼
Firewall
   │
   ▼
Internal Network
```

A firewall may allow or block traffic based on:

* Source IP address
* Destination IP address
* Source port
* Destination port
* Protocol
* Direction of traffic
* Interface
* Connection state
* Application or service, depending on the firewall

### Example firewall rule

```text
Source:        192.168.10.0/24
Destination:   Any
Protocol:      TCP
Port:          443
Action:        Allow
```

Another example:

```text
Source:        Any
Destination:   Internal Network
Port:          23
Action:        Block
```

The exact firewall rules depend on the network's security requirements.

---

## 11. Network Protocol

A **network protocol** is a defined set of rules that determines how devices communicate.

Different protocols perform different tasks.

| Protocol | Purpose                                                      |
| -------- | ------------------------------------------------------------ |
| IP       | Provides logical addressing and packet delivery              |
| TCP      | Provides reliable, connection-oriented transport             |
| UDP      | Provides connectionless transport                            |
| ARP      | Resolves an IPv4 address to a MAC address on a local network |
| DNS      | Resolves domain names to IP addresses                        |
| DHCP     | Automatically provides network configuration                 |
| HTTP     | Transfers web content                                        |
| HTTPS    | Transfers web content using TLS protection                   |
| ICMP     | Used for network diagnostics and control messages            |

Protocols allow different devices and operating systems to communicate using standardized rules.

---

## 12. Why Protocols Are Necessary

Protocols provide a common set of rules for network communication.

Without agreed rules, devices would not know how to correctly interpret transmitted information.

Protocols define things such as:

* How communication begins
* How data is formatted
* How information is addressed
* How errors are handled
* How communication ends
* How devices interpret information

Therefore, protocols provide a common language for network communication.

---

## 13. Data Transmission

When data is sent across a network, it is processed into smaller units as it moves through the networking stack.

At different layers, these units have different names.

```text
Application Data
      ↓
    Segment        ← TCP
      ↓
    Datagram       ← UDP
      ↓
     Packet        ← IP
      ↓
     Frame         ← Ethernet
```

For beginner-level understanding:

> **A packet is a unit of data at the network layer.**

The exact terminology depends on the protocol and layer being discussed.

---

## 14. Packet

A **packet** is a unit of data transmitted using a network-layer protocol such as IP.

An IP packet contains information required to help deliver the packet to its destination.

Conceptually:

```text
+-----------------------------+
| Source IP Address           |
+-----------------------------+
| Destination IP Address      |
+-----------------------------+
| Protocol Information        |
+-----------------------------+
| Data / Payload              |
+-----------------------------+
```

Example:

```text
Source IP:       192.168.10.20
Destination IP:  8.8.8.8
Protocol:        UDP
Payload:         DNS-related data
```

The actual IP packet structure contains additional fields, but this simplified representation is sufficient for an introduction.

---

## 15. Source and Destination

Whenever two devices communicate, there is generally a **source** and a **destination**.

Example:

```text
192.168.10.20 ─────────→ 8.8.8.8
     Source              Destination
```

The source is the system sending the traffic.

The destination is the intended receiver.

The direction can also be reversed:

```text
8.8.8.8 ─────────→ 192.168.10.20
 Source              Destination
```

Source and destination identify the direction of communication.

---

## 16. Source IP Address

A **source IP address** identifies the IP address associated with the sender of a packet.

Example:

```text
Source IP: 192.168.10.20
```

This indicates that the packet has a source address of `192.168.10.20`.

---

## 17. Destination IP Address

A **destination IP address** identifies where the packet is being sent.

Example:

```text
Destination IP: 192.168.10.50
```

The packet is intended for the system associated with that destination address.

Together:

```text
Source IP              Destination IP
192.168.10.20  ─────→  192.168.10.50
```

---

## 18. Internal and External Networks

A network can communicate with systems inside the same network or with systems outside the local network.

### Internal communication

```text
192.168.10.20 ─────→ 192.168.10.50
```

Both addresses are part of the internal network shown in this example.

### External communication

```text
192.168.10.20 ─────→ 8.8.8.8
```

The internal host is communicating with a public IP address.

The distinction between private and public IP addressing will be covered in greater detail in later lessons.

---

## 19. Ports

An IP address identifies a network interface or host address, but a system can run many network services at the same time.

A **port number** identifies a particular service endpoint used for network communication.

Example:

```text
192.168.10.20:443
```

Here:

* `192.168.10.20` = IP address
* `443` = port number

### Common port numbers

| Port | Common service |
| ---: | -------------- |
|   22 | SSH            |
|   53 | DNS            |
|   80 | HTTP           |
|  443 | HTTPS          |
| 3389 | RDP            |

Port numbers will be studied in much greater detail later.

---

## 20. Protocol + IP + Port

A useful way to describe network communication is to consider:

```text
Protocol + Source + Destination + Port
```

Example:

```text
Protocol:        TCP
Source:          192.168.10.20
Destination:     192.168.10.50
Destination Port: 443
```

This provides more information about the communication than an IP address alone.

---

## 21. Example of Complete Communication

Suppose a Windows computer accesses a web server.

The communication might conceptually look like this:

```text
Client
192.168.10.20
      │
      │ TCP
      │ Destination Port: 443
      ▼
Web Server
203.0.113.10
```

The client sends traffic toward the server.

The server then sends traffic back:

```text
203.0.113.10:443
        │
        ▼
192.168.10.20
```

Network communication is generally bidirectional, although one system may initially initiate the connection.

---

## 22. Network Communication Example

Consider the following simplified network event:

```text
Source IP:         192.168.10.20
Destination IP:    192.168.10.50
Protocol:          TCP
Destination Port:  443
```

The basic information can be interpreted as:

* `192.168.10.20` is the source address.
* `192.168.10.50` is the destination address.
* TCP is the transport protocol.
* Port `443` is the destination service endpoint.
* The source is communicating toward the destination.

At this stage, we should not assume anything beyond the information provided by the event.

---

# Key Terms

| Term               | Definition                                                                  |
| ------------------ | --------------------------------------------------------------------------- |
| **Network**        | A collection of connected devices that can communicate                      |
| **Host**           | A device connected to a network                                             |
| **Client**         | A system or application that requests a service                             |
| **Server**         | A system that provides a service                                            |
| **Switch**         | A device that connects devices within a network                             |
| **Router**         | A device that connects different networks                                   |
| **Firewall**       | A security control that allows or blocks network traffic according to rules |
| **Protocol**       | A set of rules used for network communication                               |
| **Packet**         | A unit of data at the network layer                                         |
| **Source IP**      | IP address associated with the sender                                       |
| **Destination IP** | IP address of the intended receiver                                         |
| **Port**           | A numerical identifier for a network service endpoint                       |

---













## Why Networking Matters in SOC

Content will be added here.

## Network Components

Content will be added here.

## How Network Communication Works

Content will be added here.

## Network Types

Content will be added here.

## Client-Server vs Peer-to-Peer

Content will be added here.

## Network Addressing

Content will be added here.

## MAC Address vs IP Address

Content will be added here.

## Ports and Protocols

Content will be added here.

## Packets and Frames

Content will be added here.

## Inbound vs Outbound Traffic

Content will be added here.

## Internal vs External Traffic

Content will be added here.

## Unicast, Broadcast and Multicast

Content will be added here.

## Basic Network Traffic Flow

Content will be added here.

## SOC-Relevant Network Concepts

Content will be added here.

## Common Network Security Threats

Content will be added here.

## Useful Networking Commands

Content will be added here.

## SOC Analyst Takeaways

Content will be added here.
