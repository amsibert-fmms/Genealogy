# GeneaX API Reference
This document provides the public API definitions for GeneaX.  
Each endpoint corresponds to **Tier 3 Implementation Models** and maps to the domain areas defined in `MASTER_OUTLINE.md`.

All responses are JSON.  
Authentication is required unless otherwise noted.

---

# 1. Overview

The GeneaX API provides access to core genealogical data structures including Persons, Events, Relationships, Sources, Citations, Claims, Conclusions, and ProofStatements.

All endpoints return JSON and follow Django REST Framework conventions.

The API is organized according to the conceptual chapters defined in `MASTER_OUTLINE.md`:

- Chapter 1 — Person
- Chapter 2 — Event
- Chapter 3 — Relationship
- Chapter 4 — Sources & Citations
- Chapter 5 — Claims, Conclusions, Proof
- Chapter 6 — Numbering & Cross-References

---

# 2. Authentication

All GeneaX API endpoints require authentication unless explicitly noted.
The system uses token-based authentication.

### 2.1 Required Headers

Requests must include the following headers:

Authorization: Token <your_token>
Content-Type: application/json
Accept: application/json

### 2.2 Authentication Method

GeneaX uses token-based authentication provided through Django REST Framework.

Clients must submit a valid token with every request:

Authorization: Token 123456abcde


### 2.3 Obtaining a Token

Token creation depends on deployment configuration.  
Tokens may be issued via:

- Django admin
- A token-generation endpoint (if implemented)
- A management command

See the setup instructions in `Developer_Docs/CONFIGURATION.md`.


### 2.4 Unauthenticated Endpoints

Most endpoints require authentication.  
Unauthenticated access may be provided in the future for system health checks or metadata endpoints.

---

# 3. Person Endpoints (Chapter 1)

### GET /api/person/
Returns a list of Person objects.

### GET /api/person/<id>/
Returns a single Person.

### POST /api/person/
Creates a Person.

### PATCH /api/person/<id>/
Updates a Person.

### DELETE /api/person/<id>/
Deletes a Person.

---

# 4. Event Endpoints (Chapter 2)

### GET /api/event/
Returns a list of Events.

### GET /api/event/<id>/
Returns a single Event.

### POST /api/event/
Creates an Event.

### PATCH /api/event/<id>/
Updates an Event.

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


## Conclusion Endpoints

### GET /api/conclusion/
List Conclusions.

### POST /api/conclusion/
Create a Conclusion.

## Proof Endpoints

### GET /api/proof/
List ProofStatements.

### POST /api/proof/
Create a ProofStatement.

---

# 9. Cross-Reference and FamilyAppearance (Chapter 6)

## CrossReference Endpoints

### GET /api/xref/
List CrossReferences.

### POST /api/xref/
Create a CrossReference.

## FamilyAppearance Endpoints

### GET /api/familyappearance/
List FamilyAppearances.

### POST /api/familyappearance/
Create a FamilyAppearance.

---

# 10. Export Endpoints

## GET /api/export/gedcomx/
Exports data in GEDCOM X JSON-LD format.

Response example:
{
  "download_url": "/exports/geneax-2025-11-15.json"
}

---

# 11. Notes

- All responses are JSON.
- Errors follow Django REST Framework error formats.
- Endpoint models correspond to the Tier 3 Implementation layer.
- The logical data model is defined in `DATA_MODELS.md`.
