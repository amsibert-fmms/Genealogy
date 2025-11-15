# 📡 GeneaX API Reference

This document outlines all public API endpoints for GeneaX.  
All responses are JSON. All endpoints require authentication unless noted.

---

## 👤 Person Endpoints

### `GET /api/person/`
Returns a list of people.

**Query Params**:
- `search`: Filter by name
- `gender`: Filter by gender
- `book_ref`: Filter by cross-referenced book ID

**Response**:
```json
{
  "count": 125,
  "results": [
    {
      "id": "uuid",
      "full_name": "Mary E. Yoder",
      "gender": "female",
      "birth": "event-id",
      "death": "event-id",
      "book_ref": "JH12:1234"
    }
  ]
}
```
### POST /api/person/

Creates a new person.

Body:
```json
{
  "full_name": "John D. Miller",
  "gender": "male",
  "birth": "event-id",
  "book_ref": "JH12:5678"
}
```

🔗 Relationship Endpoints
GET /api/relationship/

Returns relationships between people.

Query Params:
-type
-person_id

Response:

[
  {
    "person1": "uuid-a",
    "person2": "uuid-b",
    "type": "Spouse",
    "event": "event-id"
  }
]

POST /api/relationship/
{
  "person1": "uuid-a",
  "person2": "uuid-b",
  "type": "ParentChild"
}

🗓️ Event Endpoints
GET /api/event/

Fetches recorded events.

Response:

{
  "type": "Marriage",
  "date": "1885-06-10",
  "place": "place-id",
  "description": "Marriage of Eli Z. and Fannie M."
}

POST /api/event/
{
  "type": "LandSale",
  "date": "1860-11-12",
  "place": "place-id",
  "description": "Sold property to Jacob E."
}

📚 Source Endpoints
GET /api/source/
{
  "source_key": "JH12",
  "title": "Descendants of John Hochstetler",
  "author": "A. Hochstetler"
}

🧠 ProofStatement Endpoints
GET /api/proofstatement/
{
  "subject": "person-id",
  "claim": "Jacob is the son of John.",
  "confidence_level": "probable"
}

POST /api/proofstatement/
{
  "subject": "person-id",
  "claim": "Barbara was the daughter of Eli.",
  "analysis": "She appears in the 1900 census in his household.",
  "confidence_level": "possible"
}

📥 Import Endpoint
POST /api/import/

Upload a GEDCOM X JSON-LD file.

Request: multipart/form-data

Response:

{
  "status": "success",
  "imported_records": 143
}

📤 Export Endpoint
GET /api/export/?format=gedcomx

Returns downloadable GEDCOM X or GeneaX JSON export.

Response:

{
  "download_url": "/exports/geneax-2025-11-15.json"
}

🧾 Notes

All endpoints assume application/json.

Use Authorization: Token <your_token> for authenticated access.

Errors follow standard DRF error structure.

“If it has an endpoint, someone will try to break it. Be ready.”
