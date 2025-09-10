# Changelog

All notable changes to the SPY Protocol specification will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### To Be Determined
- Post-quantum cryptography support
- Hardware token integration
- Multi-factor authentication extensions
- Behavioral attestation (optional)

## [1.0.0] - 2025-01-01

### Added
- Initial SPY Protocol specification
- Four-message authentication handshake
- ECDSA-based cryptographic authentication
- Session management with heartbeats
- Rate limiting recommendations
- Security considerations and threat model
- Test vector structure
- JSON schema definitions

### Specified
- SPY_INIT message format
- SPY_CHALLENGE message format
- SPY_AUTH message format
- SPY_ACCEPT message format
- SPY_HEARTBEAT mechanism
- Error codes and handling

### Security
- Replay attack prevention
- MITM protection requirements
- DoS mitigation strategies
- Key management guidelines

### Cryptography
- NIST P-256 (REQUIRED)
- NIST P-384 (RECOMMENDED)
- SHA-256/SHA-384 hashing
- ECDSA signatures

## Pre-Release History

### 2024-12 - Concept Development
- Initial protocol design
- Security model definition
- Message flow architecture

### 2024-11 - Research Phase
- Review of existing authentication protocols
- Analysis of enterprise requirements
- Cryptographic algorithm selection

---

For detailed version information, see [versions/](versions/).

[Unreleased]: https://github.com/spy-protocol/spy-protocol/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/spy-protocol/spy-protocol/releases/tag/v1.0.0