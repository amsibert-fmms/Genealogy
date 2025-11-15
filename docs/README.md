# GeneaX Documentation Overview {#geneax-docs-overview}
_Last updated: 2025-11-15_

Related references: [Documentation home](index.md#geneax-docs-home) · [Master outline](master-outline.md#master-outline) · [Developer hub](developer/README.md#geneax-developer-hub)

GeneaX is a Django-based platform for modelling, validating, and sharing genealogical research with GEDCOM X alignment. This
overview explains the purpose of the project, highlights core goals, and points you to deeper references throughout the
`docs/` tree.

## Project vision
GeneaX combines hands-on Django learning with rigorous genealogical standards:
- **GEDCOM X compliance** keeps exchanged data interoperable.
- **Proof-oriented workflows** help researchers connect evidence to conclusions.
- **Modular architecture** enables incremental delivery and experimentation.

For the canonical conceptual map, jump to the [master outline](master-outline.md#master-outline).

## Key objectives
| Objective | Supporting documents |
| --- | --- |
| Implement GEDCOM X-aligned data structures | [Data models](core/data-models.md), [GEDCOM X compliance](core/gedcomx-compliance.md) |
| Evaluate evidence with an internal proof standard | [Proof standard](core/proof-standard.md), [Validation rules](core/validation-rules.md) |
| Provide integrations through APIs | [API reference](core/api-reference.md), [Configuration](developer/configuration.md) |
| Offer a clear developer experience | [Developer hub](developer/README.md), [Installation](developer/installation.md) |

## Feature snapshot
- Documented GEDCOM X compliance for people, relationships, sources, and events.
- Documented proof statements and confidence scoring for genealogical conclusions.
- Planned import/export utilities for GEDCOM X JSON-LD.
- Planned visualisations (relationship graphs, timelines, and maps).
- Planned collaborative editing with permissions and revision history.
- Planned schema validation tooling for quality assurance.

Track delivery progress in the [features](core/features.md) and [roadmap](core/roadmap.md) documents.

## Technology stack
| Layer | Technology |
| --- | --- |
| Backend | Django 4.2+ |
| API | Django REST Framework |
| Database | PostgreSQL with JSON/JSONB fields |
| Frontend | Tailwind CSS, HTMX (React optional later) |
| Validation | jsonschema |
| Testing | pytest |

## Get started locally
Follow the [installation guide](developer/installation.md) and then run through the [testing guide](developer/testing.md) to
confirm your environment. The top-level [repository README](../README.md) contains quick-start commands.

## Community & collaboration
- Review the [contributing guide](developer/contributing.md) before opening pull requests.
- Log notable updates in the [changelog](developer/changelog.md).
- Escalate sensitive issues through the [security policy](security.md).

Questions or ideas? Start a discussion and link back to the relevant section above to ground the conversation.
