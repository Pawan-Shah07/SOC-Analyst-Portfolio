# DNS

## 1. Overview

**Domain Name System (DNS)** is a distributed naming system that translates domain names into resource records, including IP addresses.

Instead of memorizing:

```text
142.250.x.x
```

users can use:

```text
google.com
```

## 2. Why DNS Exists

DNS provides human-readable naming and service discovery.

Common DNS records include:

- **A:** IPv4 address
- **AAAA:** IPv6 address
- **CNAME:** canonical name alias
- **MX:** mail exchanger
- **NS:** authoritative name server
- **TXT:** arbitrary text used for various purposes
- **PTR:** reverse lookup
- **SOA:** start of authority
- **SRV:** service location

## 3. DNS Hierarchy

DNS is hierarchical:

```text
Root
  ↓
Top-Level Domain (.com)
  ↓
Authoritative Domain (example.com)
  ↓
Host (www.example.com)
```

## 4. Recursive vs Iterative Resolution

### Recursive Resolver
A resolver performs work on behalf of the client and returns the final result or an error.

### Iterative Querying
A resolver may query multiple DNS servers, following referrals until it reaches an authoritative answer.

## 5. Typical Resolution Flow

```text
Client
  ↓
Recursive Resolver
  ↓
Root
  ↓
TLD
  ↓
Authoritative Server
  ↓
Answer
  ↓
Client
```

Caching normally reduces repeated queries.

## 6. DNS Transport

Traditional DNS commonly uses:

```text
UDP/53
```

TCP/53 is also used in cases such as large responses and zone transfers.

Modern encrypted DNS services include:

- **DoT:** DNS over TLS
- **DoH:** DNS over HTTPS

## 7. Forward and Reverse DNS

### Forward lookup
Name → IP address.

### Reverse lookup
IP address → hostname using PTR records.

## 8. DNS Caching and TTL

DNS responses may be cached for a period specified by the record's **TTL (Time To Live)**.

Caching reduces latency and DNS query volume.

## 9. Common Commands

Windows:

```powershell
nslookup example.com
nslookup -type=MX example.com
```

Linux:

```bash
dig example.com
dig example.com A
dig -x 8.8.8.8
```

## 10. Common DNS Problems

- Wrong DNS server
- Missing record
- Expired/incorrect record
- Cache issues
- DNS forwarding failure
- Split-DNS configuration problems
- DNSSEC validation issues

## 11. DNS Security Concepts

Common DNS-related threats include:

- DNS spoofing
- Cache poisoning
- Domain hijacking
- Malicious domains
- DNS tunneling
- Domain generation algorithms

## 12. DNS Investigation Fields

Useful evidence includes:

```text
Timestamp
Client IP
Requested domain
Query type
Response code
Returned IP
DNS server
TTL
```

A single suspicious domain should be examined alongside endpoint, firewall, and process context.

## Key Takeaways

DNS is a distributed naming system, not merely a lookup table. Understand the hierarchy, record types, resolution process, caching, transport choices, and common security concerns.
