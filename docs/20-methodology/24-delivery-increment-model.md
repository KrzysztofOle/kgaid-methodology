---
document_id: KGAID-MTH-004
title: KGAID Delivery Increment Model

document_type: capability
status: accepted
version: 0.1.0

owner: Product

approval_status: pending
approved_by:
approved_at:
---

# KGAID Delivery Increment Model

## 1. Purpose

This document defines the KGAID Delivery Increment: the bounded unit through which accepted product and project knowledge is transformed into an integrated, verified, and reviewable result.

It explains:

- how an increment relates to product outcomes, capabilities, contracts, tasks, baselines, and releases;
- how a valuable or necessary slice is selected;
- which knowledge an increment MUST contain or reference;
- when an increment is ready for realization;
- how it is decomposed into AI Execution Task Contracts;
- how humans, a Knowledge and Review AI, and Execution AI collaborate;
- how implementation, integration, verification, and acceptance are coordinated;
- how discoveries and scope changes are governed;
- when an increment MAY be called implemented, verified, baselined, released, or complete.

The model is independent of planning method, programming language, architecture style, repository platform, and AI provider.

## 2. Definition

A **Delivery Increment**, represented by the KGAID artifact type **INC**, is a bounded unit selected for realization that:

- serves an accepted product outcome, external obligation, risk reduction, migration, operational need, or explicit learning goal;
- has an identifiable scope and non-goals;
- derives from sufficiently mature upstream knowledge;
- has explicit acceptance criteria;
- identifies architecture and contract boundaries;
- can be implemented and integrated coherently;
- can be evaluated through proportionate evidence;
- preserves known limitations and residual risk;
- produces a result for which a human can make a meaningful acceptance decision.

An increment is a unit of governed outcome, not merely a container of activities.

## 3. Relationship to Other Units

| Unit | Relationship to increment |
| --- | --- |
| **Product** | Supplies vision, boundaries, desired outcomes, and success measures. |
| **Capability** | Describes an enduring product ability that one or more increments MAY realize or evolve. |
| **Requirement** | Defines an obligation that constrains one or more increments. |
| **Architecture decision** | Constrains how the increment MAY be realized. |
| **Contract** | Defines observable obligations the increment MUST preserve or implement. |
| **AI Execution Task Contract** | Delegates one bounded portion of increment realization to an Execution AI. |
| **Implementation revision** | Contains the realized system change. |
| **Evidence** | Supports exact claims about the increment and implementation. |
| **Knowledge baseline** | Binds accepted knowledge, implementation, evidence, limitations, and risk. |
| **Release** | Applies an authorized delivery decision to one or more baselined increments and a target environment. |
| **Outcome measurement** | Determines whether released behavior contributes to the intended product result. |

One capability MAY require several increments. One increment MAY affect several capabilities when the scope remains coherent and the shared result can be evaluated meaningfully.

One increment MAY contain several execution tasks. Completion of every task does not by itself prove increment completion.

## 4. Increment Types

KGAID recognizes several useful increment intents.

| Type | Intended result |
| --- | --- |
| **Product increment** | Delivers or changes user- or stakeholder-observable capability. |
| **Enabling increment** | Establishes an architecture, platform, data, or integration ability required by later product work. |
| **Risk-reduction increment** | Produces evidence or change that reduces a material uncertainty or risk. |
| **Learning increment** | Tests an explicit hypothesis and produces decision-relevant evidence. |
| **Compliance increment** | Satisfies or demonstrates an external legal, regulatory, contractual, or policy obligation. |
| **Migration increment** | Moves data, consumers, behavior, or infrastructure between accepted states. |
| **Operational increment** | Improves observability, reliability, recoverability, security operations, support, or cost control. |
| **Corrective increment** | Corrects a verified defect, incident cause, security weakness, or contract violation. |

The type does not change KGAID authority, traceability, or evidence rules.

An enabling increment MUST state the downstream capability or constraint it enables. A learning increment MUST state the decision its evidence is intended to support. An activity such as “refactor module” is not a sufficient increment outcome unless the required system property and evidence are explicit.

