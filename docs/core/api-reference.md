# GeneaX API Reference {#geneax-api-reference}
_Last updated: 2025-11-15_

Related references: [Documentation home](../index.md#geneax-docs-home) · [Master outline](../master-outline.md#master-outline)

This document describes the public API for GeneaX.  
Each endpoint corresponds to a **Tier 3 Implementation Model** and maps to the domain areas defined in the [master outline](../master-outline.md#master-outline).

All responses are JSON.  
Authentication is required unless otherwise noted.

For conceptual and logical definitions, see:
- [Master outline](../master-outline.md#master-outline)
- [Data models](data-models.md#geneax-data-models)

---

# 0. Schema Conventions

All resources follow these API conventions:

- `id` is an integer primary key.
- `created_at` and `updated_at` use ISO 8601 timestamps.
- Related objects are referenced by numeric IDs unless expanded.
- Errors follow Django REST Framework's JSON error structure.
- Date values must use `YYYY-MM-DD` format when applicable.
- Pagination format will follow DRF defaults (to be documented when implemented).
- All POST and PATCH bodies must be JSON.

---

# 1. Overview

The GeneaX API provides access to core genealogical data models:

- Persons  
- Events  
- Relationships  
- Sources  
- Citations  
- Claims  
- Conclusions  
- ProofStatements  
- CrossReferences & FamilyAppearances  

Endpoints follow Django REST Framework conventions.

The API is organized according to the conceptual chapters in the [master outline](../master-outline.md#master-outline):

- Chapter 1 — Person  
- Chapter 2 — Event  
- Chapter 3 — Relationship  
- Chapter 4 — Sources & Citations  
- Chapter 5 — Claims, Conclusions, Proof  
- Chapter 6 — Numbering & Cross-References  

---

## 1.1 Query Parameters

Most list endpoints will support search and filtering as the implementation matures.  
Planned filters include:

- Name or text search  
- Event type  
- Date range (before/after)  
- Participant role  
- Citation-based filtering  
- Cross-reference filtering  

Filtering behavior will be documented as features are added.

---

# 2. Authentication

All GeneaX API endpoints require authentication unless otherwise stated.

GeneaX uses token-based authentication.

### 2.1 Required Headers

Requests must include:

Authorization: Token <your_token>
Content-Type: application/json
Accept: application/json

### 2.2 Authentication Method

GeneaX uses token-based authentication provided through Django REST Framework.

Clients must submit a valid token with every request:

Authorization: Token 123456abcde


### 2.3 Obtaining a Token

Token creation depends on deployment configuration.  
Tokens may be generated via:

- Django admin  
- A token-generation endpoint (if implemented)  
- Management command  

See the [configuration reference](../developer/configuration.md#geneax-configuration).


### 2.4 Unauthenticated Endpoints

Future versions may include unauthenticated endpoints for:

- Health checks  
- Basic metadata  

All genealogical endpoints require authentication.

---

# 3. Person Endpoints (Chapter 1)

### GET /api/person/
Returns a list of Person objects.

### GET /api/person/<id>/
Returns a single Person.

### POST /api/person/
Creates a Person.
Body example:
{
"primary_name": "Jane Doe",
"gender": "female"
}

### PATCH /api/person/<id>/
Updates a Person.

### DELETE /api/person/<id>/
Deletes a Person.

---

# 4. Event Endpoints (Chapter 2)

### GET /api/event/
List Events.

### GET /api/event/<id>/
Retrieve an Event.

### POST /api/event/
Create an Event.

Body example:
{
"type": "birth",
"date": "1842-01-01",
"place": "Boston",
"participants": [
{"person": 42, "role": "principal"}
]
}

### PATCH /api/event/<id>/
Update an Event.

### DELETE /api/event/<id>/  *(optional, if implemented)*
Delete an Event.

---

# 5. Relationship Endpoints (Chapter 3)

### GET /api/relationship/
List Relationships.

### GET /api/relationship/<id>/
Retrieve a Relationship.

### POST /api/relationship/
Create a Relationship.

### PATCH /api/relationship/<id>/
Update a Relationship.

### DELETE /api/relationship/<id>/
Delete a Relationship.

---

# 6. Source Endpoints (Chapter 4)

### GET /api/source/
List Sources.

### GET /api/source/<id>/
Retrieve a Source.

### POST /api/source/
Create a Source.

### PATCH /api/source/<id>/
Update a Source.

### DELETE /api/source/<id>/
Delete a Source.

---

# 7. Citation Endpoints (Chapter 4)

### GET /api/citation/
List Citations.

### GET /api/citation/<id>/
Retrieve a Citation.

### POST /api/citation/
Create a Citation.

Body must follow the Citation Target Rules:
{
"source": 5,
"target_type": "person",
"target_id": 42,
"detail": "Page 12, Record 87"
}

### PATCH /api/citation/<id>/
Update a Citation.

### DELETE /api/citation/<id>/
Delete a Citation.

---

# 8. Claims, Conclusions, and Proof Endpoints (Chapter 5)

## Claim Endpoints

### GET /api/claim/
List Claims.

### POST /api/claim/
Create a Claim.

Claims must include at least one citation:
{
"statement": "John Smith was born in 1842",
"subject": 42,
"citations": [3, 4]
}

---

## Conclusion Endpoints

### GET /api/conclusion/
List Conclusions.

### POST /api/conclusion/
Create a Conclusion.

Conclusions must reference a ProofStatement:

{
"subject": 42,
"selected_claims": [12, 13],
"proofstatement": 7
}

---

## ProofStatement Endpoints

### GET /api/proof/
List ProofStatements.

### POST /api/proof/
Create a ProofStatement.

Body example:
{
"conclusion": 9,
"narrative": "After evaluating all available evidence...",
"referenced_claims": [12, 13]
}

---

# 9. Cross-Reference and FamilyAppearance (Chapter 6)

## CrossReference Endpoints

### GET /api/xref/
List CrossReferences.

### POST /api/xref/
Create a CrossReference.

---

## FamilyAppearance Endpoints

### GET /api/familyappearance/
List FamilyAppearances.

### POST /api/familyappearance/
Create a FamilyAppearance.

---

# 10. Export Endpoints

### GET /api/export/gedcomx/
Export data in GEDCOM X JSON-LD format.

Example response:
{
"download_url": "/exports/geneax-2025-11-15.json"
}

---

# 11. Notes

- All responses are JSON.
- Errors follow Django REST Framework format.
- Endpoints correspond to Tier 3 Implementation Models.
- See the [data models](data-models.md#geneax-data-models) for definitions of fields, constraints, and relationships.