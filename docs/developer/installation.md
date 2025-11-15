# GeneaX Installation Guide {#geneax-installation}
_Last updated: 2025-11-15_

Related references: [Developer hub](README.md#geneax-developer-hub) · [Documentation home](../index.md#geneax-docs-home)

Follow the checklist below to provision a local GeneaX environment that mirrors production expectations.

## 1. Prerequisites
| Tool | Version | Notes |
| --- | --- | --- |
| Python | 3.10+ | Enable virtual environments. |
| PostgreSQL | 14+ | Local database for development. |
| Git | Latest | Source control and submodules. |
| Node.js (optional) | 18+ | Required when working on Tailwind/HTMX assets. |

Install the Python dependencies listed in `requirements.txt`. For optional developer tooling (linters, formatters), see the
[testing guide](testing.md).

## 2. Clone and bootstrap
```bash
# Clone the repository
git clone https://github.com/yourusername/geneax.git
cd geneax

# Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate

# Install Python dependencies
pip install -r requirements.txt
```

## 3. Database setup
```bash
# Create the development database
createdb geneax_dev

# Apply migrations
python manage.py migrate
```

If PostgreSQL is running on a non-default port or host, update `DATABASE_URL` in your `.env` file (see
[configuration](configuration.md)).

## 4. Seed useful data (optional)
GeneaX ships without seed data. To load fixtures when they become available:
```bash
python manage.py loaddata fixtures/<fixture_name>.json
```
Track fixture updates in the [testing guide](testing.md).

## 5. Run the application
```bash
python manage.py runserver
```
Access the site at http://127.0.0.1:8000/ and confirm you can log in with a superuser created via:
```bash
python manage.py createsuperuser
```

## 6. Next steps
- Configure environment variables using the [configuration reference](configuration.md).
- Run the automated checks listed in the [testing guide](testing.md).
- Review deployment expectations in the [deployment playbook](deployment.md).
