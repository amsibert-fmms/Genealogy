# GeneaX - Genealogy Django Project

A single app Django project for learning Django and managing genealogy data.

## Project Structure

- **GeneaX**: Django project configuration
- **genealogy**: Main Django application for genealogy features
- **docs**: Documentation hub covering architecture, data models, and developer workflows

## Setup

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Run migrations:
   ```bash
   python manage.py migrate
   ```

3. Create a superuser (optional):
   ```bash
   python manage.py createsuperuser
   ```

4. Run the development server:
   ```bash
   python manage.py runserver
   ```

5. Access the application at http://127.0.0.1:8000/

## Documentation
- Start with the [docs index](docs/index.md) for a guided map of every reference.
- Read the [documentation overview](docs/README.md) for project goals and background.
- Follow the [developer hub](docs/developer/README.md) for installation, configuration, and deployment workflows.

## Requirements

- Python 3.8+
- Django 5.2+
