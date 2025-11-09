# 🌿 GeneaX Features

## Overview
**GeneaX** combines Django’s flexibility with the structured power of the **GEDCOM X** specification to build a verifiable and interoperable genealogy platform.  
This document outlines current and planned features, grouped by core functionality and development phase.

---

## 🧩 Core Features

### 1. **GEDCOM X Data Management**
- Full CRUD for all GEDCOM X entities:  
  `Person`, `Relationship`, `Fact`, `Event`, `PlaceDescription`, `SourceDescription`, `Document`.  
- Import/export of GEDCOM X JSON-LD files.  
- Schema validation with clear error reporting.  
- API endpoints for external system integration.

🧠 *This is the backbone of GeneaX — the data engine that keeps your ancestors behaving like structured data, not chaos incarnate.*

---

### 2. **Book & Family Cross-Reference System**
- Each person or family can include a Book ID reference (e.g. JH12:1234), representing the   numbering system used in community genealogy books.
- CrossReference model links people across multiple publications or editions.
- Supports roles within family listings (e.g. child, wife, spouse, in-law).
- Allows bidirectional references between family entries (e.g. JH12:1234 child ↔ JH12:6789 wife).
- Enables direct search and lookup by book or family ID.
- Fully integrated with the Proof Standard and Relationship Resolution systems.

📖 *Because “see family #1234” deserves to mean something in your database.*

---

### 3. **Proof & Evidence System**
- Integration of the **GeneaX Proof Standard (GXPS)**.  
- Confidence ratings for each claim (`certain`, `probable`, `possible`, `speculative`).  
- ProofStatements linking claims to sources, analysis, and conflicts.  
- Visual indicators for low-confidence or unverified assertions.  
- Validation checks that ensure every relationship has a proof reference.

💬 *Because "family lore" isn’t data until it’s verified.*

---

### 4. **Data Visualization**
- Interactive family tree display (zoom, pan, expand, collapse).  
- Timeline view of life events and relationships.  
- Relationship graph visualization using D3.js or Cytoscape.  
- Geographical map of historical events (Leaflet).  

🎨 *So your data can look impressive while you pretend you’re not debugging JavaScript.*

---

### 5. **Search & Discovery**
- Full-text and filtered search for people, events, and sources.  
- Phonetic (Soundex / Metaphone) surname matching.  
- Fuzzy duplicate detection for potential record merges.  
- Smart query builder for power users.

🔍 *Because your 3rd great-grandfather might be hiding behind a spelling error.*

---

### 6. **Import / Export / Interoperability**
- GEDCOM X JSON-LD import/export (core).  
- Legacy GEDCOM 5.5.1 converter (optional).  
- CSV import for quick testing.  
- API endpoint for bulk data exchange.  

🔁 *For connecting your better-designed app to everyone else’s worse one.*

---

### 7. **User Accounts & Collaboration**
- Django-based authentication system.  
- Personal “workspaces” for building private family trees.  
- Shared project editing with role-based permissions.  
- Revision history per record (audit trail).  

👥 *Because genealogy is teamwork… until someone edits the wrong grandma.*

---

### 8. **Validation & Quality Tools**
- Schema validation for GEDCOM X compliance.  
- Proof integrity checks (missing sources, unresolved conflicts).  
- Research completeness dashboard.  
- Visual indicators for unverified or incomplete data.  

📊 *A gentle reminder that your data is messy.*

---

### 9. **Customization & UI**
- Tailwind CSS framework with a fully customizable theme.  
- Light/dark mode toggle.  
- Configurable layout and typography via CSS variables.  
- Mobile-friendly templates for editing on the go.  

🎨 *Change colors, not code.*

---

## 🧾 Feature Roadmap

| Phase | Focus | Description | Status |
|-------|--------|-------------|--------|
| **1** | Core Models | Base GEDCOM X entities and CRUD | ⏳ Planned |
| **2** | Proof System | GXPS integration and confidence tracking | ⏳ Planned |
| **3** | Import/Export | GEDCOM X JSON-LD parser and exporter | ⏳ Planned |
| **4** | Visualization | Family trees, timelines, maps | ⏳ Planned |
| **5** | Collaboration | Multi-user editing and permissions | ⏳ Planned |
| **6** | Interop Layer | API and legacy GEDCOM compatibility | ⏳ Planned |
| **7** | UI Theming | Customizable styles and dark mode | ⏳ Planned |

### 🕳️ Project Stage:
- *“Currently existing primarily in Markdown and hubris.”*

---

## 🔮 Future Ideas (Nice-to-Haves)
- AI-assisted duplicate resolution and entity merging.  
- Historical place name normalization.  
- Versioned record provenance and diff viewer.  
- Integration with FamilySearch or WikiTree APIs.  
- Timeline animations (because why not).  

---

*“Features are promises to your future self — be kind, or at least realistic.”*
