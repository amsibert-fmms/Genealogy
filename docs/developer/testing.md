# Testing GeneaX {#geneax-testing}
_Last updated: 2025-11-15_

Related references: [Developer hub](README.md#geneax-developer-hub) · [Documentation home](../index.md#geneax-docs-home)

Quality checks keep the genealogical data model trustworthy. This guide explains the testing stack and how to run it locally and
in CI.

## 1. Tooling
| Purpose | Tool |
| --- | --- |
| Test runner | `pytest` with `pytest-django` |
| Factories | `factory_boy` |
| Schema validation | `jsonschema` for GEDCOM X payloads |
| Linting (optional) | `black`, `isort`, `flake8`, `mypy` |

Install optional lint tools via `pip install -r requirements-dev.txt` when the file is introduced.

## 2. Running the suite
```bash
# Ensure the virtual environment is active
source .venv/bin/activate

# Run tests
pytest
```

Use `pytest -k <keyword>` to filter specific tests and `pytest --maxfail=1` to stop on first failure during rapid iteration.

## 3. Fixtures
The `fixtures/` directory will contain:
- GEDCOM X sample payloads (valid and invalid).
- ProofStatement examples for reasoning workflows.
- Relationship edge cases for validation.

Add new fixtures when covering regression bugs or new GEDCOM X features. Document additions in the [changelog](changelog.md).

## 4. Continuous integration
- Configure CI to run `pytest` on every pull request.
- Add linting steps (black, isort, mypy) as they become available.
- Publish coverage metrics when the suite stabilises.

## 5. Troubleshooting
- If migrations fail during tests, run `python manage.py migrate --check` locally.
- For database-related flakes, ensure PostgreSQL is running and matches `DATABASE_URL`.
- When schema validation fails, review the [validation rules](../core/validation-rules.md#geneax-validation-rules) and [GEDCOM X mappings](../core/gedcomx-compliance.md#geneax-gedcomx).
