# ✅ GeneaX Validation Rules

Every record in GeneaX is subject to strict validation based on:
- The **GEDCOM X specification**
- The **GeneaX Proof Standard (GXPS)**
- Internal consistency, cross-referencing, and schema completeness

This document outlines validation rules enforced during:
- Manual entry
- Import
- Export
- API operations

---

## 🔍 Entity-Level Rules

### 🧍 Person
- Must include `full_name`
- Must link to at least one `SourceDescription` OR `ProofStatement`
- Optional `book_ref` must match `CrossReference.composite_id`

### 🔗 Relationship
- Must connect two unique `Person` records
- `type` must be recognized GEDCOM X or GeneaX URI
- If `proof` is missing → **flag as unverified**
- If `proof.confidence_level` is `speculative` → excluded from default exports

### 🗓️ Event
- Must include `type` and at least one of: `date`, `place`, `description`
- Linked `PlaceDescription` must exist
- `source` is required for all public events

### 📚 SourceDescription
- Must include `source_key` and `title`
- `source_key` must be unique across all sources
- Any linked `CrossReference` must reference an existing source

---

## 📄 ProofStatement
- `claim` and `analysis` required
- Must link to at least one `SourceDescription`
- `confidence_level` must be one of: `certain`, `probable`, `possible`, `speculative`
- If `conflicts` exist, they must link to valid `ProofStatement` IDs
- If `confidence_level = speculative`, flag for review and **exclude from GEDCOM X export**

---

## 📘 CrossReference
- `composite_id` must follow format `[SourceKey]:[RecordNumber]` (e.g. `JH12:456`)
- `composite_id` must be unique per `SourceDescription`
- `target_id` must correspond to an existing `Person`, `Event`, or other supported entity
- Circular references allowed (e.g., family ↔ child ↔ in-law), but **must be logged**

---

## 📖 FamilyAppearance
- `family_id` must match a known `CrossReference`
- `position` must be one of: `child`, `spouse`, `in-law`, etc.
- Person cannot appear twice in the same family with the same `position`

---

## 🧠 Proof Integration Checks
| Rule | Action |
|------|--------|
| Missing `ProofStatement` for relationship | Mark as **Unverified** |
| Multiple conflicting `ProofStatements` with same `confidence_level` | Flag as **Conflict** |
| No sources in `ProofStatement` | Downgrade `confidence_level` to `speculative` |
| Outdated `ProofStatement` (last updated >5 years ago) | Mark for **Review** |

---

## 🔄 Import Validation
- GEDCOM X import must pass:
  - Schema validation against `gedcomx-schema.json`
  - Logical checks for required fields
  - Reference resolution for all `@id` references
- Invalid records: quarantined, not saved
- Speculative claims: imported but excluded from default exports

---

## 📤 Export Validation
- Export fails if:
  - Unresolved references
  - Missing required proof or sources
  - Invalid JSON-LD context mappings
- Speculative data excluded unless `?include_speculative=true`

---

## 🧾 Summary

| Area | Enforcement |
|------|-------------|
| Entity Required Fields | ✅ Enforced |
| Source/Proof Presence | ✅ Enforced |
| CrossRef Integrity | ✅ Enforced |
| Conflict Resolution | ⚠️ Logged |
| Speculative Logic | ✅ Enforced |
| JSON-LD Schema | ✅ Validated |
| Timeline Events | ⚠️ Warned if missing dates |

---

> “Data is sacred. You’re just borrowing it from the dead. Treat it with respect.”

