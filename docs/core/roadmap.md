# 🗺️ GeneaX Development Roadmap {#geneax-roadmap}
_Last updated: 2025-11-15_

Related references: [Documentation home](../index.md#geneax-docs-home) · [Master outline](../master-outline.md#master-outline)


This roadmap outlines major milestones, phases, and development priorities for GeneaX — a Django-based genealogy platform built for structured, evidence-backed family history.

---

## 📍 Roadmap Overview

| Phase | Focus | Description | Status |
|-------|--------|-------------|--------|
| **1** | Core Models | Implement all GEDCOM X base entities and CRUD endpoints | ✅ In Progress |
| **2** | Proof System | Apply GXPS across claims, relationships, and validations | ✅ In Progress |
| **3** | Import/Export | GEDCOM X JSON-LD import/export; legacy GEDCOM adapter | 🚧 Planned |
| **4** | Data Visualization | Family tree UI, timelines, relationship graphs | 🚧 Planned |
| **5** | Collaboration | User accounts, permissions, editing workflows | 🚧 Planned |
| **6** | Interop Layer | API polish, 3rd-party tool integration, GEDCOM 5.5.1 support | 🚧 Planned |
| **7** | UI Customization | Theme settings, accessibility, mobile support | 🚧 Planned |

---

## 🧩 Current Work

- ✅ GEDCOM X data models (`Person`, `Event`, `Source`, `Relationship`)
- ✅ GXPS implementation with ProofStatements
- ✅ JSON-LD context planning
- ✅ API endpoints scaffolded with DRF
- ✅ Initial data validation rules

---

## 🧠 Near-Term Goals

- Add test fixtures and schema validation tests  
- Create import pipelines for GEDCOM X samples  
- Add audit logging to model changes  
- Build admin utilities for identifying incomplete or speculative records  

---

## 🔭 Mid-Term Goals

- Build UI prototype for family trees using D3.js or Cytoscape  
- Implement timeline view for individual life spans and events  
- Support phonetic surname matching for fuzzy record discovery  
- Add user registration, login, and personal workspace support  

---

## 🚀 Long-Term Ambitions

- GraphQL API for advanced frontends  
- Visual diff tool for versioned records and ProofStatement comparisons  
- GEDCOM 5.5.1 parser for older tools  
- Historical place name normalization and mapping  
- Integration with FamilySearch and WikiTree APIs  
- AI-assisted duplicate detection and conflict resolution

---

## ⚠️ Known Gaps

- No frontend UI exists yet (just templates)  
- No CI pipeline or test coverage reports  
- Export schema currently lacks full coverage for extended relationships  
- PlaceDescriptions do not yet include geolocation or historical mapping  

---

## 🧾 How to Contribute

- Clone the repo, make a branch (`feature/your-name/what-it-does`)
- Keep commits small, readable, and honest
- Link every model/endpoint to the related GEDCOM X doc
- All contributions must pass linting and include tests
- Bonus: leave a trail of breadcrumbs in [NOTES.md](../NOTES.md) (create it if it does not exist yet)

---

> “Roadmaps are lies we tell ourselves about the future — and then we build them anyway.”