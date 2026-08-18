# Network Troubleshooting

## 1. Overview

Network troubleshooting is the systematic process of identifying, isolating, and resolving communication problems.

A disciplined troubleshooting process is more reliable than changing multiple settings at random.

## 2. Troubleshooting Method

Use a structured approach:

```text
Identify
  ↓
Collect evidence
  ↓
Form hypothesis
  ↓
Test one variable
  ↓
Analyze result
  ↓
Fix
  ↓
Verify
  ↓
Document
```

## 3. Layered Troubleshooting

### Physical
Check:

- Cable
- Link light
- Interface state
- Wi-Fi signal
- Hardware

### Data Link
Check:

- VLAN
- Switch port
- MAC learning
- Duplex/speed issues
- Local frame errors

### Network
Check:

- IP address
- Prefix/subnet mask
- Default gateway
- Route table
- Destination reachability

### Transport
Check:

- Listening service
- Destination port
- TCP connectivity
- UDP behavior
- Firewall filtering

### Application
Check:

- DNS resolution
- Application response
- Authentication
- Protocol configuration
- Application logs

## 4. Essential Commands — Windows

### IP Configuration

```powershell
ipconfig /all
```

### Connectivity

```powershell
ping 8.8.8.8
```

### DNS

```powershell
nslookup example.com
```

### Route

```powershell
route print
tracert 8.8.8.8
```

### Connections

```powershell
netstat -ano
```

### ARP

```powershell
arp -a
```

## 5. Essential Commands — Linux

```bash
ip addr
ip route
ip neigh
ping 8.8.8.8
traceroute 8.8.8.8
dig example.com
ss -tuln
```

## 6. Troubleshooting Sequence

Suppose a host cannot reach a web application.

### Step 1 — Verify local configuration

Check IP, prefix, gateway, and DNS.

### Step 2 — Test local gateway

```text
ping <gateway>
```

### Step 3 — Test remote IP

```text
ping <remote-IP>
```

A failed ping does not always prove the service is unavailable because ICMP may be filtered.

### Step 4 — Test DNS

```text
nslookup example.com
```

### Step 5 — Test the service port

Use an appropriate TCP connectivity test or application client.

### Step 6 — Inspect logs

Check:

- Firewall logs
- DNS logs
- Endpoint logs
- Application logs
- Router/switch events

## 7. Common Symptoms

### No IP Address
Potential causes:

- DHCP failure
- Cable/interface issue
- VLAN problem
- Static configuration error

### Can Reach Gateway but Not Internet
Potential causes:

- Default route
- NAT
- Firewall policy
- Upstream routing
- DNS, if only names fail

### Can Ping IP but Not Domain
Likely DNS-related, but verify application and firewall context.

### Can Resolve Name but Web Service Fails
Possible causes:

- Port blocked
- Server unavailable
- TLS problem
- Application error
- Proxy/firewall issue

### Service IP Reachable but Port Closed
Possible causes:

- Service not listening
- Host firewall
- Network firewall
- Wrong port
- ACL policy

## 8. Packet Capture

When logs are insufficient, packet capture tools such as Wireshark or `tcpdump` can show actual traffic.

Examples:

```bash
tcpdump -ni eth0
```

A packet capture can reveal:

- ARP
- DNS
- TCP handshake
- Retransmissions
- ICMP
- HTTP metadata
- TLS handshakes

## 9. Avoid Random Changes

Do not immediately:

- Disable the firewall
- Flush everything
- Change multiple settings at once
- Replace configuration without evidence

Instead, isolate the failing layer and test the smallest possible change.

## 10. Document Findings

A good troubleshooting record contains:

```text
Problem
Impact
Evidence
Hypothesis
Tests performed
Root cause
Fix
Verification
Preventive action
```

## Key Takeaways

Good network troubleshooting is a repeatable evidence-driven process. Start at the lowest necessary layer, validate each assumption, change one variable at a time, and document the final root cause.
