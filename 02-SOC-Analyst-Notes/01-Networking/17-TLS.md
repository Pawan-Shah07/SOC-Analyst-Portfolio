# TLS

## 1. Overview

**Transport Layer Security (TLS)** is a cryptographic protocol used to protect network communication.

TLS provides:

- Confidentiality
- Integrity
- Server authentication through certificates
- Optional client authentication

HTTPS uses TLS to protect HTTP communication.

## 2. TLS Goals

### Confidentiality
Attackers should not be able to read protected application data in transit.

### Integrity
Unauthorized modification should be detectable.

### Authentication
Certificates can help a client verify the identity associated with a server endpoint.

## 3. TLS Handshake Concept

A simplified TLS 1.3 flow is:

```text
ClientHello
    ↓
ServerHello + Certificate + Handshake Messages
    ↓
Key Agreement
    ↓
Encrypted Application Data
```

The exact handshake depends on TLS version and negotiated options.

## 4. Certificates

A TLS certificate can contain information such as:

- Subject identity
- Subject Alternative Names (SANs)
- Public key
- Issuer
- Validity period
- Signature algorithm
- Certificate signature

## 5. Certificate Chain

A client validates a certificate through a chain of trust:

```text
Root CA
   ↓
Intermediate CA
   ↓
Server Certificate
```

The root CA must be trusted by the client for normal public PKI validation.

## 6. Symmetric vs Asymmetric Cryptography

### Asymmetric
Uses public/private key pairs and supports authentication/key agreement operations.

### Symmetric
Uses shared secret keys for efficient encryption of application data.

TLS uses both concepts rather than relying on only one type of cryptography.

## 7. TLS Versions

Modern secure deployments should use current TLS versions supported by the environment, typically TLS 1.2 or TLS 1.3. Older versions such as TLS 1.0 and TLS 1.1 are obsolete and should not be enabled in normal modern deployments.

## 8. Common TLS Problems

- Expired certificate
- Hostname mismatch
- Untrusted certificate authority
- Incompatible protocol version
- Weak cipher configuration
- Incorrect system time
- Missing intermediate certificate

## 9. TLS and Visibility

Because HTTPS encrypts application data, network monitoring may see:

- Source/destination IP
- Port
- TLS version
- Certificate information depending on visibility
- SNI where applicable
- Connection timing and volume

but not necessarily the plaintext HTTP request without endpoint or controlled decryption visibility.

## 10. TLS and Security Monitoring

Useful indicators include:

- Unexpected external destinations
- Suspicious certificate patterns
- Unusual TLS versions/ciphers
- Rare destinations
- Abnormal connection timing
- Endpoint process associated with the TLS connection

## Key Takeaways

TLS protects data in transit and authenticates servers through certificates. Understand certificates, CA chains, handshake concepts, TLS versions, and the limitations of network-only visibility into encrypted traffic.
