# LH-LAB-2026-002 — CRITICAL

**Server admitted into the chain without pinned identity.**

---

## Business impact

An MCP server was admitted into the resolved chain without a pinned identity. The runtime accepted the server based on its declared name, not on a cryptographic property.

An attacker who registers a server with the same name — name collision — can substitute the trusted server and inherit its position in the chain. The permission layer does not stop the call, because the call originates from a name the client already trusts.

This requires no privilege on the client, only the ability to register a name.

## Reproduction

1. Resolve the chain from the client runtime.
2. Inspect each node for pinned identity (key, certificate, signed descriptor).
3. Flag any node admitted by name alone.

Result: server admitted without pinned identity, flagged **MCP03:2025** and **MCP01:2025 (Beta)**. Chain integrity score **60/100** under scoring model v1.3.

## Classification

- **OWASP MCP03:2025** — Tool poisoning (Beta)
- **OWASP MCP01:2025 (Beta)** — Server resolved without authentication
- **MITRE ATLAS AML.T0051** — LLM prompt injection
- **NIST AI RMF** — GOVERN, MEASURE
- **ISO/IEC 42001** — Access control

## Remediation

- Pin server identity by cryptographic property, not by name.
- Verify identity on resolve, not on declaration.
- Fail closed on unknown servers.

## Closure

Harness exit 0. Closed by a regression harness that asserts pinned identity on resolve.

---

*This finding is from our own lab. It contains no client data. The scoring formula, execution runner, and detection criteria are proprietary.*
