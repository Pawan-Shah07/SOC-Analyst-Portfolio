# VPN

## 1. Overview

A **Virtual Private Network (VPN)** creates a protected logical communication path over an underlying network such as the Internet.

VPNs are commonly used for:

- Remote access
- Site-to-site connectivity
- Protected inter-office communication
- Secure access to private services

## 2. VPN Types

### Remote-Access VPN
Connects an individual endpoint to an organization.

```text
Remote User
    ↓
Internet
    ↓
VPN Gateway
    ↓
Internal Network
```

### Site-to-Site VPN
Connects two networks.

```text
Office A
   ↓
VPN Gateway
   ║ Encrypted Tunnel
VPN Gateway
   ↓
Office B
```

## 3. IPsec VPN

IPsec is a suite of protocols for securing IP communication.

Common concepts include:

- Authentication
- Encryption
- Integrity
- Security associations
- IKE key exchange

Common IPsec-related ports:

```text
UDP/500  → IKE
UDP/4500 → NAT-T
```

ESP is IP protocol number 50 and is not a TCP/UDP port.

## 4. SSL/TLS VPN

Some remote-access VPN products use TLS-based mechanisms rather than traditional IPsec.

The exact architecture depends on the vendor and product.

## 5. Tunneling

A VPN encapsulates protected traffic inside another communication path.

Conceptually:

```text
Original Traffic
      ↓
Encryption/Encapsulation
      ↓
VPN Tunnel
      ↓
Decapsulation/Decryption
      ↓
Original Traffic
```

## 6. Split Tunneling

With split tunneling, only selected traffic uses the VPN tunnel while other traffic goes directly to the Internet.

### Full Tunnel
All or most client traffic uses the VPN.

### Split Tunnel
Only designated traffic uses the VPN.

Each design has security and performance implications.

## 7. VPN Security Considerations

- Strong authentication
- MFA
- Modern cryptography
- Patch management
- Least privilege
- Device posture checks where available
- Restricted network access after connection

## 8. VPN Troubleshooting

Check:

- Authentication
- Client configuration
- DNS
- Routes
- Firewall rules
- MTU/MSS issues
- Certificate validity
- Time synchronization
- VPN gateway availability

## Key Takeaways

Understand the difference between remote-access and site-to-site VPNs, the basic concepts of IPsec and TLS-based VPNs, tunneling, split tunneling, and the security controls around VPN access.
