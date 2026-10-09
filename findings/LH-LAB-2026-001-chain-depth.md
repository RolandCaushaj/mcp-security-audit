# LH-LAB-2026-001 — HIGH

**MCP server chain exceeds safe depth — single compromised node propagates downstream.**

---

## Business impact

A chain of six MCP servers was resolved where the safe threshold is five. Trust is transitive along the chain: one compromised or substituted node reaches every tool downstream of it. The blast radius is not the entry point — it is everything the chain can call.

## Reproduction

1. Enumerate the resolved server chain from the client runtime, not from configuration.
2. Measure depth and identify nodes without pinned identity.
3. Flag chain depth above threshold and missing authentication per node.

Result: chain depth 6 > threshold 5, flagged **MCP04**. Chain integrity score **70/100** under scoring model v1.3. Reproduced by the verification harness, exit 0.

## Classification

- **OWASP MCP04:2025 (Beta)** — Excessive chain length
- **MITRE ATLAS AML.T0051** — LLM prompt injection
- **NIST AI RMF** — MEASURE function
- **ISO/IEC 42001** — Controls mapping

## Remediation

- Cap resolved chain depth.
- Pin server identity and verify on resolve.
- Allow-list tools per server, not per session.

## Closure

Harness exit 0. Closed by a regression harness that asserts the property.

---

*This finding is from our own lab. It contains no client data. The scoring formula, execution runner, and detection criteria are proprietary.*
