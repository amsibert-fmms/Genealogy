# 🧱 GeneaX Data Models

## Overview
The **GeneaX** data model is built on **Django ORM** principles and designed for **GEDCOM X compatibility**.  
Each entity maps closely to GEDCOM X core types, with several **GeneaX-specific extensions** to support community genealogy books, cross-referencing, and proof tracking.

*This document describes how we intend to make data behave — someday.*

---

## 🧩 Core GEDCOM X Entities

### **Person**
Represents an individual human being (alive, deceased, or theoretical ancestor).

```python
class Person(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    full_name = models.CharField(max_length=255)
    gender = models.CharField(max_length=20, blank=True)
    birth = models.ForeignKey("Event", null=True, blank=True, on_delete=models.SET_NULL, related_name="birth_of")
    death = models.ForeignKey("Event", null=True, blank=True, on_delete=models.SET_NULL, related_name="death_of")
    source = models.ForeignKey("SourceDescription", on_delete=models.SET_NULL, null=True, blank=True)
    book_ref = models.CharField(max_length=50, blank=True)  # e.g. "JH12:1234"
    notes = models.TextField(blank=True)
```

---

### **Relationship**
Defines a genealogical or social link between two people.

```python
class Relationship(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    person1 = models.ForeignKey("Person", on_delete=models.CASCADE, related_name="relationships_from")
    person2 = models.ForeignKey("Person", on_delete=models.CASCADE, related_name="relationships_to")
    type = models.CharField(max_length=80)
    event = models.ForeignKey("Event", on_delete=models.SET_NULL, null=True, blank=True)
    source = models.ForeignKey("SourceDescription", on_delete=models.SET_NULL, null=True, blank=True)
    proof = models.ForeignKey("ProofStatement", on_delete=models.SET_NULL, null=True, blank=True)
    notes = models.TextField(blank=True)
```

Supported types include:
- ParentChild
- Spouse
- OfficiantPerformer
- PropertySeller
- PropertyBuyer
- Witness
  
📎 *All types map to GEDCOM X URIs; custom ones use the GeneaX namespace.*

---

### **Event**
Captures a verifiable occurrence (birth, death, marriage, land sale, etc.).

```python
class Event(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    type = models.CharField(max_length=50)
    date = models.DateField(null=True, blank=True)
    place = models.ForeignKey("PlaceDescription", null=True, blank=True, on_delete=models.SET_NULL)
    description = models.TextField(blank=True)
    source = models.ForeignKey("SourceDescription", on_delete=models.SET_NULL, null=True, blank=True)
```

---

### **SourceDescription**
Represents a publication or document used as a genealogical source.

```python
class SourceDescription(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    source_key = models.CharField(max_length=20, unique=True)  # e.g. "JH12"
    title = models.CharField(max_length=255)
    author = models.CharField(max_length=255, blank=True)
    publication_date = models.DateField(null=True, blank=True)
    publisher = models.CharField(max_length=255, blank=True)
    notes = models.TextField(blank=True)
```

### **ProofStatement**
Implements the GeneaX Proof Standard (GXPS).

```python
class ProofStatement(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    subject = models.ForeignKey("Person", on_delete=models.CASCADE)
    claim = models.TextField()
    analysis = models.TextField()
    confidence_level = models.CharField(
        max_length=12,
        choices=[
            ("certain", "Certain"),
            ("probable", "Probable"),
            ("possible", "Possible"),
            ("speculative", "Speculative"),
        ],
    )
    sources = models.ManyToManyField("SourceDescription")
    conflicts = models.JSONField(default=list, blank=True)
    reviewed_by = models.ForeignKey("auth.User", null=True, blank=True, on_delete=models.SET_NULL)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

---

## 🧬 GeneaX Extensions
### **CrossReference**
Connects a GeneaX entity to a community genealogy book record.

```python
class CrossReference(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    composite_id = models.CharField(max_length=50, unique=True)  # e.g. "JH12:1234"
    source = models.ForeignKey("SourceDescription", on_delete=models.CASCADE)
    target_id = models.UUIDField()  # UUID of the related entity
    record_type = models.CharField(max_length=50)  # "Person", "Family", "Event"
    position = models.CharField(max_length=20, blank=True)  # child, spouse, inlaw, etc.
    references = models.ManyToManyField("self", symmetrical=False, blank=True)
    notes = models.TextField(blank=True)
```
🧠 *Allows mapping across multiple publications, e.g., JH12 ↔ DH78.*

---

### **FamilyAppearance**
Represents how a person appears in a particular family entry within a publication.

```python
class FamilyAppearance(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    person = models.ForeignKey("Person", on_delete=models.CASCADE, related_name="appearances")
    source = models.ForeignKey("SourceDescription", on_delete=models.CASCADE)
    family_id = models.CharField(max_length=50)  # e.g. "JH12:6789"
    position = models.CharField(max_length=20)
    cross_reference = models.ForeignKey("CrossReference", null=True, blank=True, on_delete=models.SET_NULL)
    notes = models.TextField(blank=True)
```
📖 *Captures cousin marriages, in-laws, and cross-linked spouse families without duplication.*

---

### **GeneratedConclusion**
Structured “written conclusion” derived from a ProofStatement.

```python
class GeneratedConclusion(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    statement = models.ForeignKey("ProofStatement", on_delete=models.CASCADE)
    summary = models.TextField()
    confidence_level = models.CharField(max_length=12)
    generated_at = models.DateTimeField(auto_now_add=True)
    context = models.JSONField(default=dict, blank=True)
```

---

## 🔗 Relationships Between Models
```plaintext
Person ─┬─< Relationship >─┬─ Person
        │
        ├─< FamilyAppearance >─ SourceDescription
        │
        ├─< CrossReference >─ SourceDescription
        │
        └─< ProofStatement >─ SourceDescription
```
This structure allows:
- Multiple books to describe the same person differently.
- Cross-linked families through shared identifiers.
- Full provenance tracking through source citations.

---

##🧠 Validation Rules
1. Every entity must link to at least one SourceDescription or ProofStatement.
1. CrossReference IDs (JH12:####) must be unique per source.
1. Circular FamilyAppearances (child ↔ spouse) allowed but logged.
1. GeneratedConclusion confidence must match its linked ProofStatement.
1. Exports omit speculative data unless explicitly requested.

---

##🧾 Implementation Status
|Model	|Status	|Notes|
|----|----|----------------|
|Person	|📄 Documented	|Basic schema defined, not yet implemented.|
|Relationship	|📄 Documented	|Supports extended types, pending validation logic.|
|Event	|📄 Documented	|Core structure aligned with GEDCOM X.|
|SourceDescription	|📄 Documented	|Acts as anchor for publications and book IDs.|
|ProofStatement	|📄 Documented	|GXPS schema finalized.|
|CrossReference	|📄 Documented	|Handles JH-style numbering systems.|
|FamilyAppearance	|📄 Documented	|Enables contextual placement within publications.|
|GeneratedConclusion	|📄 Documented	|Structure for future automation of narrative summaries.|

*“These models may not exist in the database yet,
but in the hearts of developers, they’re already normalized.”*
