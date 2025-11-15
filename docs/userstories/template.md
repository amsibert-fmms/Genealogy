# User Stories - Genealogy Application

## Document Information
**Version:** 1.0  
**Last Updated:** 2025-11-15  
**Status:** Draft

## Personas

### Primary Persona: Family Historian (Sarah)
- Age: 45-65
- Tech-savvy hobbyist
- Researching family history for 5+ years
- Has existing GEDCOM files from other software
- Values accuracy and source documentation
- Wants to share findings with family members

### Secondary Persona: Casual User (Mike)
- Age: 30-50
- Limited genealogy experience
- Wants to document living family members
- May expand to historical research later
- Prefers simple, intuitive interface

---

## Epic 1: Person Management

### US-001: Add a New Person
**As a** family historian  
**I want to** add a new person to the database  
**So that** I can record their biographical information

**Acceptance Criteria:**
- Can enter first name, middle name(s), last name, suffix
- Can enter birth date and place
- Can enter death date and place (if deceased)
- Can mark date fields as "exact", "approximate", or "before/after"
- Can enter additional biographical notes
- System validates required fields (at minimum: first name, last name)
- System generates unique identifier for person

**Priority:** High  
**Story Points:** 3

---

### US-002: Edit Person Information
**As a** family historian  
**I want to** update a person's information  
**So that** I can correct errors or add newly discovered facts

**Acceptance Criteria:**
- Can access edit form from person detail page
- All fields are editable
- System tracks change history (who/when)
- Can cancel without saving changes
- Validation same as create

**Priority:** High  
**Story Points:** 2

---

### US-003: Delete a Person
**As a** family historian  
**I want to** remove a person from the database  
**So that** I can eliminate duplicates or incorrect entries

**Acceptance Criteria:**
- Confirmation dialog warns about relationships that will be affected
- Soft delete option (mark as deleted but preserve data)
- Hard delete option (permanently remove)
- Cannot delete if person has descendants (must remove relationships first)
- Action is logged in audit trail

**Priority:** Medium  
**Story Points:** 3

---

### US-004: Search for a Person
**As a** family historian  
**I want to** search for people by various criteria  
**So that** I can quickly find individuals in a large database

**Acceptance Criteria:**
- Can search by name (partial matches supported)
- Can search by birth year range
- Can search by birth place
- Can filter by living/deceased status
- Results show key identifying info (name, birth/death dates)
- Can sort results by name, birth date, or relevance

**Priority:** High  
**Story Points:** 5

---

### US-005: View Person Details
**As a** family historian  
**I want to** view comprehensive information about a person  
**So that** I can see all recorded facts and relationships

**Acceptance Criteria:**
- Displays all biographical information
- Shows immediate family (parents, spouses, children)
- Shows attached media and documents
- Shows sources and citations
- Shows events timeline
- Provides navigation to related individuals
- Shows data quality indicators (missing info, conflicts)

**Priority:** High  
**Story Points:** 5

---

## Epic 2: Relationship Management

### US-006: Link Parent-Child Relationship
**As a** family historian  
**I want to** establish parent-child relationships  
**So that** I can build the family tree structure

**Acceptance Criteria:**
- Can add one or both parents to a person
- Can add multiple children to a parent
- System prevents impossible relationships (date logic, biological limits)
- Can specify relationship type (biological, adopted, foster, step)
- Can specify uncertainty level
- Warns about potential duplicates during linking

**Priority:** High  
**Story Points:** 5

---

### US-007: Link Spousal Relationship
**As a** family historian  
**I want to** record marriages and partnerships  
**So that** I can document family unions

**Acceptance Criteria:**
- Can add spouse/partner to a person
- Can record marriage date and place
- Can record divorce/separation date
- Can add multiple spouses (with date ranges)
- Can specify relationship type (married, domestic partnership, common-law)
- System validates date logic (marriage before children)

**Priority:** High  
**Story Points:** 5

---

### US-008: View Family Tree
**As a** family historian  
**I want to** visualize relationships in tree format  
**So that** I can see family structure at a glance

**Acceptance Criteria:**
- Displays ancestors (pedigree view)
- Displays descendants (family group view)
- Can toggle between view types
- Can expand/collapse branches
- Shows 4-5 generations by default
- Can click person to navigate to their detail page
- Handles complex relationships (multiple marriages, adoptions)

**Priority:** High  
**Story Points:** 8

---

## Epic 3: Media & Documentation

### US-009: Attach Photos
**As a** family historian  
**I want to** attach photographs to individuals  
**So that** I can preserve visual records

**Acceptance Criteria:**
- Can upload image files (JPG, PNG, GIF)
- Can add caption and date to photo
- Can tag multiple people in one photo
- Can set one photo as primary for person
- Generates thumbnails automatically
- Can view full-size image

**Priority:** Medium  
**Story Points:** 5

---

### US-010: Attach Documents
**As a** family historian  
**I want to** attach documents (birth certificates, census records)  
**So that** I can keep source material with relevant individuals

**Acceptance Criteria:**
- Can upload PDF, DOCX, TXT files
- Can add document type (birth cert, census, etc.)
- Can add description and date
- Can link document to multiple people
- Can view/download documents
- Shows document count on person detail page

**Priority:** Medium  
**Story Points:** 5

---

### US-011: Add Source Citations
**As a** family historian  
**I want to** record sources for information  
**So that** I can track evidence and maintain research standards

