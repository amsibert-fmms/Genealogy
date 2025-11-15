# 🧬 GEDCOM X Compliance

## Overview
**GeneaX** adheres closely to the **GEDCOM X Specification**, ensuring data interoperability and consistency across genealogy systems.  
This document outlines how GeneaX models and extensions align with the specification — including **CrossReferences**, **FamilyAppearances**, and **extended relationships** designed for community genealogical works.

*We follow the standard, except when it forgot the fun parts.*

---

## 📜 Compliance Goals
1. Implement all major GEDCOM X data structures.  
2. Ensure all imported/exported data validates against the official GEDCOM X JSON-LD schema.  
3. Preserve compatibility with existing GEDCOM X consumers.  
4. Extend the model where necessary, without breaking structural integrity.  

---

## 🧩 Core Entity Mapping

| GEDCOM X Entity | GeneaX Model | Notes |
|-----------------|--------------|-------|
| `Person` | `gedcomx.models.Person` | Fully compliant with identifiers, gender, and facts. |
| `Relationship` | `relationships.models.Relationship` | Extends base relationships with new types (officiant, property, witness). |
| `Event` | `gedcomx.models.Event` | Used for births, deaths, marriages, property transfers, etc. |
| `Fact` | `gedcomx.models.Fact` | Implements attributes like date, place, and type. |
| `PlaceDescription` | `gedcomx.models.PlaceDescription` | Stores geographic metadata for events. |
| `SourceDescription` | `gedcomx.models.SourceDescription` | Manages citations, publication data, and provenance. |
| `Document` | `gedcomx.models.Document` | Represents transcriptions or attached digital media. |
| `EvidenceReference` | `proof.models.ProofStatement` | References GEDCOM X entities with confidence scoring. |
| `Conclusion` | `proof.models.GeneratedConclusion` *(extension)* | Structured representation of the “written conclusion” from the Genealogical Proof Standard. |
| *(Extension)* | `relationships.models.FamilyAppearance` | Contextual family role links (child, spouse, in-law, etc.) within a publication. |
| *(Extension)* | `relationships.models.CrossReference` | Handles book/family IDs (e.g., `JH12:1234`) and cross-source entity mapping. |

---

## 🧱 GeneaX Extensions

### **1. CrossReference**
Encodes the book-style ID systems used in Amish and community genealogical publications.

| Field | Type | Description |
|-------|------|-------------|
| `composite_id` | String | Combined identifier (e.g. `JH12:1234`). |
| `source` | FK → `SourceDescription` | The publication defining this ID. |
| `target_id` | UUID | The actual entity (Person, Family, or Event) this ID refers to. |
| `position` | Enum | Context within the source (child, spouse, in-law, etc.). |
| `references` | M2M → self | Optional cross-links to matching or related entries. |

📚 *Compliant with GEDCOM X `Identifier` semantics and exported as `gx:BookReference`.*

---

### **2. FamilyAppearance**
Models a person’s contextual role in a specific family entry within a publication.

| Field | Type | Description |
|-------|------|-------------|
| `person` | FK → `Person` | The individual appearing in the record. |
| `source` | FK → `SourceDescription` | The publication defining the family. |
| `family_id` | String | The family’s composite ID (e.g. `JH12:6789`). |
| `position` | Enum | Role (child, spouse, in-law, etc.). |
| `cross_reference` | FK → `CrossReference` | Link to the other family entry for cross navigation. |

📖 *Maps to GEDCOM X `Relationship` + contextual `EvidenceReference`.*

---

### **3. Extended Relationships**
Adds culturally relevant relational types beyond standard parent/child/spouse definitions.

| Type | URI | Description |
|------|-----|-------------|
| `officiant` | `https://geneax.org/vocab#OfficiantPerformer` | Person who performed a marriage ceremony. |
| `property-seller` | `https://geneax.org/vocab#PropertySeller` | Seller in a property transfer. |
| `property-buyer` | `https://geneax.org/vocab#PropertyBuyer` | Buyer in a property transfer. |
| `witness` | `https://geneax.org/vocab#Witness` | Witness to an event, transaction, or record. |

🧩 *GEDCOM X–compliant via project-scoped vocabulary URIs.*

---

## 🔗 JSON-LD Context Mapping

```json
{
  "@context": {
    "gx": "https://geneax.org/vocab#",
    "ProofStatement": "gx:ProofStatement",
    "GeneratedConclusion": "gx:GeneratedConclusion",
    "CrossReference": "gx:CrossReference",
    "FamilyAppearance": "gx:FamilyAppearance",
    "confidence_level": "gx:confidenceLevel",
    "analysis": "gx:analysis",
    "conflicts": "gx:conflicts",
    "BookReference": "gx:BookReference"
  }
}
```

---

## 🧠 Validation & Compliance Checks
|Check	|Description|
|---|------------------|
|Schema Validation	|All JSON-LD exports validated against GEDCOM X + GeneaX context.|
|CrossReference |Integrity	Every composite_id must match a valid SourceDescription.|
|FamilyAppearance Rules	|Circular references (e.g., spouse ↔ child) allowed but logged.|
|Relationship Typing	|Custom types must use a registered GeneaX vocabulary URI.|
|Proof Integration	|All relationship claims must have an associated ProofStatement.|

---

## 🧮 Example Export
```json
{
  "persons": [
    {
      "id": "Person:JH12-1234",
      "identifiers": [
        {
          "type": "gx:BookReference",
          "value": "JH12:1234",
          "source": "Source:JH12"
        }
      ],
      "evidence": ["ProofStatement:0001"]
    }
  ],
  "relationships": [
    {
      "type": "https://geneax.org/vocab#OfficiantPerformer",
      "person1": "Person:JH12-0099",
      "person2": "Person:JH12-1234",
      "event": "Event:1901-Marriage",
      "sources": ["Source:JH12"]
    }
  ]
}
```

---

## 🧾 Summary
|Category	|Status	|Notes|
|---|---|---|
|GEDCOM X Base Model	|📄 Documented	|Core entities defined, implementation forthcoming.|
|JSON-LD Compliance	|📄 Documented	|Context structure planned, not yet validated.|
|CrossReference System	|📄 Documented	|Schema drafted, logic design complete.|
|FamilyAppearance	|📄 Documented	|Context model designed for publication mapping.|
|Extended Relationships	|📄 Documented	|Relationship types defined, implementation TBD.|
|Legacy GEDCOM 5.5.1	|🚧 Planned	|Optional import/export converter for later phase.|

“Standards compliance: currently existing in theory, but that’s where all great specs begin.”
