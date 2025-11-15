# GeneaX Data Models  
Structured by chapters that correspond to core genealogical domains.  
Each chapter contains Tier 1 (conceptual), Tier 2 (logical), and Tier 3 (implementation) descriptions.

---

# Chapter 1 — Person  {#chapter-1-person}
> Linked from MASTER_OUTLINE → Chapter 1

## Tier 1 — Conceptual Model
A Person represents an individual human subject.  
Conceptually includes multiple names, biological attributes, and participation in events and relationships.

## Tier 2 — Logical Model  {#person-model}
Logical attributes include:
- Identifiers  
- Names (primary and alternate)  
- Birth/death facts  
- Gender identity  
- Collections of events, relationships, citations, and facts  

GEDCOM-X mapping: `GEDCOMX_COMPLIANCE.md#person`

## Tier 3 — Implementation Model
See Django ORM implementation in `genealogy/models/person.py` (if present).  
Document gaps relative to Tier 2 in this section.

---

# Chapter 2 — Event  {#chapter-2-event}
> Linked from MASTER_OUTLINE → Chapter 2

## Tier 1 — Conceptual Model
An Event is a discrete occurrence associated with one or more Persons.

## Tier 2 — Logical Model  {#event-model}
Logical components:
- Event type  
- Date(s)  
- Place  
- Roles of participating persons  

GEDCOM-X mapping: `GEDCOMX_COMPLIANCE.md#event`

## Tier 3 — Implementation Model
List fields and relationships currently implemented.  
Document missing components for future expansion.

---

# Chapter 3 — Relationship  {#chapter-3-relationship}
> Linked from MASTER_OUTLINE → Chapter 3

## Tier 1 — Conceptual Model
A Relationship is a structured connection between two Persons (e.g. parent–child, spouse).

## Tier 2 — Logical Model  {#relationship-model}
Defines:
- Type  
- Person A  
- Person B  
- Optional temporal bounds  
- Supporting citations  

## Tier 3 — Implementation Model
Document the current Django Relationship model.

---

# Chapter 4 — Sources & Citations  {#chapter-4-sources}
> Linked from MASTER_OUTLINE → Chapter 4

## Tier 1 — Conceptual Model
- **Source**: An information-bearing artifact (record, book, certificate).  
- **Citation**: A reference linking a fact or claim to a source.  
- **Fact/Claim**: A proposed piece of genealogical information.

## Tier 2 — Logical Model
### Source Model  {#source-model}
Attributes and identifiers.

### Citation Model  {#citation-model}
Links claims/facts to sources.

### Fact Model  {#fact-model}
Represents a specific genealogical assertion.

## Tier 3 — Implementation Model
Document existing Source and Citation ORM structures.

---

# Chapter 5 — Claims, Conclusions, Proof  {#chapter-5-proof}
> Linked from MASTER_OUTLINE → Chapter 5

## Tier 1 — Conceptual Model
The genealogical reasoning system:
- Claims (assertions)
- Conclusions (evaluated determinations)
- ProofStatements (justifications)

## Tier 2 — Logical Model
### ProofStatement Model  {#proof-model}
Narrative synthesis of evidence.

### Conclusion Model
Represents final determinations about persons, events, or relationships.

## Tier 3 — Implementation Model
State current implementation and gaps.

---

# Chapter 6 — Numbering, Cross-References, Appearances  {#chapter-6-references}
> Linked from MASTER_OUTLINE → Chapter 6

## Tier 1 — Conceptual Model
Models for interacting with external genealogical publications:
- Numbering systems  
- Family group appearances  
- Person references  

## Tier 2 — Logical Model
### CrossReference Model  {#xref-model}
Handles numbering schemes.

### FamilyAppearance Model  {#familyappearance-model}
Represents a person or family within a structured publication.

### GeneratedConclusion Model  {#generatedconclusion-model}
Future automation outputs.

## Tier 3 — Implementation Model
Document current ORM implementations.

---

# Implementation Status Overview

| Model               | Status        | Notes |
|--------------------|---------------|-------|
| Person             | Documented    | Schema planned; partial implementation. |
| Event              | Documented    | Aligned with GEDCOM-X core. |
| Relationship       | Documented    | Validation pending. |
| SourceDescription  | Documented    | Supports publications and identifiers. |
| Citation           | Documented    | Connects sources to claims. |
| ProofStatement     | Documented    | Logical structure complete. |
| CrossReference     | Documented    | Supports numbering systems. |
| FamilyAppearance   | Documented    | Publication-contextual placement. |
| GeneratedConclusion| Documented    | Reserved for future inference. |

