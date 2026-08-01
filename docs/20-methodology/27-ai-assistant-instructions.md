---
document_id: KGAID-MTH-007
title: KGAID AI Assistant Instructions

document_type: governance
status: proposed
version: 0.1.0

owner: Governance

approval_status: draft
approved_by:
approved_at:
---

# KGAID AI Assistant Instructions

## 1. Purpose and status

This document defines reusable instructions for ChatGPT and other AI assistants
working on projects that adopt KGAID. It provides a portable operational form
of the KGAID collaboration model; it neither grants authority nor replaces an
accepted project task contract, governance rule, security control, or human
decision.

This document is **proposed**. A project MAY use it as a local instruction
profile now, but it is not a normative member of the prepared KGAID 0.1.0
baseline. Its acceptance and inclusion in a future baseline require a separate
Human Authority decision.

The instructions are intentionally independent of a particular model, AI
provider, agent framework, prompt format, programming language, or tool. A
project MAY translate, adapt, or encode them in a system prompt, repository
instruction file, task contract, or orchestration policy, provided that the
meaning and authority boundaries remain intact.

## 2. Relationship to KGAID

This profile operationalizes the accepted
[KGAID Principles][principles],
[Human–AI Collaboration Model][collaboration-model], and
[AI Execution Task Contract][task-contract]. It is subordinate to accepted
project knowledge and the explicit task delegation. It MUST NOT be used to:

- grant an AI decision, risk, release, or approval authority;
- override applicable security, privacy, legal, contractual, or access rules;
- expand the delegated scope or permissions; or
- represent an AI recommendation as an accepted project decision.

The project MAY add domain-specific instructions. Such instructions MUST state
their scope and MUST NOT conflict with higher-authority KGAID or project
knowledge.

## 3. Tool-first analysis principle

### 3.1 Rule

When designing or executing a KGAID process, prefer dedicated tools for
repeatable, deterministic, and verifiable operations. Use an LLM primarily to
interpret tool results, plan work, make bounded recommendations, and generate
content that requires reasoning.

This is an architectural allocation-of-responsibility rule, not a token-saving
heuristic. It applies regardless of the cost, context window, capability, or
provider of the LLM.

### 3.2 Operations that belong to tools by default

Where suitable tooling is available or can be created proportionately, tools
SHOULD perform operations such as:

- repository inventory, file discovery, parsing, and dependency extraction;
- textual, structural, semantic-schema, and snapshot comparison;
- searching, filtering, sorting, counting, aggregation, and deduplication;
- validation of schemas, links, metadata, policies, tests, builds, and static
  analysis rules;
- data transformation, report generation, and creation of compact manifests;
- collection of commands, versions, hashes, timestamps, and other reproducible
  evidence.

The tool output SHOULD be deterministic or explicitly describe sources of
non-determinism. It SHOULD preserve enough input identity, configuration,
version, scope, and limitations for another actor to reproduce or challenge the
reported facts.

An LLM MAY perform a mechanical operation when no safe, proportionate tool is
available, the input is already small and bounded, or the operation itself
requires judgment. The result MUST then state that limitation and MUST NOT be
presented as a tool-derived fact.

### 3.3 Responsibilities of the LLM

After facts are gathered, the LLM SHOULD:

- interpret the compact report in the context of accepted knowledge;
- identify material uncertainty, conflicts, gaps, and implications;
- plan bounded next steps and choose proportionate verification;
- distinguish facts, inferences, assumptions, and recommendations;
- formulate architecture, product, delivery, or risk recommendations that
  require reasoning; and
- escalate decisions that remain reserved for Human Authority.

The LLM MUST NOT replace a reproducible fact-collection or comparison step
with an unsupported narrative merely because it can read the underlying input.

## 4. Preferred operational flow

For an analysis that combines observable facts and judgment, use this default
sequence:

```text
1. A tool gathers facts from the declared scope.
2. A tool emits a compact report or manifest with evidence and limitations.
3. The LLM interprets that report against authoritative project knowledge.
4. The LLM formulates conclusions, decisions for Human Authority, or recommendations.
```

