# SPY Protocol Specification

**Current Version**: 1.0  
**Status**: Draft  
**Last Updated**: January 2025

## About This Document

This document provides an overview of the SPY Protocol specification. For the complete technical specification of the current version, see [versions/1.0.md](versions/1.0.md).

## Abstract

The SPY (Secure Proxy Authentication) Protocol enables cryptographic authentication between user agents and authenticating proxies to control access to protected resources. This specification defines a lightweight, efficient protocol using elliptic curve cryptography for mutual authentication and session establishment.

## Quick Navigation

- **[Full v1.0 Specification](versions/1.0.md)** - Complete protocol details
- **[Security Considerations](SECURITY.md)** - Threat model and mitigations  
- **[Implementation Guide](CONTRIBUTING.md)** - How to implement SPY
- **[Change Log](CHANGELOG.md)** - Version history

## Protocol Overview

SPY Protocol provides:
- **Passwordless Authentication** - ECDSA public key cryptography
- **Bot Protection** - Cryptographic proof of authorized agents
- **Session Management** - Secure token generation and validation
- **Enterprise Ready** - Audit logging and policy configuration

### Core Flow

```
1. Agent → Proxy: SPY_INIT (public key, capabilities)
2. Proxy → Agent: SPY_CHALLENGE (challenge, requirements)  
3. Agent → Proxy: SPY_AUTH (signed challenge)
4. Proxy → Agent: SPY_ACCEPT (session token)
```

## Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

- **Agent**: A client application implementing SPY Protocol for authentication
- **Proxy**: A server implementing SPY Protocol to authenticate agents
- **Protected Resource**: A service or application protected by the proxy
- **Session**: An authenticated connection between agent and proxy
- **Challenge**: A cryptographic nonce used to prevent replay attacks

## Implementation Requirements Summary

### Minimum Requirements (MUST)

- ECDSA with NIST P-256 curve
- SHA-256 hashing
- JSON message encoding
- Challenge expiry (60 seconds)
- Timestamp validation (±5 minutes)

### Recommended Features (SHOULD)

- ECDSA with NIST P-384 curve
- SHA-384 hashing
- Rate limiting
- Heartbeat mechanism
- Session token rotation

## Message Transport Options

SPY messages can be transported over:
- **HTTPS** - POST to `/spy/v1/{message_type}`
- **WebSocket** - Text frames with JSON payload
- **HTTP/2 or HTTP/3** - Streaming with multiplexing

## Conformance Levels

### Basic Compliance
- Core message flow (INIT, CHALLENGE, AUTH, ACCEPT)
- P-256 ECDSA support
- 60-second challenge timeout
- JSON message format

### Full Compliance  
- All basic requirements
- P-384 ECDSA support
- Heartbeat mechanism
- Rate limiting
- Configurable timeouts

## Getting Started

### For Implementers

1. Read the [full v1.0 specification](versions/1.0.md)
2. Review [security considerations](SECURITY.md)
3. Implement message handlers for SPY_INIT, SPY_CHALLENGE, SPY_AUTH, SPY_ACCEPT
4. Add session management and heartbeat support
5. Validate against test vectors (when available)

### For System Administrators

1. Deploy an SPY-compatible proxy
2. Configure agent authentication policies
3. Generate and distribute ECDSA key pairs
4. Monitor authentication logs
5. Plan key rotation schedule

## Version History

| Version | Status | Date | Link |
|---------|--------|------|------|
| 1.0 | Current | 2025-01 | [Specification](versions/1.0.md) |

Future versions will maintain backward compatibility where possible.

## Contributing

We welcome contributions to improve the SPY Protocol specification. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Security

For security considerations and threat analysis, see [SECURITY.md](SECURITY.md).

Report security issues privately - do not open public issues for vulnerabilities.

## References

- RFC 2119: Key words for use in RFCs
- RFC 7159: JavaScript Object Notation (JSON)
- RFC 7468: Textual Encodings of PKIX Structures
- RFC 4648: Base16, Base32, and Base64 Data Encodings
- NIST SP 800-186: Discrete Logarithm-Based Crypto

## License

This specification is released under the MIT License. See [LICENSE](LICENSE) for details.