**Acceptance Criteria:**
- Can create source records (book, website, document, etc.)
- Can cite sources for specific facts
- Can add source notes and repository information
- Can rate source reliability
- Can view all citations for a person
- Can search/filter by source

**Priority:** Low  
**Story Points:** 8

---

## Epic 4: Data Import/Export

### US-012: Import GEDCOM File
**As a** family historian  
**I want to** import my existing GEDCOM file  
**So that** I can transfer data from other genealogy software

**Acceptance Criteria:**
- Can upload .ged file
- System validates GEDCOM format
- Shows preview of individuals to be imported
- Detects potential duplicates
- Allows merge or skip duplicates
- Imports individuals, relationships, events, notes
- Shows import summary report
- Can undo import if needed

**Priority:** High  
**Story Points:** 13

---

### US-013: Export GEDCOM File
**As a** family historian  
**I want to** export my data as GEDCOM  
**So that** I can backup or use in other software

**Acceptance Criteria:**
- Generates valid GEDCOM 5.5.1 format
- Can export entire database or selected individuals
- Can include/exclude living persons
- Can include/exclude media files
- Downloads as .ged file
- Includes all relationships and events

**Priority:** Medium  
**Story Points:** 8

---

## Epic 5: User Management & Privacy

### US-014: Register Account
**As a** new user  
**I want to** create an account  
**So that** I can start building my family tree

**Acceptance Criteria:**
- Can register with email and password
- Email verification required
- Password strength requirements enforced
- Creates default private tree
- Welcome email sent

**Priority:** High  
**Story Points:** 5

---

### US-015: Set Privacy Levels
**As a** family historian  
**I want to** control who can see information about living persons  
**So that** I can protect their privacy

**Acceptance Criteria:**
- Can mark individuals as "living" or "deceased"
- Living persons automatically private by default
- Can set privacy level: Public, Family, Private
- Can hide specific facts (keep person visible but hide details)
- Privacy settings enforced in all views and exports
- Warning shown when making living person public

**Priority:** High  
**Story Points:** 5

---

### US-016: Share Tree with Family
**As a** family historian  
**I want to** invite family members to view/edit my tree  
**So that** we can collaborate on research

**Acceptance Criteria:**
- Can send email invitation to family member
- Can set permission level (view-only, editor, admin)
- Invited user receives link to join
- Can revoke access at any time
- Shows list of collaborators
- Activity log shows who changed what

**Priority:** Medium  
**Story Points:** 8

---

## Epic 6: Research & Analysis

### US-017: View Timeline
**As a** family historian  
**I want to** see a chronological timeline of a person's life events  
**So that** I can understand their life story

**Acceptance Criteria:**
- Shows all events in chronological order
- Includes birth, death, marriages, children born
- Can add custom events (education, occupation, residence, military)
- Shows age at each event
- Visual timeline representation
- Can compare timelines of multiple people

**Priority:** Low  
**Story Points:** 5

---

### US-018: Calculate Relationships
**As a** family historian  
**I want to** determine the relationship between any two people  
**So that** I can understand how they're connected

**Acceptance Criteria:**
- Can select two people and see their relationship
- Calculates degree of cousin (1st, 2nd, 3rd, etc.)
- Shows "removed" generations correctly
- Shows direct relationships (grandparent, great-uncle, etc.)
- Shows the connecting path through the tree
- Handles complex cases (multiple paths, half-siblings)

**Priority:** Low  
**Story Points:** 13

---

### US-019: Generate Reports
**As a** family historian  
**I want to** create printable reports  
**So that** I can share research with non-technical family members

**Acceptance Criteria:**
- Can generate descendant report (all descendants of ancestor)
- Can generate ancestor report (pedigree chart)
- Can generate family group sheet
- Can export as PDF
- Can include/exclude photos
- Can customize which fields to include

**Priority:** Low  
**Story Points:** 8

---

## Epic 7: Data Quality

### US-020: Identify Duplicate Persons
**As a** family historian  
**I want to** find potential duplicate entries  
**So that** I can maintain data quality

**Acceptance Criteria:**
- System suggests potential duplicates based on name/dates
- Shows side-by-side comparison
- Can merge duplicates
- Can dismiss false positives
- Merge preserves all data from both records
- Merge creates audit trail

**Priority:** Medium  
**Story Points:** 13

---

### US-021: Validate Data Consistency
**As a** family historian  
**I want to** identify data inconsistencies  
**So that** I can correct errors

**Acceptance Criteria:**
- Flags impossible dates (born after death, parent born after child)
- Flags unusual age gaps (very old parent, very young parent)
- Flags missing critical information
- Shows data quality score for each person
- Provides suggestions for improvement
- Can filter to show only records with issues

**Priority:** Low  
**Story Points:** 8

---

## Future Considerations

### Potential Future Stories:
- DNA integration (connect with DNA test results)
- Historical records search integration
- Mobile app companion
- Mapping (show places on map)
- Social features (public trees, connection requests)
- Advanced charts (fan charts, hourglass charts)
- Translation support for international users
- AI-assisted record matching
- Headstone/cemetery database integration
- Living family member messaging

---

## Notes

### Story Point Scale:
- 1-2: Simple, well-understood tasks
- 3-5: Moderate complexity
- 8: Complex, requires significant effort
- 13: Very complex, consider breaking down

### Priority Definitions:
- **High**: Core functionality, needed for MVP
- **Medium**: Important but can be deferred
- **Low**: Nice to have, future enhancement