# 🛠️ GeneaX Installation Guide

## Requirements
- Python 3.10+
- PostgreSQL
- Poetry or pip
- Git (for cloning your sins)

## Setup

```bash
git clone https://github.com/yourusername/geneax.git
cd geneax
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
Database
createdb geneax_dev
python manage.py migrate

Run It
python manage.py runserver


“If you hear your fan spinning loudly, you’ve done it wrong.”


---