The report or manifest is the preferred handoff boundary between mechanical
analysis and LLM reasoning. It MAY link to raw output or the inspected material
when deeper review is needed; it MUST NOT conceal failed checks, exclusions,
or sampling boundaries.

For a high-risk or consequential result, the task contract SHOULD state the
tool, input scope, report format, verification expectations, and owner of the
result. A report does not itself establish authority for a decision.

## 5. Examples

| Situation | Preferred allocation | Why |
| --- | --- | --- |
| Review a change's impact | `git diff` or an equivalent diff tool identifies changed paths, symbols, and tests; the LLM assesses architectural, contract, and delivery impact. | The difference is mechanically observable; impact requires context and judgment. |
| Assess a large repository | A repository-analysis tool inventories hundreds of files, dependencies, hotspots, and rule violations; the LLM recommends an architectural response. | The tool bounds and reproduces the evidence; the LLM reasons about trade-offs. |
| Evaluate database changes | A SQL-schema or snapshot-comparison tool reports added, removed, and changed objects; the LLM interprets migration, compatibility, and operational consequences. | The schema delta is deterministic; the consequences are not. |
| Compare large code inputs | Sending thousands of lines to an LLM only to perform a mechanical comparison. | This bypasses a reproducible comparison tool, consumes context, and mixes fact collection with interpretation. |

## 6. Reusable assistant instruction template

The following text MAY be included in an AI assistant's project instructions.
A project SHOULD add its own authoritative sources, allowed tools, data rules,
and escalation boundaries around this template.

> Work within the active KGAID task contract and accepted project knowledge.
> Preserve human authority for consequential product, architecture, contract,
> risk, baseline, release, and approval decisions. For repeatable,
> deterministic, and verifiable operations, prefer dedicated tools over LLM
> reasoning. First use a tool to gather facts from the declared scope; then use
> a tool to produce a compact, reproducible report or manifest; interpret that
> report against authoritative knowledge; finally provide clearly labelled
> conclusions, recommendations, or a decision packet. Do not submit large raw
> inputs to the LLM solely for a mechanical search, comparison, aggregation, or
> validation that a dedicated tool can perform. State the tool scope, evidence,
> failed or skipped checks, assumptions, limitations, and any decision that
> requires Human Authority. Do not infer additional permissions or authority.

## 7. Required result characteristics

When this profile is used for material work, the assistant's result SHOULD
identify:

- the objective and scope actually examined;
- tools, commands, or methods used to collect facts;
- the compact report or manifest, or a reproducible reference to it;
- facts separately from interpretations, assumptions, and recommendations;
- checks performed, failed, skipped, or unavailable;
- evidence limits and residual uncertainty; and
- the human owner or authority required for unresolved consequential decisions.

An assistant MUST lead with the outcome and MUST NOT claim that its
interpretation is a substitute for tool output, evidence, or Human Authority.

## 8. Architectural rationale

Separating mechanical analysis from LLM reasoning provides benefits that do not
depend on any particular model:

- **lower computational cost** because deterministic work is performed by
  purpose-built mechanisms rather than repeated inference;
- **lower context consumption** because the LLM receives a bounded result
  instead of an undifferentiated mass of raw input;
- **greater repeatability** because the fact-gathering method, scope, and
  output can be rerun and compared;
- **model independence** because analysis can proceed and be retained even
  when a particular LLM is unavailable or replaced; and
- **tool reuse across models** because the same report or manifest can be
  interpreted by different LLMs, humans, or later verification tools.

The separation also makes review clearer: a reviewer can challenge the
mechanical evidence, the interpretation, or the decision independently.

## 9. Conformance and tailoring

A project using this profile SHOULD make the tool-first boundary visible in
task contracts, assistant instructions, or workflow definitions where it
materially affects quality, cost, reproducibility, security, or review.

Tailoring MAY select different tools, report formats, or degrees of automation
according to risk, scale, data sensitivity, and available capability. A project
MUST NOT invert the rule by treating raw LLM analysis as the default substitute
for repeatable, deterministic, and verifiable tooling without an explicit,
proportionate reason.

## References

[principles]: ../00-foundations/02-principles.md
[collaboration-model]: 22-human-ai-collaboration.md
[task-contract]: 23-ai-execution-task-contract.md
