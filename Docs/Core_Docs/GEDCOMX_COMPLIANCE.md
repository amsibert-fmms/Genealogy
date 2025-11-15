# GEDCOM X Compliance
This document describes how GeneaX aligns with the GEDCOM X Specification.  
It corresponds primarily to **Tier 2 Logical Models** across Chapters 1–4, with limited extensions in Chapters 5–6.

---

# 1. Overview
GeneaX adopts GEDCOM X as its primary genealogical data standard.  
Compliance ensures:

- Interoperability with modern genealogical systems  
- Predictable import/export behavior  
- High fidelity when mapping people, events, relationships, and sources  
- Structural consistency across the GeneaX data model  

This document maps GeneaX entities to their GEDCOM X counterparts and identifies GeneaX extensions where needed.

---

# 2. Compliance Goals
1. Implement core GEDCOM X entities within GeneaX models.  
2. Ensure all data imported or exported validates against the official GEDCOM X JSON-LD schema.  
3. Maintain compatibility with existing GEDCOM X consumers.  
4. Extend entities only when necessary for GeneaX-specific features (Chapters 5–6).  
5. Preserve structural integrity during import, export, and transformation workflows.

---

# 3. Mapping to Chapters and Tiers

### Chapters Primarily Involved
- **Chapter 1 — Person**  
- **Chapter 2 — Event**  
- **Chapter 3 — Relationship**  
- **Chapter 4 — Sources & Citations**

### Tiers
- **Tier 1** — Conceptual entities match GEDCOM X categories.  
- **Tier 2** — Logical models map directly to GEDCOM X schema elements.  
- **Tier 3** — Implementation handles conversions, validations, and JSON-LD representation.

Extended models (Chapters 5–6) introduce structures beyond GEDCOM X but remain compatible.

---

# 4. Core GEDCOM X Entity Mapping

## 4.1 Person  {#person}
GeneaX Person Model → GEDCOM X `Person`  
Mappings include:

- Names  
- Gender  
- Facts (birth, death, occupation, etc.)  
- Identifiers  
- Links to relationships and events  

See `DATA_MODELS.md#person-model`.

---

## 4.2 Relationship  {#relationship}
GeneaX Relationship Model → GEDCOM X `Relationship`  
Supported types include:

- Parent-child  
- Couple  
- Spouse  
- Partner  

Extended types (guardian, adoptive, sibling) are GeneaX-specific but remain structurally compatible.

See `DATA_MODELS.md#relationship-model`.

---

## 4.3 Event  {#event}
GeneaX Event Model → GEDCOM X `Event` and `EventRole`  

Mappings include:

- Event type  
- Date / date range  
- Place  
- Participating persons  
- Event roles  

See `DATA_MODELS.md#event-model`.

---

## 4.4 SourceDescription  {#source}
GeneaX Source Model → GEDCOM X `SourceDescription`  

Includes:

- Title  
- Citation text  
- Publication details  
- Links to facts or events  

GeneaX adds structured identifiers useful for publication mapping (Chapter 6).

See `DATA_MODELS.md#source-model`.

---

## 4.5 Fact
GeneaX Fact Model → GEDCOM X `Fact`  

Examples:

- Birth fact  
- Death fact  
- Residence  
- Occupation  

GeneaX extends Fact with internal confidence scoring (Chapter 5).

---

# 5. JSON-LD Representation

### 5.1 Export Rules
- GeneaX exports follow GEDCOM X JSON-LD context.  
- All entities must include identifiers compatible with `@id` rules.  
- Relationships must use standard GEDCOM X type URIs.  
- Dates and places must conform to GEDCOM X formatting guidelines.

### 5.2 Import Rules
- All incoming GEDCOM X JSON-LD must be schema-validated.  
- Unknown or extended types are preserved when possible.  
- Unmapped extensions are stored in auxiliary structures for review.

---

# 6. GeneaX Extensions to GEDCOM X

GeneaX introduces several domain-specific extensions while maintaining structural compatibility.

### 6.1 CrossReference Model  
Supports publication-style numbering systems.  
Corresponds to Chapter 6.

### 6.2 FamilyAppearance  
Represents how individuals or families appear in a structured publication or compiled genealogy.  
No GEDCOM X equivalent exists; implemented as an extension.

### 6.3 Extended Relationship Types  
Adds optional types (e.g., guardian, adoptive) beyond the base GEDCOM X set.  
Mapped using `type` URIs compatible with GEDCOM X semantics.

### 6.4 Proof and Reasoning Layer  
(GeneX-only)  
Models claims, conclusions, and proof statements (Chapter 5).  
These do **not** conflict with GEDCOM X because they operate above the data layer.

---

# 7. Validation Requirements

GeneaX performs the following validations for GEDCOM X compliance:

- Person, Event, and Relationship models must include required GEDCOM X fields.  
- JSON-LD exports must conform to GEDCOM X context definitions.  
- Date and place formats must follow GEDCOM X formatting conventions.  
- Unsupported or malformed structures must be flagged and quarantined.  

See `VALIDATION_RULES.md` for full detail.

---

# 8. Interoperability Considerations

- GeneaX maintains forward-compatibility with GEDCOM X core.  
- Data imported from non-GEDCOM X systems is normalized before mapping.  
- Exported GEDCOM X data is suitable for external systems such as FamilySearch.  
- Structural extensions are isolated to avoid breaking downstream consumers.

---

# 9. Compliance Status Summary

| Category                  | Status       | Notes                                       |
|---------------------------|--------------|---------------------------------------------|
| GEDCOM X Base Model       | Documented   | Core entities mapped; implementation ongoing |
| JSON-LD Compliance        | Documented   | Context structure designed; validation pending |
| CrossReference Extension  | Documented   | Fully designed; implementation pending        |
| FamilyAppearance Model    | Documented   | Designed for publication mapping              |
| Extended Relationships    | Documented   | Additional types defined; logic deferred      |
| Legacy GEDCOM 5.5.1       | Planned      | Optional import/export for later phase        |

---

# 10. Summary

GeneaX aligns closely with the GEDCOM X specification while extending it in areas needed for:

- Publication mapping  
- Reasoning and proof structures  
- Enhanced relationship modeling  
- Data integrity and validation workflows  

This compliance layer ensures high-quality genealogical interoperability across systems.

