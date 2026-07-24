---
document_id: KGAID-MTH-006
title: KGAID Repository Resource Architecture Standard

document_type: architecture
status: proposed
version: 0.1.0

owner: Architecture

approval_status: draft
approved_by:
approved_at:
---

# KGAID Repository Resource Architecture Standard

## 1. Purpose and status

This standard defines a repository resource architecture for a KGAID-adopting
project. It separates production realization, tests, documentation, reference
data, supporting tools, and local runtime artifacts so that each resource has a
clear purpose, owner, lifecycle, and validation boundary.

This document is **proposed**. Its normative wording describes the standard
that an adopting project MAY select; it is not a normative member of the
prepared KGAID 0.1.0 baseline. Its acceptance and inclusion in a future
baseline require a separate Human Authority decision.

The pattern was generalized from an accepted resource architecture in a KGAID
adopting repository. That implementation is empirical input, not a normative
authority for this standard.

## 2. Normative conventions and scope

The keywords **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY**
have the meaning defined in the [KGAID Principles][principles].

This standard applies to a repository that chooses this structure. It is
independent of programming language, build system, framework, deployment
model, business domain, and business-module naming. It defines responsibility
classes, not a required source-tree depth or product decomposition.

An owner in this document is the accountable logical owner of a resource
class. The project governance resolves that logical owner to a team, role, or
individual. Resource ownership does not replace the semantic ownership of
knowledge artifacts defined by the [Knowledge Architecture][knowledge-architecture].

Every versioned resource MUST have one primary class and one accountable owner.
An index, generated view, translation, or copy MAY refer to an owning resource,
but MUST NOT create a competing owner.

## 3. Architectural rules

### RRA-1 — One authoritative documentation tree

Project documentation MUST have one authoritative tree: `docs/`. A
repository-root entry point MAY link to that tree, but MUST NOT become a
parallel location for maintained technical, architectural, research, legal, or
operational documentation. Documentation owned by a tool, test, or dataset
belongs in `docs/` as well.

### RRA-2 — One primary owner per resource

Each resource MUST have one primary owner. A resource MAY support several
consumers, but consumer access does not transfer ownership. If a file appears
to require two owners, the project MUST split the resource, select one owner,
or define an explicit boundary.

### RRA-3 — Production is repository-layout independent

Production code MUST NOT require `docs/`, `tests/`, `datasets/`, `tools/`,
`.local/`, a parent checkout, or an assumed working directory to start or
perform its supported runtime behavior. Runtime configuration MAY name an
external data location when that location is an explicit deployment input; it
MUST NOT infer one from the repository layout.

### RRA-4 — Runtime artifacts are local, not versioned

Snapshots, logs, reports, traces, exports, caches, generated runtime state,
and environment-specific credentials MUST NOT be versioned as repository
resources. They belong under `.local/` or in an external approved retention
system and MUST be ignored by version control.

### RRA-5 — Reference data and test data remain distinct

Versioned, sanitized reference data MUST be stored in `datasets/`, separately
from explanatory documentation. Deterministic data created to exercise a test
belongs to the test suite, normally under `tests/fixtures/`; it remains owned
by tests even when it resembles a reference dataset. Production code MUST NOT
silently treat either class as a runtime dependency.

## 4. Resource classes

The following classes are the canonical locations at repository root. A
project MAY omit a class that it does not need. It MUST NOT use an alternative
location for a present class without recording an explicit mapping and
preserving the rules of this standard.

| Class | Purpose | Accountable owner | Permitted file types | MUST NOT contain |
| --- | --- | --- | --- | --- |
| `src/` | Production code and files packaged or deployed with the product. | Production-code owner | Language source, package metadata local to the source tree, runtime schemas, and static assets required by the supported runtime. | Test-only code, research scripts, documentation, local artifacts, secrets, and data that requires the checkout layout. |
| `tests/` | Repeatable verification of product behavior and quality, including test-owned fixtures. | Test owner | Test source, test configuration, deterministic fixtures, mocks, stubs, golden files, and test-specific helper code. | Authoritative production implementation, runtime output, undocumented personal samples, and reusable reference datasets owned elsewhere. |
| `docs/` | The single authoritative documentation tree for all maintained project knowledge. | Documentation or knowledge owner | Markdown or other approved documentation source, diagrams, document-local assets, generated documentation source, and documentation configuration. | Runtime outputs, raw sensitive evidence, production source code, test-only fixtures, and machine-readable reference data whose primary purpose is data rather than explanation. |
| `datasets/` | Versioned, sanitized, machine-readable reference data used for review, reproducibility, or controlled analysis. | Reference-data steward | JSON, CSV, XML, YAML, Parquet, checksums, manifests, and other approved machine-readable data formats. | Narrative documentation, secrets, unsanitized production extracts, transient runtime output, and test fixtures whose primary owner is a test. |
| `tools/` | Supporting tooling that is not part of the product runtime, such as analyzers, generators, migration helpers, and read-only query templates. | Tool owner | Tool source, tool-local build configuration, scripts, query templates, and tool tests where the project chooses to keep them with the tool. | Production runtime code, authoritative project documentation, runtime reports, credentials, and a dependency on a sibling checkout. |
| `.local/` | Ignored local working area for runtime and research artifacts that are not repository assets. | Local operator | Logs, snapshots, traces, reports, exports, caches, temporary files, local configuration, and local credentials. | Versioned source, accepted documentation, durable reference data, test fixtures required by CI, and any artifact that another checkout must obtain from version control. |

