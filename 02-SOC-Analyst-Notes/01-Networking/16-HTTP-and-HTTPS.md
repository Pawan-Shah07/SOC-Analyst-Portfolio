# HTTP and HTTPS

## 1. Overview

**HTTP (Hypertext Transfer Protocol)** is an application-layer protocol used for web communication.

**HTTPS** is HTTP protected by **TLS**.

Common ports:

```text
HTTP  → TCP/80
HTTPS → TCP/443
```

Port numbers are conventions, not guarantees.

## 2. HTTP Request-Response Model

```text
Client → HTTP Request → Server
Client ← HTTP Response ← Server
```

## 3. HTTP Request

A request contains elements such as:

- Method
- Request target
- Headers
- Optional body

Example:

```http
GET /index.html HTTP/1.1
Host: example.com
```

## 4. Common HTTP Methods

| Method | Typical Purpose |
|---|---|
| GET | Retrieve a resource |
| POST | Submit data/create processing action |
| PUT | Replace/update a resource |
| PATCH | Partial update |
| DELETE | Delete a resource |
| HEAD | Retrieve headers without normal response body |

## 5. HTTP Response

A response contains:

- Status code
- Headers
- Optional body

Example:

```http
HTTP/1.1 200 OK
Content-Type: text/html
```

## 6. Status Codes

### 1xx
Informational.

### 2xx
Success.

Examples:

```text
200 OK
201 Created
```

### 3xx
Redirection.

Examples:

```text
301 Moved Permanently
302 Found
304 Not Modified
```

### 4xx
Client error.

Examples:

```text
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
```

### 5xx
Server error.

Examples:

```text
500 Internal Server Error
502 Bad Gateway
503 Service Unavailable
```

## 7. HTTP Headers

Common headers include:

- Host
- User-Agent
- Accept
- Content-Type
- Content-Length
- Authorization
- Cookie
- Set-Cookie
- Referer
- Cache-Control

## 8. HTTPS

HTTPS uses HTTP over TLS.

Simplified stack:

```text
HTTP
 ↓
TLS
 ↓
TCP
 ↓
IP
```

HTTPS provides confidentiality and integrity for the protected connection when TLS is correctly implemented.

## 9. HTTP vs HTTPS

| Feature | HTTP | HTTPS |
|---|---|---|
| Default port | 80 | 443 |
| Encryption | No | TLS |
| Integrity protection | No TLS protection | Yes, via TLS |
| Certificate use | No TLS certificate | Usually yes |

## 10. Common Web Attacks

- SQL injection
- Cross-site scripting
- Path traversal
- Command injection
- Broken authentication
- Malicious file upload
- SSRF
- Credential stuffing

## Key Takeaways

Understand the HTTP request/response model, methods, status codes, headers, cookies, and how HTTPS adds TLS protection.