## 5. Good Increment Properties

A well-shaped increment SHOULD be:

- **outcome-oriented** — it produces value, obligation satisfaction, risk reduction, or learning;
- **bounded** — included and excluded scope are explicit;
- **coherent** — its parts contribute to one understandable result;
- **traceable** — its need, constraints, implementation, and evidence are connected;
- **contract-aware** — affected observable obligations and consumers are known;
- **independently evaluable** — its declared claim can be verified without relying on vague future work;
- **small enough to control** — uncertainty and review remain manageable;
- **large enough to matter** — completion changes knowledge, capability, risk, or operational state meaningfully;
- **compatible or migration-ready** — consequences for existing valid uses are addressed;
- **reversible where practical** — rollback, containment, or alternative path is understood;
- **evidence-ready** — verification can be designed before completion;
- **authority-ready** — required human owners and decision roles are known.

These properties are evaluated proportionately. A small internal correction and a regulated production migration need different depth.

## 6. Slicing Rules

An increment SHOULD be sliced around an observable outcome or decision boundary.

Preferred slicing dimensions include:

- user or business scenario;
- capability behavior;
- contract or consumer boundary;
- risk or uncertainty;
- migration step with a stable coexistence point;
- operational property;
- compliance obligation;
- vertical path through architecture;
- experiment with a clear learning question.

A slice SHOULD avoid:

- distributing one acceptance claim across unrelated increments;
- hiding unfinished behavior behind task completion;
- creating a component that cannot be evaluated until unspecified future work;
- mixing unrelated product outcomes;
- combining high-risk irreversible change with unrelated routine work;
- requiring many contracts to change without explicit coordination;
- claiming vertical value for a purely technical activity.

A horizontal technical slice MAY be valid as an enabling increment when its outcome, downstream dependency, acceptance criteria, and limitations are explicit.

An increment SHOULD be split when:

- it has more than one independent outcome or decision authority;
- parts can be accepted, released, or rolled back independently;
- different parts have materially different risk or evidence needs;
- unresolved knowledge in one part blocks otherwise valid work;
- the contract or migration boundaries are easier to control separately;
- the task set becomes too large for reliable impact analysis and review.

Increments SHOULD be combined only when separation would destroy a meaningful end-to-end claim or create unsafe intermediate states.

## 7. Increment Knowledge Structure

A material Increment artifact SHOULD contain or reference:

### 7.1 Identity

- stable Increment identifier;
- title and revision;
- owner;
- knowledge status;
- delivery status;
- verification status;
- applicable KGAID version and profile.

### 7.2 Intent

- increment type;
- product outcome, obligation, risk, or learning goal;
- rationale and urgency;
- affected stakeholders and capabilities;
- intended completion claim.

### 7.3 Scope

- included scenarios, behavior, data, components, environments, and consumers;
- explicit exclusions and non-goals;
- boundaries with adjacent increments;
- allowed incidental change;
- compatibility and migration scope.

### 7.4 Upstream knowledge

- product vision and boundaries;
- terminology and business rules;
- use cases and scenarios;
- functional and quality requirements;
- external constraints;
- assumptions and risks.

### 7.5 Architecture and contracts

- applicable architecture specifications and decisions;
- affected ownership and dependency boundaries;
- system and component contracts;
- versioning and compatibility expectations;
- security, privacy, failure, and operational boundaries.

### 7.6 Acceptance and evidence

- acceptance criteria;
- intended verification methods;
- required environments;
- evidence expectations;
- limitations that will remain outside the claim;
- required human reviews and authorities.

### 7.7 Delivery structure

- AI Execution Task Contracts and human tasks;
- task dependencies;
- integration points;
- baseline and target revisions;
- deployment, migration, or rollout needs;
- rollback or containment;
- operational follow-up.

### 7.8 Governance

- Product, Domain, Architecture, Contract, Delivery, Verification, Operations, and Risk authorities as applicable;
- accepted decisions;
- delegated actions;
- unresolved questions;
- accepted deviations and risks;
- change and escalation history.

