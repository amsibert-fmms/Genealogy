🧩 GeneaX Master Outline

Canonical structure and cross-reference map for all project documentation.

0. Purpose of This Document

This outline defines the three schema tiers used throughout GeneaX.
All other documents should reference these definitions when describing models, features, APIs, or architecture.

Whenever a supplemental file expands on one of these sections, it should include a matching header with the marker:

> Linked from MASTER_OUTLINE → [Tier / Section]


This creates a bidirectional documentation graph.

1. Tier Definitions

These terms have fixed meaning and should not be redefined elsewhere.

1.1 Tier 1 — Conceptual Model

The abstract representation of genealogical entities and relationships.
Technology-independent. Includes persons, events, sources, assertions, citations, and proofs.

1.2 Tier 2 — Logical Model

The full, idealized database structure.
Defines entities, relationships, constraints, and GEDCOM-X mappings.
Represents the target schema GeneaX aims to achieve.

1.3 Tier 3 — Implementation Model

The currently implemented Django ORM layer.
May be incomplete relative to Tier 2 but should always clearly reference it.

2. Tier 1 — Conceptual Model

(See more detail in: Core_Docs/DATA_MODELS.md#tier-1-conceptual-model)

2.1 Core Entities

Person

Event

Relationship

Source

Citation

Claim (Assertion)

Conclusion

ProofStatement

2.2 Core Relationships

Persons participate in Events

Events are supported by Sources

Citations support Claims

Claims lead to Conclusions

ProofStatements explain Conclusions

3. Tier 2 — Logical Model

(See: Core_Docs/DATA_MODELS.md#tier-2-logical-model)

3.1 Entities (Idealized Schema)

Each entity below should have a corresponding section in DATA_MODELS.md.

Person — DATA_MODELS.md#person-model

Event — DATA_MODELS.md#event-model

Relationship — DATA_MODELS.md#relationship-model

SourceDescription — DATA_MODELS.md#source-model

Citation — DATA_MODELS.md#citation-model

Fact — DATA_MODELS.md#fact-model

ProofStatement — DATA_MODELS.md#proof-model

CrossReference — DATA_MODELS.md#xref-model

FamilyAppearance — DATA_MODELS.md#familyappearance-model

GeneratedConclusion — DATA_MODELS.md#generatedconclusion-model

3.2 Constraints & Rules

(See: Core_Docs/VALIDATION_RULES.md)

Examples:

A Person may have multiple Events.

A Relationship must reference two Persons.

A Citation must support a Fact or Claim.

ProofStatements must reference specific Conclusions.

3.3 GEDCOM-X Mapping

(See: Core_Docs/GEDCOMX_COMPLIANCE.md)

This section defines how Tier 2 maps to GEDCOM-X entities.

4. Tier 3 — Implementation Model

(See: Core_Docs/DATA_MODELS.md#tier-3-implementation-model)

4.1 Current Django Models

List each real Django model and link it back to its Tier 2 counterpart.

4.2 Gaps vs. Tier 2

This is where “future work” lives—but it’s tied directly to the logical model.

5. Cross-Document Map

These sections list where in the documentation ecosystem each part of the outline is expanded.

5.1 Architecture

Core_Docs/ARCHITECTURE.md
Corresponds to Tier 2 overall structure and Tier 3 implementation layers.

5.2 Features

Core_Docs/FEATURES.md
Maps feature descriptions back to conceptual entities.

5.3 API

Core_Docs/API_REFERENCE.md
Should reference Tier 3 models and Tier 2 relationships.

5.4 Proof / Evidence

Core_Docs/PROOF_STANDARD.md
Connects deeply to Tier 1 reasoning and Tier 2 logic.

5.5 Developer Docs

(installation, testing, configuration, etc.)
These belong primarily to Tier 3 but should reference Tier 2 whenever discussing models.

6. Growth Notes

As GeneaX evolves:

Add new anchor headers to supplemental docs.

Add cross-references only here (the master file stays the root).

Avoid duplicating explanations; use links instead.

Keep the tier definitions stable so the ecosystem remains coherent.
