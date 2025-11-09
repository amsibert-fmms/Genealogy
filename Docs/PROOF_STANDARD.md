# 🧾 GeneaX Proof Standard (GXPS)

## Overview
The **GeneaX Proof Standard (GXPS)** defines how genealogical conclusions are supported, scored, and validated within the GeneaX system.  
It adapts the **Genealogical Proof Standard (GPS)** to a structured, machine-readable model that integrates with **GEDCOM X** entities.

In short: **every claim needs proof, and every proof needs a source.**

---

## 🎯 Purpose
To provide a consistent and transparent method for:
- Evaluating genealogical conclusions.  
- Documenting the reasoning behind assertions.  
- Assigning confidence levels to data.  
- Maintaining source traceability for every relationship or fact.  

---

## 📚 Foundations

GXPS builds on the **five principles** of the *Genealogical Proof Standard (GPS)*:

1. **Reasonably exhaustive research**  
2. **Complete and accurate source citations**  
3. **Critical analysis and correlation of data**  
4. **Resolution of conflicting evidence**  
5. **A soundly reasoned, written conclusion**

In GeneaX, these principles are represented as structured data attached to `ProofStatement` objects.

---

## 🧩 Core Concepts

### **ProofStatement**
A `ProofStatement` represents a genealogical claim or conclusion supported by sources and analysis.

| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Unique identifier |
| `subject` | FK → `Person` | The entity or person the statement concerns |
| `claim` | Text | The specific genealogical assertion (e.g. “John Smith is the father of Mary Smith.”) |
| `sources` | M2M → `SourceDescription` | List of supporting evidence |
| `analysis` | Text | Explanation of reasoning and evaluation of evidence |
| `confidence_level` | Enum | One of `certain`, `probable`, `possible`, `speculative` |
| `conflicts` | JSON | References to conflicting statements and resolutions |
| `reviewed_by` | FK → `User` | Optional peer reviewer or verifier |
| `created_at` | DateTime | Timestamp of creation |
| `updated_at` | DateTime | Timestamp of last edit |

---

### **Confidence Levels**

| Level | Meaning | Typical Use |
|-------|----------|-------------|
| `certain` | Supported by primary, corroborated, and consistent evidence | Birth certificates, official records |
| `probable` | Strong evidence but minor gaps or secondary sources | Census, secondary records |
| `possible` | Suggestive evidence but insufficient corroboration | Inferred relationships |
| `speculative` | Hypothetical or unverified | “Might be related to…” theories |

💡 Confidence affects both **visual indicators** in the UI and **validation reports** during GEDCOM X exports.

---

## ⚙️ Validation Rules
Every relationship or fact in GeneaX must reference at least one **ProofStatement**.  
The following rules ensure data quality:

1. Missing proof → flagged as **unverified**.  
2. Conflicts unresolved → flagged as **incomplete**.  
3. Speculative claims → excluded from GEDCOM X export by default.  
4. Confidence downgraded if supporting sources lack citations.  

---

## 🧮 Evidence Scoring (Optional)
ProofStatements can carry a numeric **confidence score** (0.0–1.0) generated from:
- **Source Type Weighting**: original > derivative > authored.  
- **Information Quality**: primary > secondary > tertiary.  
- **Evidence Type**: direct > indirect > negative.  
- **Corroboration Count**: number of consistent supporting sources.

This allows algorithmic consistency checks and visual confidence indicators.

Example:

| Metric | Value | Weight | Score |
|--------|--------|--------|-------|
| Source Type | Original | 0.9 | 0.9 |
| Information | Primary | 0.8 | 0.8 |
| Evidence | Direct | 0.7 | 0.7 |
| Corroboration | 2 sources | 0.6 | 0.6 |
| **Composite Score** | — | — | **0.75 (Probable)** |

---

## 🧠 Integration with GEDCOM X

Each `ProofStatement` links to one or more GEDCOM X entities using `EvidenceReference`.  
This preserves compatibility and data portability.

```python
class ProofStatement(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    subject = models.ForeignKey(Person, on_delete=models.CASCADE)
    claim = models.TextField()
    analysis = models.TextField()
    confidence_level = models.CharField(
        max_length=12,
        choices=[
            ('certain', 'Certain'),
            ('probable', 'Probable'),
            ('possible', 'Possible'),
            ('speculative', 'Speculative'),
        ],
    )
    sources = models.ManyToManyField(SourceDescription)
    conflicts = models.JSONField(default=list, blank=True)
    reviewed_by = models.ForeignKey(User, null=True, blank=True, on_delete=models.SET_NULL)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

## 📊 Visualization & Reporting

- Proof levels displayed as color-coded badges (certain → green, speculative → red).
- Proof summaries automatically generated for each person.
- Validation report summarizing:
    - Missing proof statements
    - Conflicting evidence
    - Unsupported claims

## 🧩 Example JSON Output
```json
{
  "subject": "Person:12345",
  "claim": "John Smith is the father of Mary Smith.",
  "confidence_level": "probable",
  "sources": [
    {"id": "Source:6789", "title": "Baptism Record of Mary Smith"},
    {"id": "Source:6810", "title": "1841 Census, London"}
  ],
  "analysis": "Both records list John Smith as Mary’s father. No conflicts identified.",
  "conflicts": [],
  "reviewed_by": "User:admin",
  "created_at": "2025-10-27T14:21:00Z",
  "updated_at": "2025-11-08T09:13:00Z"
}
```

## 🧾 Summary
- Every fact or relationship must have at least one ProofStatement.	
- Confidence must be declared or derived.	
- Speculative statements excluded from export by default.	
- Validation must check for missing, conflicting, or outdated claims.	

“Truth may be relative, but your data shouldn’t be.”
