# Audit Phases

The four phases of an MCP security audit. Each phase produces an artefact that the next phase consumes, and has a defined exit condition.

---

## Phase 1 — Scoping

**Goal**: define the perimeter that will actually be tested.

The perimeter of an MCP deployment is not the system. It is the chain the system trusts.

In this phase:

- Map the architecture as deployed, not as documented
- Identify trust boundaries between components
- Enumerate what the system can actually reach
- Select the applicable subset of the case library
- Produce a costed test plan

**Output**: attack-path map and signed scope.

**Exit condition**: scope signed by both parties. No testing occurs in this phase.

---

## Phase 2 — Chain resolution

**Goal**: enumerate the live chain as the runtime sees it.

The chain is resolved from the client runtime, not from configuration. For each server:

- **Identity** — pinned or admitted by name?
- **Authentication** — authenticated on resolve, or trusted by position?
- **Integrity** — descriptor verified, or accepted as declared?
- **Capability** — which tools exposed at resolve time?

**Output**: resolved chain with per-node properties.

**Exit condition**: every node has observed (not asserted) properties. An asserted property is context, never assurance.

---

## Phase 3 — Integrity scoring

**Goal**: produce a per-chain integrity score.

Dimensions:

- Chain length against safe threshold
- Nodes without pinned identity
- Nodes without authentication
- Nodes with unverified descriptors

**Output**: chain integrity score.

**Exit condition**: score recorded with rationale per dimension. A score alone is not a finding. A finding requires a reproducible property violation.

---

## Phase 4 — Reporting

**Goal**: produce evidence that survives vendor assessment.

Every finding ships with:

- ID and severity (assigned to the weakness)
- Business impact in plain language
- Step-by-step reproduction
- Framework classification
- Remediation with named owner
- Closure condition

**Output**: findings report, evidence pack, executive summary.

**Exit condition**: report delivered. Retest available within 30 days of client remediation notice.

---

## Related

- [mcp-security-reference](https://github.com/RolandCaushaj/mcp-security-reference) — patterns
- [ai-security-assurance](https://github.com/RolandCaushaj/ai-security-assurance) — case library
- [llm-red-team-playbook](https://github.com/RolandCaushaj/llm-red-team-playbook) — engagement phases