## 8. Independent State Axes

KGAID maintains three primary state axes for an increment.

### 8.1 Knowledge status

Knowledge status follows the accepted Knowledge Lifecycle:

~~~text
captured
→ proposed
→ reviewed
→ accepted
→ superseded or retired
~~~

It answers: **Is the increment definition authoritative?**

### 8.2 Delivery status

| Status | Meaning |
| --- | --- |
| **not-started** | No authorized realization is active. |
| **preparing** | Knowledge, contracts, tasks, or environment are being prepared. |
| **ready** | Realization-readiness conditions are satisfied. |
| **active** | Authorized realization work is in progress. |
| **integration-review** | Task results are being integrated and reviewed as one increment. |
| **implementation-complete** | Declared realization exists without unresolved scope-changing conflict. |
| **baselined** | Knowledge, implementation, evidence, limitations, and risk are bound coherently. |
| **released** | An authorized release applied to the baseline and target environment. |
| **closed** | Required follow-up is complete or transferred explicitly. |
| **paused** | Work is intentionally stopped while retaining current scope. |
| **cancelled** | Realization was stopped and will not complete under the current increment. |

It answers: **What has been realized operationally?**

### 8.3 Verification status

| Status | Meaning |
| --- | --- |
| **not-planned** | Verification has not yet been defined. |
| **planned** | Claims, methods, environments, and evidence needs are identified. |
| **in-progress** | Evidence collection or evaluation is active. |
| **partially-supported** | Some required evidence supports only part of the declared claim. |
| **failed** | Evidence contradicts at least one applicable criterion or claim. |
| **verified** | Proportionate evidence supports the declared completion claim. |
| **verified-with-limitations** | Human authority accepted an explicitly narrowed verification claim. |
| **inconclusive** | Available evidence cannot resolve the claim. |
| **invalidated** | Change in knowledge, implementation, environment, or method makes prior evidence unusable for the claim. |
| **expired** | Time or policy boundary requires reverification. |

It answers: **What exact claim does evidence support?**

These axes MUST NOT be collapsed.

An increment MAY have accepted knowledge, active delivery, and partially-supported verification. It MAY be implementation-complete but not verified. It MAY be verified in a test environment but not released. It MAY be released while the intended product outcome remains unproven.

## 9. Increment Lifecycle

The typical delivery flow is:

~~~mermaid
flowchart TD
    A["Candidate need"] --> B["Shape increment"]
    B --> C["Review and human acceptance"]
    C --> D["Realization readiness"]
    D --> E["Delegate and execute tasks"]
    E --> F["Integrate"]
    F --> G["Implementation Conformance Review"]
    G --> H["Verify increment claim"]
    H --> I["Baseline"]
    I --> J["Release or retain"]
    J --> K["Observe and learn"]
    K --> A
~~~

The flow MAY return upstream whenever a discovery changes product meaning, requirement, architecture, contract, risk, or evidence scope.

### 9.1 Candidate and shaping

A need is identified, related to an outcome or obligation, and shaped into a bounded proposal.

### 9.2 Review and acceptance

Applicable authorities evaluate purpose, business meaning, requirements, architecture, contracts, risk, compatibility, and verification feasibility. Human acceptance makes the Increment artifact normative for its declared scope.

### 9.3 Readiness

Tasks, dependencies, environments, verification, and authorities are prepared. Readiness applies only to the affected scope.

### 9.4 Execution

Humans and AI realize authorized tasks. Discoveries are routed back to the appropriate knowledge lifecycle.

### 9.5 Integration

Task results are combined into an implementation revision that is ready for
Implementation Conformance Review.

### 9.6 Implementation conformance review

The integrated result is compared with the accepted architecture and applicable
contracts. Its review outcome determines the rework route before claim
verification continues.

### 9.7 Verification

Evidence is aggregated and gaps are made explicit. Verification status reflects the exact supported claim.

### 9.8 Baseline and release

Accepted knowledge, implementation, evidence, limitations, and risk are bound. A separate human authority decides release where applicable.

