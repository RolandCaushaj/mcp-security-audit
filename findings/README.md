# Findings register — Logic4Hack OÜ

Register of findings from our own lab. Each finding is:

- **Reproducible** — runnable command, exit 0 or 1
- **Classified** — mapped to a public control
- **Closed** — by a harness asserting the property

Severity is assigned to the weakness, never to the detection event. Controls that hold are recorded as coverage.

---

## Register

| ID | Severity | Weakness | Classification | Closure |
|---|---|---|---|---|
| [LH-LAB-2026-001](LH-LAB-2026-001-chain-depth.md) | HIGH | MCP chain depth above threshold | OWASP MCP04 · MITRE AML.T0051 · NIST AI RMF · ISO/IEC 42001 | harness exit 0 |
| [LH-LAB-2026-002](LH-LAB-2026-002-unpinned-identity.md) | CRITICAL | Server without pinned identity | OWASP MCP03 · MCP01 (Beta) | harness exit 0 |

---

## What's not here

The full register includes reproduction commands, scoring model inputs, and closure harnesses. Client findings are shared under NDA in the same format. Both are proprietary.

---

## Format

A finding sheet contains:

- ID and severity with rationale
- Business impact in plain language
- Step-by-step reproduction
- Classification (framework mapping)
- Remediation with a named owner
- Closure condition

The same format is used for lab findings and client findings.

---

## Related

- [mcp-security-reference](https://github.com/RolandCaushaj/mcp-security-reference) — patterns and considerations
- [ai-security-assurance](https://github.com/RolandCaushaj/ai-security-assurance) — the 61-case library
- [llm-red-team-playbook](https://github.com/RolandCaushaj/llm-red-team-playbook) — engagement phases
