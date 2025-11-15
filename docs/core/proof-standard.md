# GeneaX Proof Standard (GXPS) {#geneax-proof-standard}
_Last updated: 2025-11-15_

Related references: [Documentation home](../index.md#geneax-docs-home) · [Master outline](../master-outline.md#master-outline)

The GeneaX Proof Standard defines how genealogical claims, conclusions, and proof statements are evaluated, documented, and validated within the system.  
This document corresponds to **Chapter 5** in the [master outline](../master-outline.md#chapter-5-proof).

---

# 1. Overview
The GeneaX Proof Standard (GXPS) adapts traditional genealogical reasoning into a structured, machine-readable model. Its purpose is to ensure that:

- Every genealogical claim is supported by evidence  
- Every conclusion is derived through transparent reasoning  
- Every proof statement is traceable to its sources  
- Conflicts are identified, recorded, and resolvable  

GXPS integrates directly with the Tier 2 Logical Models for Claims, Conclusions, and ProofStatements described in the [data models](data-models.md#geneax-data-models).

---

# 2. Purpose
The Proof Standard provides a consistent framework for:

- Evaluating genealogical conclusions  
- Documenting the reasoning behind assertions  
- Assigning confidence levels to claims  
- Ensuring source traceability  
- Managing conflicting evidence  
- Supporting automated and manual review workflows  

It ensures that genealogical data remains verifiable, maintainable, and interoperable.

---

# 3. Alignment With Chapters and Tiers

- **Chapter 5** defines the conceptual structure of claims, conclusions, and proof.  
- **Tier 1** describes the reasoning concepts (claim → conclusion → proof).  
- **Tier 2** defines the full logical data model for ProofStatements, Conclusions, and associated relationships.  
- **Tier 3** defines the Django ORM implementation for the reasoning layer.

Relevant models in the [data models](data-models.md#geneax-data-models):

- [Proof model](data-models.md#proof-model)
- [Fact model](data-models.md#fact-model)
- [Conclusion model](data-models.md#conclusion-model)

---

# 4. Core Reasoning Entities

## 4.1 Claim
A *Claim* (or Fact Assertion) represents a proposed genealogical statement such as:

- “John Smith was born in 1842.”  
- “Mary Jones is the daughter of Thomas Jones.”

### Characteristics
- Claims reference one or more **Citations**.  
- Claims may conflict with other claims.  
- Claims may represent low-, medium-, or high-confidence statements.

### Model Links
Logical structure: [Data models — Fact](data-models.md#fact-model)
Citation structure: `Chapter 4 — Sources & Citations`

---

## 4.2 Conclusion
A *Conclusion* represents a reasoned determination about a person, event, or relationship.

### Characteristics
- Derived from one or more claims  
- Must be supported by a ProofStatement  
- May override conflicting claims  
- Should represent the best-supported interpretation of the evidence  

### Model Links
Logical structure: [Data models — Conclusion](data-models.md#conclusion-model)

---

## 4.3 ProofStatement
A *ProofStatement* is a structured narrative explaining how a conclusion was reached.

### Characteristics
- Must reference all claims used in the reasoning process  
- Summarizes evidence, contradictions, and resolution  
- Maps to external genealogical proof standards via Tier 2  
- Required for any conclusion exported or published  

### Model Links
Logical structure: [Data models — Proof](data-models.md#proof-model)
Standard mapping: [GEDCOM X compliance](gedcomx-compliance.md#geneax-gedcomx)

---

# 5. Evidence and Citation Requirements

## 5.1 Mandatory Citation
Every claim must link to at least one **Citation**.  
Citations must reference a **SourceDescription** (Chapter 4).

## 5.2 Multi-Citation Support
Claims may be supported by multiple citations.  
Conclusions may be supported by multiple claims.

## 5.3 Unsupported Statements
Statements lacking citations:

- Cannot form conclusions  
- Are excluded from exports  
- Must be flagged by validation rules

---

# 6. Confidence Assessment

## 6.1 Confidence Levels
Confidence reflects the quality and agreement of evidence.  
Standard levels include:

- **High** — multiple, consistent sources  
- **Moderate** — adequate evidence with minor gaps  
- **Low** — limited evidence or unresolved conflicts  
- **Speculative** — insufficient evidence; excluded from export  

## 6.2 Confidence Derivation
Confidence may be:

- Manually assigned, or  
- Automatically inferred from citation strength and claim agreement  

Confidence scores must be stored as part of the claim or conclusion record.

---

# 7. Conflict Handling

## 7.1 Conflict Types
Conflicts may include:

- Contradictory dates  
- Overlapping or impossible events  
- Multiple incompatible relationships  
- Conflicting identities or roles  

## 7.2 Recording Conflicts
All conflicts must be recorded in the reasoning layer and attached to the relevant claims.

## 7.3 Resolution
Resolutions occur when:

- A conclusion overrides one or more conflicting claims  
- A ProofStatement documents the reasoning behind the decision  

---

# 8. Validation Requirements

GXPS requires the following validations:

- Every claim must have at least one citation  
- Every conclusion must have a ProofStatement  
- Conflicting claims must be marked for review  
- Missing or outdated citations must be flagged  
- Speculative statements must be excluded from export  

Rules are detailed in the [validation rules](validation-rules.md#geneax-validation-rules).

---

# 9. Example Structure (JSON)

```json
{
  "claim_id": "c123",
  "subject": "person:42",
  "statement": "John Doe was born in 1842",
  "citations": ["ct1", "ct2"],
  "confidence": "moderate",
  "conclusion": "cn1",
  "proof": "ps1",
  "conflicts": [],
  "reviewed_by": "admin",
  "created_at": "2025-10-27T14:21:00Z",
  "updated_at": "2025-11-08T09:13:00Z"
}
```
---

# 10. Summary

- Claims represent asserted genealogical facts.  
- Conclusions represent evaluated interpretations based on claims.  
- ProofStatements provide the reasoning that justifies each conclusion.  
- Every claim must include one or more citations.  
- Every conclusion must include a ProofStatement.  
- All conflicts between claims must be recorded and resolvable.  
- Speculative or unsupported statements must be excluded from export.  

This standard ensures that genealogical information in GeneaX remains accurate, transparent, and defensible.