### 9.9 Observation and learning

Operational evidence evaluates actual behavior and product outcomes. Material learning begins another governed knowledge cycle.

## 10. Increment Readiness

An increment is ready for realization when, proportionate to risk:

- purpose and intended outcome are accepted;
- scope, exclusions, and completion claim are explicit;
- required business rules and requirements are accepted;
- significant architecture decisions are accepted;
- material contracts and consumers are identified and accepted;
- assumptions, risks, and unresolved questions are visible;
- compatibility, migration, and operational effects are addressed;
- tasks and dependencies are defined sufficiently;
- AI Execution Task Contracts can be authorized;
- target baselines and environments are known;
- integration approach is feasible;
- verification plan can support the intended claim;
- required human authorities are identified;
- no unresolved conflict invalidates execution.

This specializes **PC-5 Realization Ready** and **KG-4 Realization Ready** for one Increment artifact.

Readiness MUST be assessed against semantic conditions, not percentage of documents completed.

A human Risk Authority MAY authorize reduced readiness when the missing knowledge, limited scope, compensating controls, reevaluation trigger, and accepted risk are recorded. AI cannot make that decision.

## 11. Task Decomposition

An accepted increment MAY be decomposed into:

- AI execution tasks;
- human decision or specialist-review tasks;
- knowledge refinement tasks;
- integration tasks;
- verification tasks;
- migration, rollout, and operational tasks.

Every material AI execution task SHOULD use the accepted [KGAID AI Execution Task Contract](23-ai-execution-task-contract.md).

A task MUST:

- identify the Increment it realizes;
- remain within the increment scope;
- inherit applicable accepted knowledge and constraints;
- have a bounded outcome;
- state dependencies and integration point;
- define task-level acceptance criteria and evidence;
- expose discoveries that affect increment knowledge;
- avoid creating a completion claim broader than its evidence.

The Increment artifact owns increment scope. A task contract cannot broaden it.

### 11.1 Task dependency graph

Task dependencies SHOULD be explicit when they affect order, shared state, contract versions, or integration.

~~~mermaid
flowchart TD
    A["Accepted increment"] --> B["Task A: contract representation"]
    A --> C["Task B: implementation"]
    B --> C
    C --> D["Task C: integration"]
    D --> E["Task D: increment verification"]
~~~

The graph is illustrative. Tasks MAY proceed concurrently when their inputs, write scopes, and contracts do not conflict.

### 11.2 Task completion

A task is complete only relative to its contract. Its completion means neither:

- that dependent tasks are complete;
- that integration succeeded;
- that increment-wide criteria passed;
- that the increment is verified;
- that a human accepted the increment;
- that the result is released.

## 12. Human–ChatGPT–Codex Coordination

In the reference collaboration pattern:

| Actor | Increment responsibility |
| --- | --- |
| **Human** | Establishes the outcome with ChatGPT, accepts increment scope, resolves consequential changes, accepts residual risk, and decides final result and release. |
| **ChatGPT** | Shapes the increment, preserves knowledge context, prepares task decomposition and Codex contracts, reviews task results, coordinates corrections, assesses aggregate evidence, and prepares human decisions. |
| **Codex** | Implements authorized task contracts, runs required checks, returns actual changes and evidence, and escalates discoveries. |

The control flow is:

1. Human and ChatGPT agree the increment outcome, scope, constraints, and completion claim.
2. ChatGPT verifies upstream readiness and proposes the Increment artifact.
3. Human authorities accept the Increment artifact.
4. ChatGPT decomposes the increment into bounded AI Execution Task Contracts.
5. Human authorizes consequential delegation.
6. Codex executes each authorized task and returns evidence.
7. ChatGPT reviews actual task results and coordinates corrections within accepted scope.
8. ChatGPT evaluates integration and increment-wide evidence.
9. New product, architecture, contract, security, compatibility, evidence, or risk decisions return to the Human.
10. ChatGPT presents a final decision packet.
11. Human accepts, limits, rejects, or requests revision of the increment result.

