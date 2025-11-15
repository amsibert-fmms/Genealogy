# GeneaX Master Outline  
Canonical conceptual structure for all GeneaX documentation.  
This outline defines the chapters and tiers that organize the genealogical domain, the data model, and the implementation.

For a list of all documentation files, see:  
👉 `Docs/index.md`

---

# 0. Purpose  
This document provides the structured “map” of the GeneaX knowledge system.  
All supplemental documents should anchor their sections to the chapters and tiers defined here.

Each chapter presents one core genealogical domain area.  
Each chapter is divided into three layers:

- **Tier 1 — Conceptual Model**  
- **Tier 2 — Logical Model**  
- **Tier 3 — Implementation Model**

This top-down structure supports incremental development: build Tier 1 first, then Tier 2, then Tier 3.

---

# Chapter 1 — Person  {#chapter-1-person}
The Person is the foundational entity of genealogical systems.

### Tier 1 — Conceptual  
Definition of a Person as an individual human subject.  
Includes identity attributes, alternative names, and participation in events and relationships.

### Tier 2 — Logical  
See: `Core_Docs/DATA_MODELS.md#person-model`  
Defines identifiers, names, gender, facts, events, relationships, and citations.

### Tier 3 — Implementation  
Person ORM model and current field set.  
Document any gaps relative to Tier 2.

---

# Chapter 2 — Event  {#chapter-2-event}
Events describe occurrences involving one or more people.

### Tier 1 — Conceptual  
Definition of events such as birth, marriage, migration, death, etc.

### Tier 2 — Logical  
See: `Core_Docs/DATA_MODELS.md#event-model`  
Fully defined event types, dates, places, and participant roles.

### Tier 3 — Implementation  
Event ORM model and implementation notes.

---

# Chapter 3 — Relationship  {#chapter-3-relationship}
Relationships define structured links between people.

### Tier 1 — Conceptual  
Relationships such as parent–child, spouse, guardian, sibling.

### Tier 2 — Logical  
See: `Core_Docs/DATA_MODELS.md#relationship-model`  
Relationship type, direction, participants, and temporal attributes.

### Tier 3 — Implementation  
Implementation of Relationship ORM model and missing features.

---

# Chapter 4 — Sources & Citations  {#chapter-4-sources}
Evidence-based genealogy depends on sources and their citations.

### Tier 1 — Conceptual  
Definition of sources, citations, and facts/claims.

### Tier 2 — Logical  
See:  
- `Core_Docs/DATA_MODELS.md#source-model`  
- `Core_Docs/DATA_MODELS.md#citation-model`  
- `Core_Docs/DATA_MODELS.md#fact-model`

Logical structure for source descriptions, citation targeting, and fact representation.

### Tier 3 — Implementation  
ORM models for sources, citations, and facts (once implemented).

---

# Chapter 5 — Claims, Conclusions, and Proof  {#chapter-5-proof}
This chapter describes the reasoning layer above raw data and evidence.

### Tier 1 — Conceptual  
Claims, conclusions, and proof statements in genealogical reasoning.

### Tier 2 — Logical  
See:  
- `Core_Docs/DATA_MODELS.md#proof-model`  
- Conclusion model section (pending)  
Mapping of reasoning entities and relationships.

### Tier 3 — Implementation  
Current ProofStatement/Conclusion ORM structures.

---

# Chapter 6 — Numbering, Cross-References, and Appearances  {#chapter-6-references}
Publication-oriented structures used for rendering genealogies in books or numbered systems.

### Tier 1 — Conceptual  
Numbering schemes, appearance tracking, and cross-reference systems.

### Tier 2 — Logical  
See:  
- `Core_Docs/DATA_MODELS.md#xref-model`  
- `Core_Docs/DATA_MODELS.md#familyappearance-model`  
- `Core_Docs/DATA_MODELS.md#generatedconclusion-model`

### Tier 3 — Implementation  
ORM implementations for publication and appearance models.

---

# Cross-Document Map  

### Architecture  
`Core_Docs/ARCHITECTURE.md`  
Aligns with Tier 2 and Tier 3 structure.

### Validation Rules  
`Core_Docs/VALIDATION_RULES.md`  
Defines constraints applied to Tier 2 models.

### GEDCOM-X Mapping  
`Core_Docs/GEDCOMX_COMPLIANCE.md`  
Logical mapping to external standard.

### Features  
`Core_Docs/FEATURES.md`

### Developer Documentation  
Installation, Configuration, Deployment, Testing  
Located in `Docs/Developer_Docs/`

---

# Growth Guidelines  
- Add new chapters when introducing new conceptual domains.  
- Expand tiers in order: Tier 1 → Tier 2 → Tier 3.  
- Add anchor headers to supplemental documents so they tie back to chapters.  
- Update this outline when new entities or domain areas are added.

