# SPY Protocol

[![Version](https://img.shields.io/badge/version-1.0-blue.svg)](versions/1.0.md)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-draft-orange.svg)](SPECIFICATION.md)

## Secure Proxy Authentication Protocol

SPY Protocol enables cryptographic authentication between user agents and proxies to control access to protected resources, without passwords or behavioral tracking.

## Overview

SPY provides a standardized method for:
- **Strong Authentication** - ECDSA-based cryptographic proof
- **Zero Passwords** - Public key authentication only
- **Session Management** - Secure token generation and validation
- **Bot Protection** - Cryptographic agent verification
- **Enterprise Control** - Per-domain authentication policies

## Quick Start

### For Implementers

1. Read the [SPECIFICATION](SPECIFICATION.md)
2. Review [version 1.0](versions/1.0.md) requirements
3. Check [test vectors](test-vectors/) for validation
4. Use [JSON schemas](schemas/) for message validation

### For System Administrators

SPY Protocol requires:
- An SPY-compatible proxy (gatekeeper)
- An SPY-compatible agent (authenticated browser/client)
- ECDSA key pairs (P-256 or P-384)

## Protocol Flow

```
Agent → Proxy: SPY_INIT (public key, capabilities)
Proxy → Agent: SPY_CHALLENGE (challenge, requirements)
Agent → Proxy: SPY_AUTH (signed challenge)
Proxy → Agent: SPY_ACCEPT (session token)
```

## Implementation Status

### Reference Implementations
- [ ] Go implementation
- [ ] Rust implementation  
- [ ] JavaScript/TypeScript implementation
- [ ] Python implementation

### Compatible Software
*No compatible implementations yet. Be the first!*

## Specification Versions

| Version | Status | Date | Description |
|---------|--------|------|-------------|
| [1.0](versions/1.0.md) | Draft | 2025-01 | Initial specification |

## Contributing

We welcome contributions to the SPY Protocol specification:

1. **Propose Changes** - Open an issue describing your proposal
2. **Submit PRs** - For typos, clarifications, or minor improvements
3. **Implement** - Build SPY support and share your experience
4. **Test** - Validate implementations against test vectors

## Security Considerations

- SPY Protocol requires secure key storage on agents
- Time synchronization (±5 minutes) is required
- Proxies should implement rate limiting
- See [SECURITY.md](SECURITY.md) for detailed analysis

## Adoption

To implement SPY Protocol in your software:

### For Proxy Developers
Implement these endpoints:
- `/spy/init` - Handle initial handshake
- `/spy/auth` - Validate authentication
- Session management with configurable timeouts

### For Agent Developers
Implement:
- ECDSA key generation and storage
- SPY message formatting and signing
- Session token management
- Heartbeat mechanism

## Resources

- [Specification](SPECIFICATION.md) - Complete protocol specification
- [JSON Schemas](schemas/) - Message validation schemas
- [Test Vectors](test-vectors/) - Reference test cases
- [Examples](examples/) - Configuration examples

## Community

- GitHub Issues - For specification discussions
- Implementation Reports - Share your experience

## License

The SPY Protocol specification is released under the [MIT License](LICENSE).

## Acknowledgments

SPY Protocol builds upon established standards:
- RFC 8446 (TLS 1.3) - Cryptographic practices
- RFC 7519 (JWT) - Token formats
- NIST SP 800-186 - Elliptic curve standards

---

*SPY Protocol - Secure authentication without surveillance*