ChatGPT MUST NOT declare the increment accepted merely because every Codex task reports success.

## 13. Execution and Coordination

During active realization, the Delivery Authority or delegated Knowledge AI SHOULD maintain:

- current increment and task status;
- authoritative baseline and latest revisions;
- task dependencies;
- active write scopes;
- discovered knowledge and conflicts;
- integration state;
- evidence coverage;
- decisions and escalations;
- change to risk or compatibility;
- remaining work for the declared completion claim.

AI MAY reorder or refine tasks without human interruption when:

- increment intent and scope remain unchanged;
- accepted architecture and contracts remain unchanged;
- compatibility and evidence scope remain unchanged;
- no new external effect or residual risk is introduced;
- task dependencies and write ownership remain safe.

A changed delivery tactic is not necessarily an increment change. A changed observable outcome or accepted boundary is.

## 14. Integration

Integration evaluates the combined result, not only individual tasks.

Integration review SHOULD verify:

- all intended task results are present at identified revisions;
- combined behavior satisfies increment scope;
- architecture boundaries and ownership remain consistent;
- contract representations and implementations agree;
- dependencies and versions are compatible;
- migrations and coexistence behave as intended;
- security and privacy controls hold across boundaries;
- error, failure, and recovery behavior remain coherent;
- derived documentation and traceability are current;
- no task introduced unintended behavior outside scope;
- increment-level verification can run against the integrated result.

A set of individually passing tasks MAY fail integration.

Integration defects MAY return to task correction when the accepted increment remains valid. A defect that challenges increment knowledge returns to the relevant human authority.

## 15. Implementation Conformance Review

An **Implementation Conformance Review** is a bounded review of an integrated
Vertical Slice against its accepted architecture. It determines whether an
observed deviation is implementation-only or proves that accepted architecture
MUST be reworked. It is neither a lifecycle status, a verification status, nor
a project-level KGAID conformance determination.

### 15.1 Inputs and authority

The review MUST identify its subject scope and exact implementation revision.
It MUST inspect, as applicable:

- the accepted Architecture Baseline and applicable ADRs;
- the Domain Model, requirements, and material contracts that constrain the
  slice;
- architecture boundaries, responsibilities, dependencies, and quality
  strategies;
- the actual integrated implementation, diff, and traceability;
- relevant checks, evidence, limitations, and previous review findings.

A Knowledge and Review AI MAY prepare the comparison and recommendation. The
applicable Human Authority remains responsible for accepting a changed
architecture, contract, Baseline, Domain Model, ADR, risk, or formal closure
claim. A review MUST preserve its subject revision, findings, result, and
follow-up rather than mutating a previous review run into a later outcome.

### 15.2 Review outcomes

The full Implementation Conformance Review MUST conclude with exactly one of
the following outcomes:

| Outcome | Meaning and required next action |
| --- | --- |
| **Conformant** | The implementation conforms to accepted architecture. The Vertical Slice MAY be formally closed for its declared scope, subject to separate verification, baseline, release, and Human Authority conditions. |
| **Conformant with Observations** | Observations or minor deviations are recorded, owned, and do not invalidate architecture or block formal closure of the declared slice. |
| **Implementation Rework Required** | Accepted architecture remains correct. All required corrections are limited to implementation; they require no new ADR, change to Baseline, contract change, or Domain Model change. Rework returns to implementation and MUST be followed by a Quick Conformance Review. |
| **Architecture Rework Required** | The implementation demonstrates an error in accepted architecture: for example an incorrect Domain Model, Baseline, contract, module boundary, or ADR. The affected scope MUST return to Architecture; any affected contract and readiness work follows its normal lifecycle before implementation resumes. |

An observation MUST NOT be used to conceal a deviation that changes accepted
meaning or boundary. Conversely, an implementation defect MUST NOT be labeled
architecture rework merely because its correction is difficult. The review
record MUST state the authoritative source, observed divergence, affected
scope, rationale for the classification, and required follow-up.

### 15.3 Quick Conformance Review