`src/`, `tests/`, and `tools/` MAY contain language-specific subdirectories.
The standard intentionally does not prescribe their names. Documentation may
refer to a dataset by stable identifier or path, and tests MAY read a controlled
reference dataset when that dependency is explicit; neither relationship
changes the owner's class.

## 5. Recommended repository structure

```text
repository/
├── src/
│   └── <production-package-or-module>/
├── tests/
│   ├── fixtures/
│   └── <test-suites>/
├── docs/
│   ├── architecture/
│   ├── operations/
│   └── <project-knowledge>/
├── datasets/
│   └── <reference-data-set>/
├── tools/
│   └── <supporting-tool>/
├── .local/                 # ignored; normally absent from version control
├── README.md                # navigation entry point, not a second docs tree
├── <build-and-repository-control-files>
└── <license-and-contribution-files>
```

Repository-root control files, build descriptors, license files, and a concise
navigation entry point are outside the six resource classes. They SHOULD remain
small and MUST NOT become catch-all storage for a class that has a canonical
location above.

## 6. Migration rules for existing repositories

Migration MUST preserve behavior and history unless the authorized change
explicitly includes a behavior change. The project SHOULD perform the work in
the following order:

1. Inventory the existing files, generated artifacts, consumers, and current
   version-control rules before moving content.
2. Classify every material resource by its primary purpose and accountable
   owner; identify mixed directories, duplicated documentation, and runtime
   dependencies on repository-relative paths.
3. Establish the target classes and `.gitignore` rules before relocating
   sensitive or generated output.
4. Move maintained documentation into `docs/`; replace duplicate copies with
   links or a short navigation entry point.
5. Move versioned, sanitized reference data into `datasets/`; move
   test-owned samples into `tests/fixtures/`; document any explicit test use of
   shared reference data.
6. Move supporting scripts and query templates into `tools/`; keep production
   runtime implementation in `src/`.
7. Move non-versioned runtime artifacts into `.local/` or an approved external
   store, remove them from the index when authorized, and prevent their return
   with ignore rules.
8. Replace repository-relative runtime discovery with packaged resources,
   explicit configuration, or an external deployment input.
9. Update links, build configuration, packaging rules, test paths, and
   documentation indexes; then run the project's relevant validation.

Migration MAY proceed incrementally. During an incremental migration, each
temporary exception MUST have an owner, a stated reason, and a removal
condition. A compatibility shim MUST NOT become an undocumented permanent
second location.

## 7. Anti-patterns

The following patterns violate this standard or require an explicit,
time-bounded migration exception:

- Documentation maintained beside source code, tests, or tools instead of in
  `docs/`.
- JSON, CSV, XML, or similar reference data stored under `docs/` because it is
  described by a nearby narrative.
- Generated reports, snapshots, traces, exports, or logs committed with source
  files instead of retained locally or externally.
- Production code that resolves `../docs`, `../datasets`, a sibling checkout,
  or its current working directory as part of normal supported behavior.
- A directory that mixes production source, tests, reference data, documents,
  and local output without a single primary purpose.
- A reference sample copied into `tests/` without declaring whether it is a
  test fixture or a shared dataset, leaving ownership ambiguous.
- A tool that is silently imported or deployed as production runtime code,
  despite being maintained as a repository helper.
- A root README that duplicates maintained documentation and diverges from the
  authoritative `docs/` content.

## 8. Architectural effect and conformance

Applying this standard improves:

- **readability**, because a reader can infer a resource's purpose and owner
  from its location;
- **automatic validation**, because tools can check ownership boundaries,
  forbidden files, ignored local artifacts, and documented exceptions;
- **runtime independence**, because deployed code does not depend on the
  repository checkout or research material;
- **maintainability**, because documentation, tests, data, tools, and runtime
  artifacts evolve through separate and visible lifecycles; and
- **scalability**, because teams can add modules and supporting resources
  without turning the repository root into a mixed-responsibility workspace.

A project conforms to this standard for a declared repository scope when it
can show that present resource classes have the stated purpose and owner,
documentation has one authoritative tree, runtime is independent of the
repository layout, local artifacts are not versioned, reference data is
separate from documentation, and test data remains owned by tests. A project
MAY tailor names and depths, but MUST record a mapping that preserves these
boundaries.

## 9. Relationship to KGAID

This standard realizes the [Single Knowledge Ownership][single-ownership]
invariant without reducing artifact identity to a path. It provides a storage
and execution boundary for the semantic domains defined by the [Knowledge
Domains Model][knowledge-domains], and supports the Process Model's requirement
that implementation, evidence, and learning remain distinguishable. It does
not define product modules, replace architecture decisions, or make a
directory structure the owner of business meaning.

[principles]: ../00-foundations/02-principles.md#2-normative-language
[knowledge-architecture]: ../10-knowledge-architecture/11-knowledge-architecture.md
[single-ownership]: ../10-knowledge-architecture/11-knowledge-architecture.md#7-knowledge-architecture-invariants
[knowledge-domains]: ../10-knowledge-architecture/16-knowledge-domains.md
