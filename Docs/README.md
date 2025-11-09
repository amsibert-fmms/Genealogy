# 🧬 GeneaX  
*A Django-based genealogy platform built for learning and strict GEDCOM X compliance.*

---

## Overview
**GeneaX** is a hands-on project for exploring full-stack web development with **Django**, focused on the complexities of **genealogical data modeling** and **proof validation**.  
Unlike typical hobby genealogy apps, GeneaX adheres closely to the **GEDCOM X standard**, ensuring structured, interoperable, and verifiable family history data.

It’s equal parts learning exercise, data standard experiment, and quiet rebellion against messy ancestry spreadsheets.

---

## Objectives
- Build a Django application that implements the GEDCOM X data model.  
- Support import/export of GEDCOM X JSON-LD data.  
- Integrate an internal **Proof Standard (GXPS)** for evaluating evidence and source quality.  
- Provide a flexible and customizable UI using Tailwind CSS.  
- Offer an API layer for integration with other genealogy tools.

---

## Key Features
- 📄 Documented **GEDCOM X compliance** for people, relationships, sources, and events.  
- 📄 Documented **Proof Statements** and confidence scoring for genealogical conclusions.  
- 🚧 **Import/export utilities** for GEDCOM X JSON-LD.  
- 🚧 **Family tree visualizations** with relationship graphs and maps.  
- 🚧 **Collaborative editing** with revision history and permissions.  
- 🚧 **Schema validation tools** for quality assurance.

---

## Tech Stack

| Layer | Technology |
|-------|-------------|
| **Backend** | Django (4.2+) |
| **API** | Django REST Framework |
| **Database** | PostgreSQL (with JSON fields) |
| **Frontend** | Tailwind CSS, HTMX (optional React layer later) |
| **Validation** | jsonschema |
| **Testing** | pytest |

---

## Installation

```bash
# Clone the repo
git clone https://github.com/yourusername/geneax.git
cd geneax

# Set up environment
python -m venv .venv
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run migrations
python manage.py migrate

# Start dev server
python manage.py runserver