A **Quick Conformance Review** is a limited follow-up review after
`Implementation Rework Required`. Its sole purpose is to confirm that the
specific deviations identified by the previous full review have been removed.

It MUST:

- reference the preceding review run and each deviation identifier;
- inspect the corrected implementation revision and the checks relevant to
  those deviations;
- preserve the accepted architecture and the original review scope; and
- avoid re-performing a full implementation review or treating unreviewed
  implementation as conformant.

It MUST NOT re-evaluate the whole implementation, replace the full review, or
silently extend the correction scope. A closed Quick Conformance Review ends
with one of these outcomes only:

| Outcome | Meaning and next action |
| --- | --- |
| **Conformant** | All named deviations are removed; the slice MAY proceed to formal closure for the declared scope. |
| **Conformant with Observations** | All named deviations are removed; recorded observations do not block formal closure. |
| **Architecture Rework Required** | The correction evidence shows that accepted architecture, a Baseline, contract, Domain Model, module boundary, or ADR is wrong; return to Architecture. |

If a named implementation deviation remains unresolved without challenging
architecture, the quick review remains open and returns the same bounded scope
to implementation rework. It does not create a new full-review outcome or
broaden the review.

### 15.4 Rework boundaries and Human Authority

`Implementation Rework Required` authorizes only a correction within already
accepted meaning and delegation. It MUST NOT authorize a new ADR, a Baseline
change, contract change, Domain Model change, or architectural boundary change.
Discovery of any such need converts the route to `Architecture Rework
Required`; the relevant Human Authority decides the resulting knowledge
changes. Neither AI nor the implementation itself MAY redefine architecture to
make a review pass.

## 16. Verification and Evidence Coverage

Increment verification compares the integrated result with the accepted increment claim and criteria.

Evidence coverage SHOULD be maintained per criterion:

| Criterion | Required boundary | Evidence | Status | Limitation |
| --- | --- | --- | --- | --- |
| AC-1 | Component | EVD reference | supported | none |
| AC-2 | Integration | EVD reference | failed | dependency version |
| AC-3 | Production-like environment | none | unsupported | environment unavailable |

The exact representation is project-specific.

The Knowledge and Review AI SHOULD:

- aggregate task evidence without broadening it;
- identify criteria with no supporting evidence;
- detect inconsistent environments or revisions;
- distinguish automated, manual, simulated, and operational evidence;
- identify evidence invalidated by later changes;
- prepare an exact verification claim and limitations.

The Verification Authority determines whether evidence supports the claim. The Human Risk or Baseline Authority accepts residual limitations where applicable.

## 17. Completion and Decision Semantics

KGAID distinguishes:

| Claim | Required condition |
| --- | --- |
| **Increment knowledge accepted** | Human authority accepted the Increment artifact and scope. |
| **Increment ready** | Readiness conditions in Section 10 are satisfied. |
| **Tasks complete** | Each declared task met its own contract or has an explicit disposition. |
| **Implementation complete** | The integrated realization exists without unresolved scope-changing conflict. |
| **Increment verified** | Evidence supports the accepted increment completion claim. |
| **Increment baselined** | Knowledge, implementation, evidence, limitations, and residual risk form a coherent reference. |
| **Increment accepted** | Human authority accepted the reviewed result for the declared scope. |
| **Increment released** | Human Release Authority applied the baseline to a target environment. |
| **Outcome achieved** | Operational evidence supports the related product success measure. |

These claims MUST NOT be used interchangeably.

An increment is not complete merely because:

- all tasks are marked done;
- the code was merged;
- the build passed;
- unit tests passed;
- ChatGPT reviewed Codex output;
- deployment succeeded;
- no defect has yet been reported.

The declared completion claim, scope, evidence, limitations, and human decision determine completion.

## 18. Scope Change and Discovery

A material discovery during realization MUST be classified.

