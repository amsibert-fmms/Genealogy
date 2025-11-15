# GeneaX Architecture {#geneax-architecture}
_Last updated: 2025-11-15_

Related references: [Documentation home](../index.md#geneax-docs-home) · [Master outline](../master-outline.md#master-outline)

Foundational description of the GeneaX application structure and its alignment with the chapter and tier model defined in the [master outline](../master-outline.md#master-outline).

---

## 1. Overview  
GeneaX is a modular Django-based application designed around the principles of:

- **Standards alignment** — Primary modeling follows the GEDCOM X specification.  
- **Data integrity** — Entities, relationships, and facts reflect explicit rules defined in the [validation rules](validation-rules.md#geneax-validation-rules).
- **Traceable reasoning** — Evidence → Claims → Conclusions → ProofStatements mirror genealogical best practices.  
- **Incremental growth** — Architecture supports expansion from Tier 1 (conceptual) to Tier 3 (implementation).  

This document describes how GeneaX maps domain concepts (Chapters 1–6) into a functional, maintainable application structure.

---

## 2. Architectural Layers  
The system is organized into three major layers that correspond to the tiers defined in the [master outline](../master-outline.md#master-outline).

### 2.1 Domain Layer (Tier 2 → Tier 3)  
Located primarily in Django models, this layer implements:

- Person (Chapter 1)  
- Event (Chapter 2)  
- Relationship (Chapter 3)  
- Source, Citation, Fact (Chapter 4)  
- Claims, Conclusions, Proof (Chapter 5)  
- CrossReference, FamilyAppearance (Chapter 6)

These models implement the **Tier 3 Implementation Model** and map directly onto the **Tier 2 Logical Model** described in the [data models](data-models.md#geneax-data-models).

### 2.2 Application Layer  
Contains the internal logic of GeneaX, including:

- Business rules  
- Validation routines (aligned with the [validation rules](validation-rules.md#geneax-validation-rules))
- Data services and orchestration  
- Import/export workflows  
- GEDCOM X converters  

This layer enforces constraints defined in the logical model.

### 2.3 API & Presentation Layer  
Exposes data and capabilities through:

- Django REST Framework (DRF) API  
- Admin views  
- Future UI views (timelines, family trees)  
- Future GraphQL endpoint  

API endpoints map directly to Tier 3 implementation classes.  
See the [API reference](api-reference.md#geneax-api-reference) for endpoint-level details.

---

## 3. Django Application Structure  

```plaintext
genealogy/
│
├── apps/
│   ├── persons/          # Chapter 1
│   ├── events/           # Chapter 2
│   ├── relationships/    # Chapter 3
│   ├── sources/          # Chapter 4
│   ├── reasoning/        # Chapter 5
│   ├── publications/     # Chapter 6
│   └── common/           # Shared utilities, enums, validators
│
├── api/
│   ├── serializers/
│   ├── viewsets/
│   ├── routers.py
│   └── schemas/
│
├── core/
│   ├── validation/       # Logical constraints
│   ├── mapping/          # GEDCOM X mappers
│   ├── workflows/
│   └── services/
│
└── utils/
    ├── date_parsing/
    ├── location/
    └── identifiers/
```
Each directory corresponds to a conceptual chapter or a shared cross-cutting concern.

---

## 4. Data Flow

### 4.1 Creation Flow
1. Client submits structured data through API  
2. Serializer validates input  
3. Logical rules applied ([validation rules](validation-rules.md#geneax-validation-rules))
4. Instance saved to ORM  
5. Optional: reasoning layer updates claims or conclusions  

### 4.2 Read Flow
1. ORM retrieves model instance  
2. Serializer expands references  
3. Optional: computed attributes (age, spans, derived facts)  
4. API returns JSON or GEDCOM X-aligned output  

### 4.3 Import Flow (GEDCOM X)
1. GEDCOM X input parsed  
2. Mapped to Tier 2 logical entities ([GEDCOM X compliance](gedcomx-compliance.md#geneax-gedcomx))
3. Logical validation (see [validation rules](validation-rules.md#geneax-validation-rules))
4. ORM instances created or merged (document interoperability notes in [GEDCOM X compliance](gedcomx-compliance.md#geneax-gedcomx))

---

## 5. Alignment With Chapters

| Chapter | Architectural Location | Description |
|--------|-------------------------|-------------|
| 1. Person | `apps/persons/` | Identity data and person-level logic |
| 2. Event | `apps/events/` | Event types, dates, places, participant roles |
| 3. Relationship | `apps/relationships/` | Structured person-to-person connections |
| 4. Sources | `apps/sources/` | Source descriptions, citations, facts |
| 5. Proof | `apps/reasoning/` | Claims, conclusions, proof statements |
| 6. Numbering | `apps/publications/` | Cross-references, numbering, appearances |

---

## 6. Scaling and Extension

The architecture is designed for incremental extension.

### 6.1 Planned Additions
- GraphQL endpoint  
- Visualization components (tree view, timelines, charts)  
- Collaborative editing and permissions  
- Provenance tracking for record changes  
- Automated inference and narrative generation  

### 6.2 External Integrations
- GEDCOM X import/export pipelines  
- Potential integration with FamilySearch APIs  
- Optional OCR workflows  

---

## 7. References
- GEDCOM X Specification  
- Django REST Framework  
- PostgreSQL JSON/JSONB  
- [Data models](data-models.md#geneax-data-models) — logical and implementation models
- [Proof standard](proof-standard.md#geneax-proof-standard) — reasoning and conclusion structure