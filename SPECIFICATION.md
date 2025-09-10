# SPY Protocol Specification

**Current Version**: 1.0  
**Status**: Draft  
**Last Updated**: January 2025

## Abstract

The SPY (Secure Proxy Authentication) Protocol enables cryptographic authentication between user agents and authenticating proxies to control access to protected resources. This specification defines a lightweight, efficient protocol using elliptic curve cryptography for mutual authentication and session establishment.

## Table of Contents

1. [Introduction](#introduction)
2. [Terminology](#terminology)
3. [Protocol Overview](#protocol-overview)
4. [Message Specifications](#message-specifications)
5. [Cryptographic Requirements](#cryptographic-requirements)
6. [Security Considerations](#security-considerations)
7. [Implementation Requirements](#implementation-requirements)
8. [Conformance](#conformance)

## Introduction

SPY Protocol addresses the need for strong, passwordless authentication between clients and proxies while preventing unauthorized automated access to protected resources. The protocol uses established cryptographic standards to ensure security while maintaining simplicity and performance.

## Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

- **Agent**: A client application implementing SPY Protocol for authentication
- **Proxy**: A server implementing SPY Protocol to authenticate agents
- **Protected Resource**: A service or application protected by the proxy
- **Session**: An authenticated connection between agent and proxy
- **Challenge**: A cryptographic nonce used to prevent replay attacks

## Protocol Overview

SPY Protocol uses a four-message handshake:

1. **SPY_INIT**: Agent announces capabilities and public key
2. **SPY_CHALLENGE**: Proxy provides authentication challenge
3. **SPY_AUTH**: Agent proves possession of private key
4. **SPY_ACCEPT**: Proxy confirms authentication and issues session

After establishment, sessions are maintained through periodic heartbeats.

## Message Specifications

All messages MUST be encoded as JSON (RFC 7159) with UTF-8 encoding.

### Message Transport

Messages MAY be transported over:
- HTTPS POST requests to `/spy/v1/{message_type}`
- WebSocket frames with text payload
- HTTP/2 or HTTP/3 streams

### Message Structure

Every message MUST contain:
- `type`: String identifying message type
- `version`: Protocol version string
- `timestamp`: ISO 8601 timestamp with timezone

### Detailed Message Formats

See [versions/1.0.md](versions/1.0.md) for complete message specifications.

## Cryptographic Requirements

### Supported Algorithms

Implementations MUST support:
- **ECDSA** with NIST P-256 (secp256r1)
- **SHA-256** for hashing

Implementations SHOULD support:
- **ECDSA** with NIST P-384 (secp384r1)
- **SHA-384** for hashing

### Key Encoding

Public keys MUST be encoded in:
- PEM format (RFC 7468) for configuration
- Base64 (RFC 4648) for transmission

### Randomness

All random values MUST be generated using cryptographically secure random number generators with at least 128 bits of entropy.

## Security Considerations

### Replay Protection

- Challenges MUST be unique and expire after 60 seconds
- Timestamps MUST be verified within ±5 minutes
- Session tokens MUST be unguessable (minimum 256 bits entropy)

### Denial of Service

Implementations SHOULD:
- Rate limit authentication attempts per IP address
- Implement exponential backoff for failed attempts
- Limit concurrent pending authentications

### Key Management

- Private keys MUST be stored securely (hardware security module recommended)
- Public keys SHOULD be rotated periodically
- Compromised keys MUST be revocable

## Implementation Requirements

### Agent Requirements

Agents MUST:
- Securely store private keys
- Validate proxy certificates (for HTTPS transport)
- Maintain accurate time (NTP recommended)
- Handle session expiration gracefully

### Proxy Requirements

Proxies MUST:
- Verify signatures correctly
- Maintain session state securely
- Log authentication events for audit
- Support configurable policies per domain

## Conformance

### Compliance Levels

**Basic Compliance**:
- Support P-256 ECDSA
- Implement core message flow
- 60-second challenge timeout

**Full Compliance**:
- Support P-256 and P-384
- Implement heartbeat mechanism
- Configurable timeouts
- Rate limiting

### Testing

Implementations SHOULD validate against official test vectors in [test-vectors/](test-vectors/).

## References

- RFC 2119: Key words for use in RFCs
- RFC 7159: JavaScript Object Notation (JSON)
- RFC 7468: Textual Encodings of PKIX Structures
- RFC 4648: Base16, Base32, and Base64 Data Encodings
- NIST SP 800-186: Discrete Logarithm-Based Crypto

## Version History

See [versions/](versions/) for all specification versions.

## License

This specification is released under the MIT License. See [LICENSE](LICENSE) for details.