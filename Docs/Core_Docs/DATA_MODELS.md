# GeneaX Data Models
This document defines the conceptual, logical, and implementation models for all genealogical entities.  
It is organized according to the chapter structure defined in `MASTER_OUTLINE.md`.

Each chapter follows the pattern:

- Tier 1 — Conceptual Model  
- Tier 2 — Logical Model  
- Tier 3 — Implementation Model (Django ORM)

---

# Chapter 1 — Person  {#chapter-1-person}

## Tier 1 — Conceptual Model
A Person represents an individual human being.  
Conceptually, a person may have:

- Multiple names  
- Gender identity  
- Biographical facts  
- Participation in events  
- Relationships to other persons  
- Associated claims, citations, and conclusions  

Persons are the foundation of genealogical data.

---

## Tier 2 — Logical Model  {#person-model}

### Attributes
- Identifiers  
- Primary and alternate names  
- Birth and death facts  
- Gender  
- Unique ID for exports  
- Event participation list  
- Relationship roles  

### Relationships
- Many events through EventRole  
- Many relationships  
- Many citations  
- Many claims and conclusions  

### GEDCOM X Mapping
Mapped to GEDCOM X `Person`.

---

## Tier 3 — Implementation Model

### Location in Repository
genealogy/apps/persons/models/person.py


### Implementation Requirements
- Must include all Tier 2 fields  
- Must conform to validation rules for persons (name presence, date formats, etc.)  
- Must use ISO 8601–compatible date fields  
- Related names must use consistent `related_name` conventions  

### Documentation Requirements
- List all implemented Django fields  
- Identify any Tier 2 fields not yet implemented  
- Note unique constraints and validation logic  

---

# Chapter 2 — Event  {#chapter-2-event}

## Tier 1 — Conceptual Model
An Event represents an occurrence involving one or more persons.  
Examples: birth, marriage, migration, death, residence.

Events carry:

- Type  
- Date or date range  
- Place  
- Participating persons and their roles  

---

## Tier 2 — Logical Model  {#event-model}

### Attributes
- type  
- date / date_range  
- place  
- identifiers  
- description (optional)

### Relationships
- One-to-many EventRole for participants

### GEDCOM X Mapping
Mapped to `Event` and `EventRole`.

---

## Tier 3 — Implementation Model

### Location in Repository
genealogy/apps/events/models/event.py


### Implementation Requirements
- Event types should use enumerations  
- Date and place fields must align with GEDCOM X rules  
- Participant roles must enforce allowed combinations  

### Documentation Requirements
- List implemented fields  
- Identify missing roles or validations  

---

# Chapter 3 — Relationship  {#chapter-3-relationship}

## Tier 1 — Conceptual Model
A Relationship defines a structured connection between two persons:  
parent–child, spouse, partner, guardian, adoptive relationships, etc.

---

## Tier 2 — Logical Model  {#relationship-model}

### Attributes
- type  
- person_a  
- person_b  
- start_date / end_date (optional)  
- notes  

### GEDCOM X Mapping
Mapped to `Relationship`.

---

## Tier 3 — Implementation Model

### Location in Repository
genealogy/apps/relationships/models/relationship.py


### Implementation Requirements
- Enforce valid relationship types  
- Prevent logically impossible relationships  
- Optional temporal boundaries  

### Documentation Requirements
- List implemented types  
- Document implementation gaps  

---

# Chapter 4 — Sources, Citations, and Facts  {#chapter-4-sources}

## Tier 1 — Conceptual Model

### Source
An information-bearing artifact (record, certificate, book, census page).  

### Citation
A reference linking a Fact or Claim to a Source.  

### Fact (Claim)
An asserted piece of genealogical information.

---

## Tier 2 — Logical Model

### SourceDescription  {#source-model}
- title  
- publication_info  
- identifiers  
- extraction notes  

### Citation  {#citation-model}
- source_id  
- target_type (Person/Event/Relationship/Fact/Conclusion)  
- target_id  
- detail / page / locator  

### Fact (Claim)  {#fact-model}
- statement  
- subject  
- citations[]  
- confidence_level  
- conflict_links[]  

---

## Citation Target Rules (New Clarification)

### Allowed targets
A Citation may point **only** to:

- Person  
- Event  
- Relationship  
- Fact (Claim)  
- Conclusion  

### Prohibited targets
- Citations may **not** reference other citations.  
- Citations may not reference ProofStatements.

### Cardinality
- Claims must have ≥ 1 Citation.  
- Persons/Events/Relationships may have 0–N Citations.  
- Conclusions cite ProofStatements, not raw sources.

---

## Tier 3 — Implementation Model

### Location in Repository
genealogy/apps/sources/models/


### Implementation Requirements
- Foreign keys must preserve target rules through validators  
- Citation must enforce valid target types  
- Sources must support GEDCOM X-compatible metadata fields  

### Documentation Requirements
- List implemented fields  
- Identify extensions beyond GEDCOM X  

---

# Chapter 5 — Claims, Conclusions, Proof  {#chapter-5-proof}

## Tier 1 — Conceptual Model (Expanded)

### Claim
A Claim is a proposed genealogical assertion derived from one or more citations.  
Claims may contradict each other and may have varying confidence levels.

### Conclusion
A Conclusion is a reasoned determination about a person, event, or relationship.  
Every Conclusion must be backed by a ProofStatement.

### ProofStatement
A ProofStatement is a structured narrative explaining:

- Which claims were evaluated  
- How conflicts were resolved  
- Why the conclusion was chosen  

This ensures transparency and reproducibility.

---

## Tier 2 — Logical Model

### Claim
- statement  
- subject  
- citations[]  
- confidence  
- conflict_links[]  

### Conclusion
- subject  
- selected_claims[]  
- proofstatement_id  
- confidence  
- superseded_claims[]  

### ProofStatement  {#proof-model}
- conclusion_id  
- narrative (string or structured block list)  
- referenced_claims[]  
- reviewer / created_by  
- timestamps  

---

## Tier 3 — Implementation Model

### Location in Repository
genealogy/apps/reasoning/models/


### Implementation Requirements
- Claims must enforce ≥1 citation rule  
- Conclusions must enforce presence of a ProofStatement  
- ProofStatements must support markdown or structured text  

### Documentation Requirements
- Document implemented claim structure  
- Note reasoning automation plans (future)  

---

# Chapter 6 — Numbering, Cross-References, Appearances  {#chapter-6-references}

## Tier 1 — Conceptual Model
Models for interacting with genealogical publications:

- Cross-reference systems  
- Numbering schemes  
- Family appearance mappings  

---

## Tier 2 — Logical Model

### CrossReference Model  {#xref-model}
- number  
- type  
- associated_person  

### FamilyAppearance Model  {#familyappearance-model}
- person  
- family group identifier  
- appearance order  

### GeneratedConclusion Model  {#generatedconclusion-model}
- auto-generated narrative  
- links to conclusions  

---

## Tier 3 — Implementation Model

### Location in Repository
genealogy/apps/publications/models/


### Implementation Requirements
- Must maintain stable identifiers for publication output  
- Must support export formatting rules  

### Documentation Requirements
- Document numbering formats  
- Identify unsupported publication structures  
