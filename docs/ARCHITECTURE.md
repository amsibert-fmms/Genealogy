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
