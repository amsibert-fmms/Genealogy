# GeneaX Deployment Playbook {#geneax-deployment}
_Last updated: 2025-11-15_

Related references: [Developer hub](README.md#geneax-developer-hub) · [Documentation home](../index.md#geneax-docs-home)

This playbook outlines the steps required to deploy GeneaX to staging or production. Adapt the infrastructure commands to suit
your hosting platform while keeping the guardrails below in place.

## 1. Pre-deployment checklist
- [ ] All tests pass (`pytest`).
- [ ] Static assets are built if the frontend changes (`npm run build` when applicable).
- [ ] Database migrations have been generated and reviewed.
- [ ] The [changelog](changelog.md) reflects user-facing updates.
- [ ] Security-impacting changes are reviewed against the [security policy](../security.md).

## 2. Environment preparation
- Confirm environment variables match the [configuration reference](configuration.md).
- Ensure HTTPS termination is configured (proxy, load balancer, or platform service).
- Provision PostgreSQL with automated backups.
- (Optional) Configure Redis for caching or background tasks.

## 3. Deployment commands
Below is a reference flow for a container-based deployment:
```bash
# Build the image
docker build -t registry.example.com/geneax:<version> .

# Run database migrations
docker run --rm \
  --env-file .env.production \
  registry.example.com/geneax:<version> \
  python manage.py migrate

# Launch the application (example using docker-compose)
docker compose -f deploy/docker-compose.yml up -d
```
Adjust the path to match your deployment configuration files.

## 4. Post-deployment verification
1. Run health checks: `curl https://your-domain.example.com/health/`.
2. Validate database migrations by spot-checking key entities (Persons, Events) via the admin.
3. Execute smoke tests or critical API calls from the [API reference](../core/api-reference.md).
4. Monitor logs for errors during the first hour after release.

## 5. Rollback strategy
- Maintain tagged container images or release branches for quick rollback.
- Keep a recent database snapshot and document restore procedures.
- If a release fails, communicate status in the project channels and update the [changelog](changelog.md) with remediation notes.

For platform-specific automation (GitHub Actions, Heroku, etc.), add a subsection here and link it from the [documentation home](../index.md#geneax-docs-home) once implemented.
