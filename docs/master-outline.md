# GeneaX Master Outline {#master-outline}
_Last updated: 2025-11-15_

Related references: [Documentation home](index.md#geneax-docs-home) · [Data models](core/data-models.md#geneax-data-models) · [Architecture](core/architecture.md#geneax-architecture)

This outline is the canonical map of the GeneaX documentation set. It defines the chapters and tiers that structure our
genealogical domain knowledge, our logical models, and their implementation in code. Every supplemental document should link back
here so contributors can quickly trace concepts across the stack.

## How to navigate
- Start with the [documentation home](index.md#geneax-docs-home) for a directory of every guide.
- Jump to detailed entities in the [data models](core/data-models.md).
- Align engineering work with the [roadmap](core/roadmap.md) and [features](core/features.md).

Each chapter below provides:
1. **Tier 1 — Conceptual model**: the language of genealogy.
2. **Tier 2 — Logical model**: structured representations described in [core/data-models.md](core/data-models.md#geneax-data-models).
3. **Tier 3 — Implementation model**: Django components and open gaps.

---

## Chapter 1 — Person {#chapter-1-person}
The Person is the foundational entity of genealogical systems.

### Tier 1 — Conceptual
Defines identity, alternative names, demographics, and participation in events and relationships.

### Tier 2 — Logical
See [Person model](core/data-models.md#person-model). Covers identifiers, names, gender, facts, events, relationships, and
citations.

### Tier 3 — Implementation
Django ORM model plus serializers housed in `genealogy/apps/persons/`. Document any gaps relative to Tier 2 in
[validation rules](core/validation-rules.md).

---

## Chapter 2 — Event {#chapter-2-event}
Events describe occurrences involving one or more people.

### Tier 1 — Conceptual
Defines events such as birth, marriage, migration, and death.

### Tier 2 — Logical
See [Event model](core/data-models.md#event-model) for event types, dates, places, and participant roles.

### Tier 3 — Implementation
Event ORM model and supporting workflows in `genealogy/apps/events/`. Capture implementation notes in the
[architecture](core/architecture.md) guide.

---

## Chapter 3 — Relationship {#chapter-3-relationship}
Relationships define structured links between people.

### Tier 1 — Conceptual
Covers relationships such as parent–child, spouses, guardians, and siblings.

### Tier 2 — Logical
See [Relationship model](core/data-models.md#relationship-model) for relationship type, direction, participants, and temporal
attributes.

### Tier 3 — Implementation
Relationship ORM model and open gaps within `genealogy/apps/relationships/`.

---

## Chapter 4 — Sources & Citations {#chapter-4-sources}
Evidence-based genealogy depends on sources and their citations.

### Tier 1 — Conceptual
Defines sources, citations, and fact statements.

### Tier 2 — Logical
See the [Source](core/data-models.md#source-model), [Citation](core/data-models.md#citation-model), and
[Fact](core/data-models.md#fact-model) entries.

### Tier 3 — Implementation
ORM models for sources, citations, and facts (pending). Track outstanding work in the
[roadmap](core/roadmap.md).

---

## Chapter 5 — Claims, Conclusions, and Proof {#chapter-5-proof}
This chapter describes the reasoning layer above raw data and evidence.

### Tier 1 — Conceptual
Explains claims, conclusions, and proof statements used in genealogical reasoning.

### Tier 2 — Logical
See [Proof model](core/data-models.md#proof-model) and related conclusion sections (in progress).

### Tier 3 — Implementation
Current proof-statement and conclusion structures within `genealogy/apps/reasoning/`. Evaluation rules reside in the
[proof standard](core/proof-standard.md).

---

## Chapter 6 — Numbering, Cross-References, and Appearances {#chapter-6-references}
Publication-oriented structures used for rendering genealogies in books or numbered systems.

### Tier 1 — Conceptual
Describes numbering schemes, appearance tracking, and cross-reference systems.

### Tier 2 — Logical
See [Cross-reference](core/data-models.md#xref-model), [Family appearance](core/data-models.md#familyappearance-model), and
[Generated conclusion](core/data-models.md#generatedconclusion-model) entries.

### Tier 3 — Implementation
ORM implementations for publication and appearance models (planned) in `genealogy/apps/publications/`.

---

## Cross-document map {#cross-document-map}
| Topic | Location | Purpose |
| --- | --- | --- |
| Architecture | [core/architecture.md](core/architecture.md) | Maps chapters to Django modules. |
| Validation rules | [core/validation-rules.md](core/validation-rules.md) | Constraints applied to Tier 2 models. |
| GEDCOM X mapping | [core/gedcomx-compliance.md](core/gedcomx-compliance.md) | External standard alignment. |
| Features | [core/features.md](core/features.md) | Delivery checklist connected to this outline. |
| Developer docs | [developer/README.md](developer/README.md) | Installation, configuration, deployment, testing. |

---

## Growth guidelines
- Add new chapters when introducing new conceptual domains.
- Expand tiers in order: Tier 1 → Tier 2 → Tier 3.
- Add anchor headers to supplemental documents referencing chapter IDs.
- Update this outline whenever new entities or domain areas are added.
