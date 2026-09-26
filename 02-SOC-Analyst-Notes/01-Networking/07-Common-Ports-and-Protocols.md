# Common Ports and Protocols

## 1. Overview

A **port number** identifies a transport-layer service endpoint. A protocol defines how communication works.

A common flow representation is:

```text
Source IP:Source Port → Destination IP:Destination Port / Protocol
```

Example:

```text
192.168.10.20:51542 → 203.0.113.50:443/TCP
```

## 2. Common TCP Ports

| Port | Protocol/Service | Typical Use |
|---:|---|---|
| 20 | FTP Data | FTP data channel |
| 21 | FTP Control | FTP control |
| 22 | SSH | Secure remote administration |
| 23 | Telnet | Remote terminal, unencrypted |
| 25 | SMTP | Mail transfer |
| 53 | DNS | DNS over TCP when required |
| 80 | HTTP | Web |
| 110 | POP3 | Email retrieval |
| 143 | IMAP | Email access |
| 443 | HTTPS | Web over TLS |
| 445 | SMB | Windows file/printer sharing |
| 587 | SMTP Submission | Authenticated mail submission |
| 993 | IMAPS | IMAP over TLS |
| 995 | POP3S | POP3 over TLS |
| 3389 | RDP | Remote Desktop |

## 3. Common UDP Ports

| Port | Protocol/Service | Typical Use |
|---:|---|---|
| 53 | DNS | Name resolution |
| 67 | DHCP Server | DHCP server port |
| 68 | DHCP Client | DHCP client port |
| 69 | TFTP | Trivial File Transfer |
| 123 | NTP | Time synchronization |
| 161 | SNMP | Network management |
| 162 | SNMP Trap | SNMP notifications |
| 500 | IKE | IPsec key exchange |
| 514 | Syslog | Traditional syslog over UDP |
| 520 | RIP | Routing Information Protocol |
| 4500 | IPsec NAT-T | NAT traversal for IPsec |

## 4. Important Protocols

### HTTP
Application protocol for web communication. Default port: TCP/80.

### HTTPS
HTTP protected by TLS. Default port: TCP/443.

### DNS
Resolves names to resource records. Commonly UDP/53, with TCP also used.

### DHCP
Automatically provides IPv4 network configuration. Uses UDP/67 and UDP/68.

### SSH
Encrypted remote shell and administration. TCP/22.

### RDP
Microsoft Remote Desktop. Commonly TCP/3389 and may also use UDP depending on configuration and version.

### SMB
Windows file and printer sharing. TCP/445 is the modern direct-hosted SMB port.

### SMTP
Email transfer and submission. Common ports include TCP/25 and TCP/587.

## 5. Important Notes

A port number is not proof of the application using it. Applications can be configured to use non-standard ports.

For example, an HTTP service can run on TCP/8080, and malware can use TCP/443 for encrypted command-and-control traffic.

Therefore:

```text
Port number ≠ guaranteed application identity
```

## 6. Port Ranges

TCP and UDP each have ports from `0–65535`.

Common categories are:

- **0–1023:** well-known ports
- **1024–49151:** registered ports
- **49152–65535:** dynamic/private ports

The exact assignment and conventions should be interpreted using current IANA registry information and application documentation.

## 7. Practical Identification

For:

```text
10.10.10.20:51532 → 10.10.10.50:22/TCP
```

Interpret:

- Source IP: `10.10.10.20`
- Source port: `51532`
- Destination IP: `10.10.10.50`
- Destination port: `22`
- Transport: TCP
- Expected service: SSH

## Key Takeaways

Ports help identify transport endpoints, while protocols define communication behavior. Always verify application identity using context such as process information, protocol payload, service banners, or logs rather than relying solely on a port number.