| Discovery | Default handling |
| --- | --- |
| Local implementation defect within accepted knowledge | Correct through an existing task contract. |
| Implementation Conformance Review finds implementation-only deviation | Record `Implementation Rework Required`; correct the identified scope and perform a Quick Conformance Review. |
| Implementation Conformance Review challenges architecture | Record `Architecture Rework Required`; return to Architecture and revise affected knowledge through its lifecycle. |
| Missing task that remains within increment scope | Add and authorize a task. |
| Clarification without semantic change | Record clarification and update affected task context. |
| Requirement or business meaning change | Return to the owning knowledge artifact and Human Authority. |
| Significant architecture change | Create or supersede the applicable architecture decision. |
| Contract semantic or compatibility change | Revise the Contract through its knowledge lifecycle. |
| New security, compliance, or privacy concern | Suspend affected scope and escalate to specialist authority. |
| Broader evidence claim required | Revise verification plan and obtain proper authority. |
| New residual risk | Record and obtain Risk Authority decision. |
| Independent new outcome | Create another increment. |

A material semantic scope change SHOULD create a new increment revision and return it to review and human acceptance.

When the original and new outcomes can be accepted independently, a separate Increment artifact SHOULD be created rather than continually expanding the active increment.

History and evidence for the previous accepted revision MUST be preserved.

## 19. Dependencies and Concurrent Increments

Increment relationships MAY include:

- **depends_on** — one increment requires another result;
- **enables** — one increment makes another feasible;
- **blocks** — unresolved state prevents a declared claim;
- **shares_contract** — increments depend on the same contract version;
- **conflicts_with** — concurrent scope or decisions are incompatible;
- **supersedes** — a later increment replaces the earlier meaning or plan;
- **migrates_from** and **migrates_to** — controlled state transition;
- **verifies** — an increment primarily produces evidence for another concern.

Concurrent increments MUST coordinate:

- shared authoritative artifacts;
- contract versions;
- data and migration order;
- repository or component write ownership;
- environments;
- verification baselines;
- release sequencing;
- impact of upstream changes.

A change to shared knowledge triggers impact analysis for every dependent increment. Unrelated ready work MAY continue when the disputed scope remains isolated.

## 20. Baseline, Release, and Learning

A baselined increment SHOULD identify:

- accepted Increment revision;
- relevant upstream artifact revisions;
- implementation revision;
- contract versions;
- evidence set;
- verification claim;
- known limitations;
- unresolved and accepted risks;
- required operational conditions.

Release is a separate decision that SHOULD identify:

- baseline;
- target environment and rollout scope;
- migration and compatibility plan;
- operational readiness;
- rollback or containment;
- release authority;
- residual risk;
- required monitoring.

After release, outcome and operational evidence SHOULD be linked back to the Increment artifact.

Operational success does not retroactively prove that every design claim was correct. Operational failure does not automatically invalidate all accepted knowledge. Each observation is scoped and routed to the relevant owner.

## 21. Reference Increment Template

~~~markdown
# INC-NNN — Increment title

## Metadata

- Knowledge status:
- Delivery status:
- Verification status:
- Version:
- Owner:
- Increment type:
- KGAID profile:
- Product Authority:
- Delivery Authority:
- Verification Authority:
- Risk Authority:

## Intent

### Outcome, obligation, risk reduction, or learning goal

### Rationale and urgency

### Intended completion claim

### Affected stakeholders and capabilities

## Scope

### Included

### Excluded and non-goals

### Boundaries with other increments

### Compatibility and migration scope

## Upstream knowledge

| Artifact | Version | Relationship | Authority |
| --- | --- | --- | --- |

## Assumptions, unknowns, and risks

| Item | Owner | Impact | Validation or treatment |
| --- | --- | --- | --- |

## Architecture and contracts

| Artifact | Version | Meaning for this increment |
| --- | --- | --- |

## Acceptance criteria

| Criterion | Upstream source | Verification method | Evidence |
| --- | --- | --- | --- |

## Readiness

- [ ] Purpose and scope accepted
- [ ] Business meaning sufficient
- [ ] Requirements accepted
- [ ] Significant architecture accepted
- [ ] Material contracts accepted
- [ ] Assumptions and risks visible
- [ ] Compatibility and migration addressed
- [ ] Tasks and dependencies prepared
- [ ] Verification feasible
- [ ] Authorities identified
- [ ] No invalidating conflict

