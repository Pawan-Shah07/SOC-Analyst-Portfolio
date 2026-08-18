# Networking Fundamentals

This lesson covers the core networking concepts required to understand how devices communicate and how network traffic is structured.

## Table of Contents

* [What is a Computer Network?](#what-is-a-computer-network)
* [Why Networking Matters in SOC](#why-networking-matters-in-soc)
* [Network Components](#network-components)
* [How Network Communication Works](#how-network-communication-works)
* [Network Types](#network-types)
* [Client-Server vs Peer-to-Peer](#client-server-vs-peer-to-peer)
* [Network Addressing](#network-addressing)
* [MAC Address vs IP Address](#mac-address-vs-ip-address)
* [Ports and Protocols](#ports-and-protocols)
* [Packets and Frames](#packets-and-frames)
* [Inbound vs Outbound Traffic](#inbound-vs-outbound-traffic)
* [Internal vs External Traffic](#internal-vs-external-traffic)
* [Unicast, Broadcast and Multicast](#unicast-broadcast-and-multicast)
* [Basic Network Traffic Flow](#basic-network-traffic-flow)
* [SOC-Relevant Network Concepts](#soc-relevant-network-concepts)
* [Common Network Security Threats](#common-network-security-threats)
* [Useful Networking Commands](#useful-networking-commands)
* [SOC Analyst Takeaways](#soc-analyst-takeaways)

---

## What is a Computer Network?

A **computer network** is a collection of two or more devices connected so that they can communicate, exchange data, and share resources.

Network-connected devices can include:

* Computers
* Laptops
* Servers
* Smartphones
* Printers
* Routers
* Switches
* Firewalls
* Wireless access points
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

* Communication between devices
* File sharing
* Hardware sharing
* Application and service access
* Internet access
* Resource sharing
* Data exchange

---

## Why Networking Matters in SOC

Networking is a core skill for a SOC analyst because many security events involve network communication.

A SOC analyst may investigate information such as:

```text
Source IP:        192.168.10.20
Destination IP:   8.8.8.8
Protocol:         UDP
Destination Port: 53
Timestamp:        12:30:15
```

Understanding networking helps an analyst determine:

* Which system generated the traffic
* Where the traffic is going
* Which protocol is being used
* Which service or port is involved
* Whether the communication is internal or external
* Whether the activity is expected or suspicious

Networking knowledge is especially important when working with:

* Firewall logs
* DNS logs
* IDS/IPS alerts
* Network traffic captures
* SIEM events
* Proxy logs
* Authentication events
* Endpoint telemetry

---

## Network Components

A network is made up of different components that perform different functions.

### Host

A **host** is a device connected to a network that can communicate over that network.

Examples:

* Desktop computer
* Laptop
* Server
* Smartphone
* Virtual machine
* Network printer

---

### Client

A **client** is a system or application that requests a service from another system.

Example:

```text
Web Browser ───────→ Web Server
   Client             Server
```

Examples:

* Web browser
* Email application
* SSH client
* FTP client
* Mobile application

---

### Server

A **server** is a system that provides services or resources to clients.

Examples:

| Server                | Purpose                                |
| --------------------- | -------------------------------------- |
| Web Server            | Provides websites and web applications |
| DNS Server            | Resolves domain names to IP addresses  |
| DHCP Server           | Provides network configuration         |
| File Server           | Provides files                         |
| Mail Server           | Handles email                          |
| Database Server       | Provides database services             |
| Authentication Server | Handles authentication                 |

---

### Switch

A **switch** connects devices within a local network and forwards Ethernet frames to the appropriate destination.

```text
PC 1 ───┐
PC 2 ───┤
PC 3 ───┼── Switch
Server ──┤
Printer ─┘
```

A switch primarily uses **MAC addresses** when forwarding Ethernet frames.

---

### Router

A **router** connects different networks and forwards packets between them.

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

A router commonly performs functions such as:

* Packet forwarding
* Routing
* Network-to-network communication
* NAT
* Interconnection between internal and external networks

---

### Firewall

A **firewall** controls network traffic according to configured security rules.

```text
Internet
   │
   ▼
Firewall
   │
   ▼
Internal Network
```

Firewall decisions can be based on:

* Source IP
* Destination IP
* Source port
* Destination port
* Protocol
* Direction
* Interface
* Connection state
* Application, depending on firewall capabilities

---

## How Network Communication Works

When one device communicates with another, information is transmitted according to networking protocols.

A basic communication model is:

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

For example, when a browser accesses a web server:

```text
Browser
(Client)
   │
   │ HTTPS Request
   ▼
Web Server
   │
   │ HTTPS Response
   ▼
Browser
```

Network communication involves several important pieces of information:

```text
Source
   ↓
Destination
   ↓
Protocol
   ↓
Port
   ↓
Data
```

---

## Network Types

Networks can be classified by geographical coverage, communication method, or purpose.

### PAN — Personal Area Network

A **PAN** covers a very small area around an individual.

Examples:

* Smartphone and smartwatch
* Bluetooth headphones
* Wireless keyboard
* Smartphone and laptop using Bluetooth

```text
             Smartphone
                 │
          Bluetooth / USB
                 │
        ┌────────┴────────┐
        │                 │
     Laptop            Smartwatch
```

---

### LAN — Local Area Network

A **LAN** connects devices within a relatively small area.

Examples:

* Home
* Office
* School laboratory
* Building

```text
PC 1 ───┐
PC 2 ───┤
PC 3 ───┼── Switch ─── Router
Printer ─┘
```

---

### WLAN — Wireless Local Area Network

A **WLAN** is a LAN in which devices connect wirelessly, typically using Wi-Fi.

```text
Laptop ─── Wi-Fi ─── Access Point ─── Switch
```

WLAN is a type of LAN based on the wireless connection method.

---

### MAN — Metropolitan Area Network

A **MAN** covers a larger area than a LAN but generally smaller than a WAN.

It may connect multiple buildings or LANs across a city or metropolitan area.

```text
Building A ─────┐
                │
Building B ─────┼──── Metropolitan Network
                │
Building C ─────┘
```

---

### WAN — Wide Area Network

A **WAN** connects networks across large geographical distances.

Examples:

* Multiple cities
* Multiple countries
* Global corporate networks

```text
Office A
Kathmandu
    │
    └──── WAN ──── Office B
                   Delhi
                         │
                         └──── Office C
                                London
```

---

### Internet

The **Internet** is a global system of interconnected networks.

It is not one single physical network. It consists of many networks operated by organizations such as:

* Internet service providers
* Businesses
* Universities
* Governments
* Cloud providers

---

### Intranet

An **intranet** is a private network used within an organization.

Examples:

* Internal websites
* Employee portals
* Internal applications
* Internal file services

---

### Extranet

An **extranet** provides controlled access to selected organizational resources for authorized external users.

Examples:

* Supplier portals
* Partner portals
* Vendor access systems

### Quick comparison

| Type     | Description                                               |
| -------- | --------------------------------------------------------- |
| PAN      | Personal-area network                                     |
| LAN      | Local-area network                                        |
| WLAN     | Wireless local-area network                               |
| MAN      | Metropolitan-area network                                 |
| WAN      | Wide-area network                                         |
| Internet | Global interconnected networks                            |
| Intranet | Private internal organizational network                   |
| Extranet | Private network/resources with controlled external access |

---

## Client-Server vs Peer-to-Peer

### Client-Server Model

In the **client-server model**, clients request services from centralized servers.

```text
Client 1 ───┐
Client 2 ───┼──→ Server
Client 3 ───┘
```

Examples:

* Browser → Web server
* Computer → File server
* Client → Database server
* Computer → Authentication server

### Advantages

* Centralized management
* Centralized security controls
* Easier administration
* Centralized data storage
* Easier backup and monitoring

---

### Peer-to-Peer Model

In a **peer-to-peer (P2P)** network, devices can communicate directly and can act as both clients and servers.

```text
Peer A ───── Peer B
  │ \         / │
  │   \     /   │
  └──── Peer C ─┘
```

Each peer can provide resources to another peer.

### Advantages

* Simple for small environments
* No dedicated central server required
* Direct resource sharing

### Comparison

| Feature        | Client-Server         | Peer-to-Peer                     |
| -------------- | --------------------- | -------------------------------- |
| Central server | Usually present       | Not required                     |
| Management     | Centralized           | Distributed                      |
| Scalability    | Generally better      | More limited                     |
| Administration | Easier centrally      | More difficult as size increases |
| Example        | Corporate application | Small file-sharing network       |

---

## Network Addressing

Network addressing allows devices and interfaces to be identified and located for communication.

Two important addressing concepts are:

* **MAC address**
* **IP address**

A system may have both.

```text
Device
  │
  ├── MAC Address
  │
  └── IP Address
```

---

### IPv4 Address

An IPv4 address is a 32-bit logical address usually written in dotted-decimal notation.

Example:

```text
192.168.10.20
```

It consists of four octets:

```text
192 . 168 . 10 . 20
```

Each octet ranges from `0` to `255`.

IPv4 addressing will be studied in greater detail in a later lesson.

---

### IPv6 Address

IPv6 uses 128-bit addresses.

Example:

```text
2001:db8::1
```

IPv6 was developed to provide a much larger address space than IPv4.

---

## MAC Address vs IP Address

### MAC Address

A **MAC address** is a link-layer address associated with a network interface.

Example:

```text
00:1A:2B:3C:4D:5E
```

MAC addresses are commonly used for local Ethernet communication.

---

### IP Address

An **IP address** is a logical network-layer address.

Example:

```text
192.168.10.20
```

IP addresses can change depending on the network configuration.

### Comparison

| Feature                 | MAC Address                    | IP Address                 |
| ----------------------- | ------------------------------ | -------------------------- |
| Layer                   | Data Link                      | Network                    |
| Purpose                 | Local interface identification | Logical network addressing |
| Example                 | `00:1A:2B:3C:4D:5E`            | `192.168.10.20`            |
| Usually associated with | Network interface              | Network configuration      |
| Commonly used by        | Switches                       | Routers and hosts          |

### Simple concept

```text
MAC → Local network/interface addressing
IP  → Logical network addressing
```

---

## Ports and Protocols

### Port

A **port** is a numerical identifier used to identify a network service endpoint.

Example:

```text
192.168.10.20:443
```

Where:

* `192.168.10.20` = IP address
* `443` = port

### Common ports

| Port | Common service |
| ---: | -------------- |
|   22 | SSH            |
|   23 | Telnet         |
|   25 | SMTP           |
|   53 | DNS            |
|   80 | HTTP           |
|  443 | HTTPS          |
| 3389 | RDP            |

---

### Protocol

A **protocol** is a set of rules for network communication.

Common protocols include:

| Protocol | Purpose                                   |
| -------- | ----------------------------------------- |
| IP       | Logical addressing and packet delivery    |
| TCP      | Reliable, connection-oriented transport   |
| UDP      | Connectionless transport                  |
| ARP      | IPv4-to-MAC resolution on a local network |
| DNS      | Domain-name resolution                    |
| DHCP     | Automatic network configuration           |
| HTTP     | Web communication                         |
| HTTPS    | Web communication protected by TLS        |
| ICMP     | Network diagnostic and control messages   |

---

## Packets and Frames

Network data is processed at different layers of the networking stack.

A simplified representation is:

```text
Application Data
      ↓
Segment        ← TCP
      ↓
Datagram       ← UDP
      ↓
Packet         ← IP
      ↓
Frame          ← Ethernet
```

### Packet

A **packet** is a unit of data at the network layer, commonly associated with IP.

A simplified IP packet may contain:

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

### Frame

A **frame** is a data unit at the data-link layer.

An Ethernet frame contains information such as:

* Source MAC address
* Destination MAC address
* EtherType
* Payload
* Frame Check Sequence

### Packet vs Frame

| Feature    | Packet        | Frame           |
| ---------- | ------------- | --------------- |
| Layer      | Network layer | Data-link layer |
| Addressing | IP            | MAC             |
| Example    | IPv4 packet   | Ethernet frame  |

---

## Inbound vs Outbound Traffic

Traffic direction is commonly described from the perspective of a particular network, host, or security boundary.

### Inbound Traffic

**Inbound traffic** is traffic entering a system or network.

```text
Internet
   │
   ▼
Firewall
   │
   ▼
Internal Host
```

For the internal network, the traffic is inbound.

### Outbound Traffic

**Outbound traffic** is traffic leaving a system or network.

```text
Internal Host
     │
     ▼
 Firewall
     │
     ▼
  Internet
```

For the internal network, the traffic is outbound.

### Important point

Inbound and outbound are **directional terms**.

The same communication can be inbound from one perspective and outbound from another.

---

## Internal vs External Traffic

### Internal Traffic

Traffic between systems inside the same organization or internal network.

Example:

```text
192.168.10.20 ─────→ 192.168.10.50
```

### External Traffic

Traffic between an internal system and a system outside the internal network.

Example:

```text
192.168.10.20 ─────→ 8.8.8.8
```

The exact definition of "internal" and "external" depends on the network architecture.

---

## Unicast, Broadcast and Multicast

These terms describe how traffic is delivered.

### Unicast

**Unicast** is communication from one sender to one receiver.

```text
Host A ─────→ Host B
```

Example:

```text
192.168.10.20 ─────→ 192.168.10.50
```

---

### Broadcast

**Broadcast** is communication from one sender to all devices within a defined broadcast domain.

```text
         ┌── Host B
         │
Host A ──┼── Host C
         │
         └── Host D
```

IPv4 broadcast traffic can use addresses such as:

```text
255.255.255.255
```

or a subnet-directed broadcast address depending on the network.

---

### Multicast

**Multicast** is communication from one sender to multiple subscribed receivers.

```text
             ┌── Host B
             │
Host A ──────┼── Host C
             │
             └── Host D
```

Only hosts that have joined the multicast group receive the traffic.

### Comparison

| Type      | Delivery                               |
| --------- | -------------------------------------- |
| Unicast   | One-to-one                             |
| Broadcast | One-to-all within the broadcast domain |
| Multicast | One-to-selected-many                   |

---

## Basic Network Traffic Flow

A typical communication flow may look like:

```text
Client
   │
   │ 1. Request
   ▼
Switch
   │
   ▼
Router / Firewall
   │
   ▼
Internet / Remote Network
   │
   ▼
Server
   │
   │ 2. Response
   ▼
Client
```

For a web request, the process can be simplified as:

```text
User
 ↓
Browser
 ↓
DNS Resolution
 ↓
Destination IP
 ↓
TCP Connection
 ↓
HTTPS Request
 ↓
Web Server
 ↓
HTTPS Response
 ↓
Browser
```

This is a conceptual flow. Real communication can involve additional systems, protocols, and network devices.

---

## SOC-Relevant Network Concepts

Network information commonly appears in security logs and alerts.

Important fields include:

### Source IP

The address associated with the system sending traffic.

### Destination IP

The address associated with the intended receiving system.

### Source Port

The source-side port associated with the connection.

### Destination Port

The destination service endpoint.

### Protocol

Examples:

* TCP
* UDP
* ICMP

### Timestamp

The time when the event occurred.

### Direction

Whether traffic is inbound or outbound relative to the monitored environment.

### Example event

```text
Source IP:        192.168.10.20
Source Port:      51542
Destination IP:   203.0.113.50
Destination Port: 443
Protocol:         TCP
Direction:        Outbound
Timestamp:        2026-08-18 12:30:15
```

A network analyst or SOC analyst can use these fields to understand the communication.

---

## Common Network Security Threats

Understanding common network threats requires familiarity with normal network behavior.

### Port Scanning

An attacker probes multiple ports to identify available services.

Example:

```text
Attacker
   │
   ├──→ Port 22
   ├──→ Port 80
   ├──→ Port 443
   ├──→ Port 3389
   └──→ Port 8080
```

---

### Brute-Force Attacks

An attacker repeatedly attempts authentication with different credentials.

Examples:

* SSH brute force
* RDP brute force
* Web login brute force

---

### Denial-of-Service

An attacker sends excessive traffic or requests to make a service unavailable.

---

### Man-in-the-Middle

An attacker positions themselves between communicating systems and attempts to intercept or manipulate communication.

---

### DNS Attacks

Possible attacks include:

* DNS spoofing
* DNS cache poisoning
* DNS tunneling
* Malicious DNS requests

---

### ARP Spoofing

An attacker sends fraudulent ARP information to associate their MAC address with another device's IP address.

---

### Network Scanning

Attackers may discover:

* Hosts
* Services
* Ports
* Operating systems
* Network topology

---

### Command and Control Traffic

Compromised systems may communicate with attacker-controlled infrastructure.

This communication can occur through:

* HTTP/HTTPS
* DNS
* Other network protocols

---

## Useful Networking Commands

These commands help inspect and troubleshoot network configuration and connectivity.

### Windows

#### `ipconfig`

Displays IP configuration.

```powershell
ipconfig
```

More detailed information:

```powershell
ipconfig /all
```

---

#### `ping`

Tests basic IP connectivity.

```powershell
ping 8.8.8.8
```

---

#### `tracert`

Shows the path traffic takes toward a destination.

```powershell
tracert 8.8.8.8
```

---

#### `nslookup`

Performs DNS queries.

```powershell
nslookup google.com
```

---

#### `netstat`

Displays network connections and listening ports.

```powershell
netstat -ano
```

---

### Linux

#### `ip addr`

Displays network interfaces and addresses.

```bash
ip addr
```

---

#### `ip route`

Displays the routing table.

```bash
ip route
```

---

#### `ping`

Tests connectivity.

```bash
ping 8.8.8.8
```

---

#### `traceroute`

Shows the path toward a destination.

```bash
traceroute 8.8.8.8
```

---

#### `nslookup`

Performs DNS queries.

```bash
nslookup google.com
```

---

#### `dig`

Provides detailed DNS information.

```bash
dig google.com
```

---

#### `ss`

Displays sockets and network connections.

```bash
ss -tuln
```

---

## SOC Analyst Takeaways

The most important networking concepts to remember are:

### 1. Devices communicate using protocols

```text
Host → Protocol → Host
```

### 2. IP addresses provide logical network addressing

```text
192.168.10.20
```

### 3. MAC addresses operate at the local data-link level

```text
00:1A:2B:3C:4D:5E
```

### 4. Ports identify service endpoints

```text
192.168.10.20:443
```

### 5. Protocols define communication behavior

Examples:

```text
TCP
UDP
DNS
HTTP
HTTPS
ICMP
ARP
DHCP
```

### 6. Packets and frames are different

```text
Frame → Data Link Layer
Packet → Network Layer
```

### 7. Traffic has a direction

```text
Inbound
Outbound
```

### 8. Traffic can be classified by scope

```text
Internal
External
```

### 9. Communication can be one-to-one or one-to-many

```text
Unicast
Broadcast
Multicast
```

### 10. Common network information

When reading a network event, identify:

```text
Who?
   ↓
Source IP / Source Port

Where?
   ↓
Destination IP / Destination Port

What?
   ↓
Protocol / Service

When?
   ↓
Timestamp

Which direction?
   ↓
Inbound / Outbound
```

---

## Quick Reference

```text
Network
 ├── Hosts
 ├── Switches
 ├── Routers
 ├── Firewalls
 └── Servers

Addressing
 ├── MAC Address
 └── IP Address

Transport
 ├── TCP
 └── UDP

Common Protocols
 ├── ARP
 ├── DNS
 ├── DHCP
 ├── HTTP
 ├── HTTPS
 └── ICMP

Traffic
 ├── Inbound / Outbound
 ├── Internal / External
 └── Unicast / Broadcast / Multicast

Data Units
 ├── Segment
 ├── Datagram
 ├── Packet
 └── Frame
```

---

## Conclusion

Networking fundamentals provide the foundation for understanding how systems communicate.

A strong understanding of:

* Network components
* Network types
* Client-server communication
* Network addressing
* MAC and IP addresses
* Ports and protocols
* Packets and frames
* Traffic direction
* Traffic scope
* Network traffic flow

is essential before moving into more advanced networking topics such as **OSI and TCP/IP models, IPv4 addressing, subnetting, routing, DNS, DHCP, TCP/UDP, NAT, and firewall operation**.
