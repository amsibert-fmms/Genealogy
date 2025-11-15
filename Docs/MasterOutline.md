# GeneaX Master Outline  
Unified table of contents and structural reference for the GeneaX documentation set.  
Each chapter presents one conceptual entity or domain area, progressing from:
- Tier 1: Conceptual Model  
- Tier 2: Logical Model  
- Tier 3: Implementation Model  

Supplemental documents should anchor their relevant sections to these chapters.

---

## Chapter 1 — Person  {#chapter-person}
Tier 1: Conceptual definition of a Person  
Tier 2: Logical Person Model  
Tier 3: Person ORM implementation  
Detailed model: `Core_Docs/DATA_MODELS.md#chapter-1-person`

## Chapter 2 — Event  {#chapter-event}
Tier 1: Conceptual Event  
Tier 2: Logical Event Model  
Tier 3: Event ORM  
Detailed model: `Core_Docs/DATA_MODELS.md#chapter-2-event`

## Chapter 3 — Relationship  {#chapter-relationship}
Tier 1: Conceptual Relationship  
Tier 2: Logical Relationship Model  
Tier 3: Implementation  
Detailed model: `Core_Docs/DATA_MODELS.md#chapter-3-relationship`

## Chapter 4 — Sources & Citations  {#chapter-sources}
Tier 1: Conceptual Source and Citation  
Tier 2: Source, Citation, and Fact Models  
Tier 3: Implementation  
Detailed model: `Core_Docs/DATA_MODELS.md#chapter-4-sources`

## Chapter 5 — Claims, Conclusions, and Proof  {#chapter-proof}
Tier 1: Conceptual reasoning system  
Tier 2: ProofStatement, Conclusion models  
Tier 3: Implementation  
Detailed model: `Core_Docs/DATA_MODELS.md#chapter-5-proof`

## Chapter 6 — Numbering, Cross-References, Appearances  {#chapter-references}
Tier 1: Conceptual handling of external numbering and publication placement  
Tier 2: CrossReference and FamilyAppearance models  
Tier 3: Implementation  
Detailed model: `Core_Docs/DATA_MODELS.md#chapter-6-references`

---

## Cross-Document Map

### Architecture  
`Core_Docs/ARCHITECTURE.md`

### Validation Rules  
`Core_Docs/VALIDATION_RULES.md`

### GEDCOM-X Mapping  
`Core_Docs/GEDCOMX_COMPLIANCE.md`

### Developer Documentation  
Installation, Configuration, Testing, Deployment  
Located in `Docs/Developer_Docs/`

---

## Growth Notes
- Add new chapters as new conceptual areas are introduced.  
- Anchor each new chapter in both this outline and the Data Models document.  
- Maintain the chapter order to preserve conceptual flow: Person → Event → Relationship → Evidence → Reasoning → Publication Structures.  
