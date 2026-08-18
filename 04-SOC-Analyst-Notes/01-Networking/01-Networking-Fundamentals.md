# Networking Fundamentals

## 1. What is a Computer Network?

A computer network is a collection of connected devices that exchange data and share services or resources using defined communication protocols.

Examples of networked devices include:

- Workstations and laptops
- Servers
- Printers
- Switches
- Routers
- Firewalls
- Wireless access points
- IoT devices

```text
PC ─── Switch ─── Router ─── Internet
        │
        └──── Server
```

## 2. Network Components

### Host
A **host** is a network-connected device that can send or receive IP traffic.

### Client
A **client** requests a service, such as a web page or file.

### Server
A **server** provides a service to clients, such as DNS, HTTP, file sharing, or authentication.

### Switch
A switch connects devices within a local network and normally forwards Ethernet frames using MAC addresses.

### Router
A router connects different IP networks and forwards packets according to routing information.

### Firewall
A firewall permits or blocks traffic according to configured security policy.

## 3. How Communication Works

A simplified communication flow is:

```text
Client → Request → Server
Client ← Response ← Server
```

Network communication is governed by protocols that define addressing, formatting, delivery, error handling, and session behavior.

## 4. Network Types

- **PAN:** Personal Area Network
- **LAN:** Local Area Network
- **WLAN:** Wireless LAN
- **MAN:** Metropolitan Area Network
- **WAN:** Wide Area Network
- **Internet:** Global interconnected networks
- **Intranet:** Private organizational network
- **Extranet:** Controlled access for authorized external users

## 5. Client-Server vs Peer-to-Peer

### Client-Server
Resources are provided by centralized servers.

### Peer-to-Peer
Peers can directly provide and consume resources without requiring a dedicated central server.

## 6. Network Addressing

Two fundamental addressing concepts are:

- **MAC address:** local link-layer identity
- **IP address:** logical network address used for routed communication

## 7. Ports and Protocols

An IP address identifies the network endpoint, while a transport port identifies a service endpoint.

Example:

```text
192.168.10.20:443/TCP
```

## 8. Packets and Frames

```text
Application Data
      ↓
TCP Segment / UDP Datagram
      ↓
IP Packet
      ↓
Ethernet/Wi-Fi Frame
      ↓
Bits / Signals
```

## 9. Traffic Direction

- **Inbound:** entering a defined host or network.
- **Outbound:** leaving a defined host or network.
- **Internal:** between internal systems.
- **External:** involving systems outside the defined internal environment.

These terms are always relative to a stated point of view.

## 10. Unicast, Broadcast, and Multicast

| Type | Delivery |
|---|---|
| Unicast | One sender to one receiver |
| Broadcast | One sender to all hosts in the broadcast domain |
| Multicast | One sender to subscribed receivers |

## 11. Basic Traffic Flow

```text
Client
  ↓
Switch
  ↓
Gateway/Firewall
  ↓
Router/ISP
  ↓
Remote Network
  ↓
Server
```

## 12. Essential Commands

Windows:

```powershell
ipconfig /all
ping 8.8.8.8
tracert 8.8.8.8
nslookup example.com
netstat -ano
```

Linux:

```bash
ip addr
ip route
ping 8.8.8.8
traceroute 8.8.8.8
dig example.com
ss -tuln
```

## Key Takeaways

A strong networking foundation requires understanding **hosts, switches, routers, IP addresses, MAC addresses, ports, protocols, packets, frames, and traffic direction**. These concepts form the vocabulary used throughout the remaining networking lessons.
