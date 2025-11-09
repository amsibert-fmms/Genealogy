# 🏗️ GeneaX Architecture

## Overview
**GeneaX** is a modular Django-based application structured around the **GEDCOM X specification** for genealogical data.  

The architecture prioritizes:
- **Data integrity** – strict adherence to GEDCOM X entities.  
- **Extensibility** – easily add new data types or validation rules.  
- **Transparency** – traceable, verifiable genealogical assertions.  
- **Educational clarity** – intentionally written for learning Django deeply.

---

## 🧩 Application Structure

```plaintext
geneax/
│
├── core/              # Shared utilities, mixins, base models
├── gedcomx/           # GEDCOM X data entities (Person, Relationship, etc.)
├── proof/             # ProofStandard logic (ProofStatement, evidence scoring)
├── api/               # REST API endpoints (DRF)
├── import_export/     # Import/export and schema validation logic
├── ui/                # Templates, static files, and front-end integration
│
├── docs/              # Documentation suite
├── tests/             # Unit and integration tests
└── manage.py
```

## ⚙️ Data Flow

**1. Input Layer**  
- Data can be entered manually via Django admin or imported as GEDCOM X JSON-LD.  
- Import pipeline validates data against the GEDCOM X schema and custom GeneaX rules.  

**2. Core Processing**  
- Validated entities are stored in the PostgreSQL database.  
- The `proof` app applies confidence scoring and creates ProofStatements.  
- Any conflicts or low-confidence claims are automatically flagged.  

**3. API Layer**  
- The REST API (Django REST Framework) exposes entities for external integration.  
- Supports CRUD operations, pagination, and filtering.  
- API responses are fully JSON-LD compliant.  

**4. Output Layer**  
- Export tools generate GEDCOM X JSON-LD or GeneaX proof bundles.  
- Visualization endpoints feed tree and timeline components in the UI.


## 🧱 Core Components
|Component | Description |
|-----|-----------------|
| **core/**	| Foundational utilities, base models, and shared mixins. |
| **gedcomx/**	| Implements primary GEDCOM X entities and relationships. |
| **proof/** | Houses the GeneaX Proof Standard implementation. |
| **api/** | REST API endpoints, serializers, and viewsets. |
| **import_export/** | Schema validation and GEDCOM X import/export logic. |
| **ui/** | Templates, static assets, and CSS/Tailwind theming. |

## 🗃️ Database Design Summary
- **Backend:** PostgreSQL
- **Schema:** Normalized tables with JSON fields for flexible genealogical structures.
- **Primary Keys:** UUIDs to align with GEDCOM X resource identifiers.
- **Major Entities:**
    - Person
    - Relationship
    - Event
    - Fact
    - SourceDescription
    - ProofStatement
    - Document
    - PlaceDescription

## 🔗 Interoperability
GeneaX aligns with GEDCOM X’s **data model** and **JSON-LD serialization** principles:
- Each entity maps to a corresponding GEDCOM X type.
- Imports and exports are schema-validated against the GEDCOM X JSON-LD spec.
- Extensible conversion layer for legacy GEDCOM 5.5.1 compatibility.

## 🧠 Design Principles
**1. Transparency over convenience.**
     Every relationship or assertion must trace back to a source or ProofStatement.
**1. Layered modularity.**
     Each Django app performs a single, clearly defined role.
**1. Human-legible logic.**
     Readable code > clever code. Future-you deserves mercy.
**1. Loose coupling, strict validation.**
     Apps can evolve independently, but all data must pass compliance checks.

## 🚀 Future Extensions
- GraphQL API for advanced querying.
- Family tree and timeline visualization APIs.
- Collaboration features (shared editing, user permissions).
- Provenance tracking for versioned historical records.

## 🧾 References
- [GEDCOM X Specification](https://github.com/FamilySearch/gedcomx)
- [Django REST Framework](https://www.django-rest-framework.org/)
- [PostgreSQL JSON Fields](https://www.postgresql.org/docs/current/datatype-json.html)


“Architecture is the art of making your future debugging sessions inevitable.”
