# GeneaX Configuration Reference {#geneax-configuration}
_Last updated: 2025-11-15_

Related references: [Developer hub](README.md#geneax-developer-hub) · [Documentation home](../index.md#geneax-docs-home)

GeneaX relies on environment variables to decouple secrets and deployment-specific settings from the codebase. Define these
values in a `.env` file for local development and in your deployment platform's secret store for production.

## Required environment variables
| Variable | Description | Example |
| --- | --- | --- |
| `DJANGO_SECRET_KEY` | Secret key used for cryptographic signing. | `django-insecure-<generated>` |
| `DATABASE_URL` | Connection string for PostgreSQL. | `postgres://user:pass@localhost:5432/geneax_dev` |
| `DEBUG` | Enables Django debug mode. Use `False` in production. | `True` |
| `ALLOWED_HOSTS` | Comma-separated list of hostnames. | `localhost,127.0.0.1` |

## Optional environment variables
| Variable | Purpose |
| --- | --- |
| `EMAIL_URL` | SMTP connection string for outbound mail. |
| `REDIS_URL` | Enables caching and background jobs when Redis is provisioned. |
| `SENTRY_DSN` | Activates error monitoring in production. |

## Sample `.env`
```env
DJANGO_SECRET_KEY=django-insecure-change-me
DATABASE_URL=postgres://geneax:password@localhost:5432/geneax_dev
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
EMAIL_URL=smtp://apikey:secret@localhost:1025/
```
Store the `.env` file at the project root and ensure it is ignored by Git.

## Applying configuration
1. Copy `.env.example` (when available) to `.env` and edit values.
2. Export variables manually when running one-off commands:
   ```bash
   export DJANGO_SECRET_KEY=...
   export DATABASE_URL=...
   ```
3. Restart Django or the ASGI server after changing environment variables.

## Where settings live
- Django settings modules reside in `geneax/settings/`.
- Connection details flow into the ORM via `DATABASE_URL`.
- Third-party integrations should read from environment variables in the same style; document additions here as they are added.

See the [deployment playbook](deployment.md) for platform-specific examples and the [API reference](../core/api-reference.md) for
endpoints affected by configuration changes.
