# MCP Security Audit

Methodology for auditing Model Context Protocol (MCP) multi-server 
architectures. Scope definition, chain resolution, integrity scoring, 
and findings reporting.

> **Maintained by [Roland Caushaj](https://github.com/RolandCaushaj)**, 
> security researcher at [Logic4Hack](https://logic4hack.com) — 
> adversarial testing of LLM, RAG and agent systems.
>
> This is the methodology we apply in client engagements. The toolchain 
> that executes it, the detection criteria, and client findings are 
> proprietary and shared under NDA.

---

## What this repository is

An MCP deployment is not a single system. It is a chain of servers, 
each with its own identity, permissions, and trust relationships. 
Auditing it requires resolving the chain as the runtime sees it — 
not as the configuration file claims it is.

This repository documents the four-phase audit methodology we apply:

1. **Scoping** — defining the perimeter
2. **Chain resolution** — enumerating the live server chain
3. **Integrity scoring** — measuring depth, identity, and authentication
4. **Reporting** — producing reproducible findings

It does not include the execution toolchain or the case library. 
Those are proprietary and used in client engagements.

---

## Phase 1 — Scoping

The perimeter of an MCP audit is not the system. It is the chain the 
system trusts.

Scoping defines:

- **Which servers are in scope** — enumerated from the runtime, 
  not from the deployment configuration
- **Which tools each server exposes** — resolved per server, 
  not per session
- **Which credentials flow through the chain** — mapped to the 
  tools that can use them
- **Which external systems are reachable** — the blast radius, 
  not the entry point

Output of this phase: an attack-path map and a costed test plan. 
No testing occurs during scoping. Scoping is exploration.

---

## Phase 2 — Chain resolution

The chain is resolved from the live runtime, not from configuration.

For each server in the chain:

- **Identity** — is the server pinned to a known identity, or 
  admitted by name?
- **Authentication** — is the server authenticated on resolve, or 
  trusted by position?
- **Integrity** — is the server's descriptor verified, or accepted 
  as declared?
- **Capability** — which tools does it actually expose at resolve time?

The output is a resolved chain with per-node properties. A property 
is either **observed** (established by the collector from the runtime) 
or **asserted** (declared by the target). An asserted property is 
context, never assurance.

---

## Phase 3 — Integrity scoring

Each node contributes to a chain integrity score. The scoring model 
is internal. The dimensions are:

- **Chain length** — resolved depth against a safe threshold
- **Identity** — nodes without pinned identity reduce the score
- **Authentication** — unauthenticated nodes reduce the score
- **Integrity** — unverified descriptors reduce the score

A score alone is not a finding. A finding requires a **reproducible 
property violation** with a runnable command and a pass/fail criterion.

---

## Phase 4 — Reporting

Every finding ships with:

- **ID and severity** — assigned to the weakness, not the detection event
- **Business impact** — what an attacker can reach from this node
- **Reproduction** — step-by-step, with a runnable command
- **Classification** — mapped to OWASP MCP, MITRE ATLAS, NIST AI RMF, 
  ISO/IEC 42001
- **Remediation** — with a named owner
- **Closure** — a harness that asserts the property, exit 0 or 1

A finding is delivered in the same format to every client. The full 
report is built for procurement, auditors, and insurers — not rewritten 
before delivery.

---

## Worked example — LH-LAB-2026-001

The following finding is from our own lab, on our own infrastructure. 
It contains no client data. It is included here because it demonstrates 
the methodology end to end.

### LH-LAB-2026-001 — HIGH

**MCP server chain exceeds safe depth — single compromised node 
propagates downstream.**

#### Business impact

A chain of six MCP servers was resolved where the safe threshold is 
five. Trust is transitive along the chain: one compromised or 
substituted node reaches every tool downstream of it. The blast 
radius is not the entry point — it is everything the chain can call.

#### Reproduction

1. Enumerate the resolved server chain from the client runtime, not 
   from configuration.
2. Measure depth and identify nodes without pinned identity.
3. Flag chain depth above threshold and missing authentication per 
   node.

Result: chain depth 6 > threshold 5, flagged **MCP04**. Chain integrity 
score **70/100** under scoring model v1.3, with deductions for chain 
length and missing authentication. Reproduced by the verification 
harness, exit 0.

#### Classification

- **OWASP MCP04:2025 (Beta)** — Excessive chain length
- **MITRE ATLAS AML.T0051** — LLM prompt injection
- **NIST AI RMF** — MEASURE function
- **ISO/IEC 42001** — Controls mapping

Classification is controls mapping, not certification. Certification 
is issued by an accredited body.

#### Remediation

- Cap resolved chain depth.
- Pin server identity and verify on resolve.
- Allow-list tools per server, not per session.

#### Closure

Closed by a regression harness that asserts the property. Change the 
code and break the property, the harness fails.

---

## What's not in this repository

- The execution toolchain (ServerChainAuditor, PermissionEnforcer, 
  ToolAbuseDetector, MCPSecurityOrchestrator)
- The detection criteria for any of the 61 test cases
- The scoring model formula
- Client findings, client packs, or evidence artefacts
- The case library

Client engagements, anonymized by sector and perimeter, are shared 
under NDA on request.

---

## Data sovereignty

Audits run on hardware we own, in an isolated environment dedicated 
to a single engagement at a time. No client data reaches a third-party 
model API. No subprocessors are declared in the DPA.

- On-premises execution on owned DGX infrastructure
- Cross-model testing on locally hosted models
- Artefacts retained for 30 days, then destroyed
- Immediate destruction on written request

---

## About

[Logic4Hack](https://logic4hack.com) is an AI security firm 
specializing in adversarial testing of LLM, RAG, agent, and MCP 
systems. Two named researchers deliver every engagement. No 
subcontracting, no pyramid.

[Get in touch](https://logic4hack.com/contact) if you are shipping 
an AI system into production and need to prove its security to a 
customer, an auditor, or an insurer.

---

## License

Content in this repository is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). 
Code examples, if any, are licensed under MIT.

---

**Last updated**: October 2026  
**Status**: Active — methodology updated as MCP security research evolves