## Delivery tasks

| Task | Type | Contract | Dependencies | Owner or executor | Status |
| --- | --- | --- | --- | --- | --- |

## Integration plan

## Verification and evidence coverage

## Deployment, migration, rollback, and operations

## Discoveries and changes

## Implementation Conformance Review

- Review run identifier:
- Review type: Full / Quick
- Subject scope and implementation revision:
- Accepted Architecture Baseline and applicable ADRs:
- Applicable Domain Model, contracts, and requirements:
- Preceding full review and deviation identifiers (Quick only):
- Outcome (Full): Conformant / Conformant with Observations / Implementation Rework Required / Architecture Rework Required
- Outcome (Quick): Conformant / Conformant with Observations / Architecture Rework Required

### Findings and observations

| ID | Classification | Authoritative source | Observed divergence or observation | Affected scope | Required follow-up |
| --- | --- | --- | --- | --- | --- |

### Rework rationale

### Formal-closure recommendation

### Implementation result

### Evidence-supported claim

### Limitations

### Residual risk

### ChatGPT recommendation

## Human decision

- Decision:
- Decided by:
- Date:
- Accepted scope:
- Accepted limitations:
- Accepted risk:
- Baseline:
- Release decision:
- Follow-up:
~~~

A project MAY combine or shorten sections when the retained content is sufficient for its risk and conformance profile.

## 22. Minimal and Extended Application

### 22.1 Minimal application

A low-risk increment MAY be represented by one concise change record containing:

- intended outcome;
- scope and non-goals;
- authoritative requirement or assumption;
- architecture and contract boundary;
- acceptance criteria;
- tasks;
- checks and evidence;
- limitations;
- human authorization and final decision.

### 22.2 Extended application

A high-risk, regulated, production-critical, security-sensitive, distributed, or long-lived increment SHOULD include:

- independently accepted upstream artifacts;
- formal authority and separation of duties;
- controlled revision and baseline;
- detailed task and dependency graph;
- contract versioning and migration;
- security, privacy, and compliance review;
- independent verification;
- reproducible evidence retention;
- release and rollback controls;
- operational monitoring and learning;
- explicit residual-risk acceptance.

## 22. Failure Signals

The following indicate likely increment failure:

- the increment is named after an activity without a meaningful result;
- scope grows whenever a new task is discovered;
- tasks exist without accepted upstream knowledge;
- Codex task contracts do not identify their Increment artifact;
- task completion is reported as increment verification;
- implementation begins while significant architecture or contract meaning is unresolved;
- individual task tests pass but integrated behavior is not evaluated;
- evidence from different revisions or environments is combined without qualification;
- ChatGPT accepts aggregate success without inspecting unsupported criteria;
- the Human sees only task status rather than outcome, evidence, limitations, and risk;
- a release is inferred from merge or deployment;
- operational feedback is not linked to the increment and upstream knowledge;
- cancelled or superseded work loses its history.

## 23. Conformance

A project conforms to this model when, for a declared KGAID version and profile:

- each material increment has a stable identity, owner, outcome, scope, and completion claim;
- the increment derives from accepted product and business knowledge;
- significant architecture and material contracts constrain realization;
- readiness is evaluated before implementation commitment;
- tasks remain bounded by accepted increment scope;
- material AI execution uses authorized task contracts;
- task, integration, verification, baseline, release, and outcome states remain distinct;
- task results are integrated and reviewed as one increment;
- evidence coverage is evaluated against increment-wide criteria;
- material discoveries return to the correct knowledge and human authority;
- semantic scope change preserves history and requires acceptance;
- concurrent increments coordinate shared knowledge and contracts;
- baselines bind exact knowledge, implementation, evidence, limitations, and risk;
- final increment acceptance and release remain human decisions;
- operational learning returns to the knowledge process.

Conformance does not require Scrum, Kanban, iterations of a fixed duration, story points, a specific backlog tool, programming language, repository platform, or AI product.
