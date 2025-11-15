# GeneaX Security Policy {#geneax-security}
_Last updated: 2025-11-15_

Related references: [Documentation home](index.md#geneax-docs-home) · [Deployment playbook](developer/deployment.md#geneax-deployment)

GeneaX processes personally identifiable information about living and historical individuals. Protecting that data and the
infrastructure that stores it is essential. This policy describes how to report vulnerabilities and the expectations applied to
contributors.

## Reporting a vulnerability
- Email the security contact at `your.email@example.com` with clear reproduction steps.
- Use an encrypted channel whenever possible; request a PGP key in your first message if needed.
- Do not create public issues for undisclosed vulnerabilities.

## In-scope data
GeneaX manages:
- Personally identified ancestors and living relatives.
- Public and private family tree data.
- Historical documents that may include PII.

## Security expectations
- Always use HTTPS in production environments.
- Sanitize and validate every input path—consult the [validation rules](core/validation-rules.md).
- Review external data sources before import and map them through the [GEDCOM X compliance](core/gedcomx-compliance.md)
  guidelines.
- Follow the [deployment checklist](developer/deployment.md) to keep infrastructure hardened.

> "Ancestry may be public, but data leaks shouldn't be."
