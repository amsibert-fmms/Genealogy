## ⚙️ `CONFIGURATION.md`

```markdown
# ⚙️ Configuration

GeneaX uses environment variables. You can define them in a `.env` file or export them directly.

## Required Variables

| Variable | Description |
|----------|-------------|
| `DJANGO_SECRET_KEY` | You know what this is. |
| `DATABASE_URL` | PostgreSQL URL (`postgres://user:pass@localhost:5432/db`) |
| `DEBUG` | `True` or `False` |
| `ALLOWED_HOSTS` | Comma-separated list |

## Example `.env`

```env
DJANGO_SECRET_KEY=shhh
DATABASE_URL=postgres://user:pass@localhost:5432/geneax_dev
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
“If everything breaks, check your .env. If it still breaks, blame Django.”
