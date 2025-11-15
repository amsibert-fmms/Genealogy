# GeneaX Features {#geneax-features}
_Last updated: 2025-11-15_

Related references: [Documentation home](../index.md#geneax-docs-home) · [Master outline](../master-outline.md#master-outline)

This document summarizes the current, planned, and future features of the GeneaX platform.
All features are organized to align with the chapter structure defined in the [master outline](../master-outline.md#master-outline).

---

## 1. Overview
GeneaX combines a modern Django architecture with the structured genealogical guidance of GEDCOM X.  
Features are grouped according to the major domain areas (Chapters 1–6) and categorized by development stage.

Development stages:
- **Implemented** — Available in the current system  
- **Planned** — Defined in design documents; implementation pending  
- **Future** — Conceptual or exploratory features  

---

# 2. Chapter-Aligned Features

## Chapter 1 — Person
### Implemented
- Basic person entity support (Tier 3)  
- Identity attributes: names, gender, life span fields  
- CRUD operations through Django admin and API  

### Planned
- Alternate names and name types  
- Person merging and duplicate detection  
- Person timelines (integration with Events)  

### Future
- Identity resolution across imported GEDCOM X sources

---

## Chapter 2 — Event
### Implemented
- Event model structure aligned with Tier 2  
- Event types, dates, places, and participants  
- API creation and retrieval

### Planned
- Event role classification  
- Event place normalization  
- Multi-date interpretations (e.g., ranges, approximations)

### Future
- Event visualizations and chronological graphs

---

## Chapter 3 — Relationship
### Implemented
- Support for essential relationship types (parent–child, spouse)  
- Validation rules for allowable structures  

### Planned
- Temporal bounds for relationships  
- Extended relationship types (guardian, adoptive, sibling)  
- Relationship conflict detection

### Future
- Graph-based kinship calculations

---

## Chapter 4 — Sources, Citations, and Facts
### Implemented
- SourceDescription structure (Tier 2)  
- Basic citation support  
- Fact model design documented in the [data models](data-models.md#chapter-4-sources) reference

### Planned
- Source ingestion and structured extraction workflows  
- Citation-level evidence assessment  
- Fact-level confidence scoring  

### Future
- OCR-assisted record import  
- Automated metadata extraction

---

## Chapter 5 — Claims, Conclusions, and Proof
### Implemented
- ProofStatement model (Tier 2)  
- Conceptual reasoning framework defined in the [proof standard](proof-standard.md#geneax-proof-standard)

### Planned
- Conclusion model implementation  
- Multi-citation claims  
- Integrated evidence evaluation workflow  

### Future
- Semi-automated narrative generation  
- Conflict analysis between competing conclusions  

---

## Chapter 6 — Numbering, Appearances, and Cross-References
### Implemented
- Basic CrossReference model  
- Support for external numbering schemes

### Planned
- FamilyAppearance model implementation  
- Publication rendering and structured numbering generation  

### Future
- Export to book formats (including numbering systems and appearances)

---

# 3. System-Level Features

## 3.1 Data Interchange
### Implemented
- GEDCOM X import/export (baseline mappings)

### Planned
- Full GEDCOM X JSON-LD compliance  
- Import validation and transformation pipeline definitions

### Future
- Integration with FamilySearch or WikiTree APIs

---

## 3.2 API and Integration
### Implemented
- Django REST Framework endpoints for core models  
- Basic serializers for Chapters 1–4  
- Token-based authentication

### Planned
- Comprehensive DRF endpoint coverage  
- Schema-first API documentation  
- Versioned API design  

### Future
- GraphQL endpoint

---

## 3.3 Developer Tools
### Implemented
- Local development configuration  
- Model-driven architecture compatible with Tier 2 design  
- Unit test scaffolding

### Planned
- Factory sets for models  
- Validation and reasoning workflow tests  

### Future
- CLI utilities for bulk import/export and data inspection

---

# 4. Future Exploration
The following ideas are speculative and not yet part of the roadmap:

- Automated duplicate detection using machine learning  
- Historical place normalization service  
- Versioned record provenance with diff viewer  
- Visualization tools (timeline animations, relationship heatmaps)

---

# 5. References
- [Master outline](../master-outline.md#master-outline) — conceptual framework
- [Data models](data-models.md#geneax-data-models) — logical and implementation details
- [Validation rules](validation-rules.md#geneax-validation-rules) — constraints and integrity requirements
- [Proof standard](proof-standard.md#geneax-proof-standard) — evidence and reasoning model
- [GEDCOM X compliance](gedcomx-compliance.md#geneax-gedcomx) — alignment with the GEDCOM X specification