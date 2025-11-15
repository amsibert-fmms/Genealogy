# GeneaX Documentation Home {#geneax-docs-home}
_Last updated: 2025-11-15_

Welcome to the GeneaX knowledge base. This hub gathers every document that explains how the project fits together—from domain
concepts and data models to day-to-day developer workflows. Use the sections below to jump directly to what you need, then use
the **Related references** tables to keep the big picture in view.

## Quick start for readers
- **New to the project?** Begin with the [documentation overview](README.md) for a narrative introduction and installation
  pointers.
- **Need the canonical structure?** Review the [master outline](master-outline.md#master-outline) to see how every chapter and tier connects.
- **Just want to build?** Head to the [developer guides](developer/README.md) and follow the installation checklist.

## Core knowledge base
| Topic | Description | Key cross-links |
| --- | --- | --- |
| [Architecture](core/architecture.md#geneax-architecture) | Django application structure, layers, and data flow. | [Master outline](master-outline.md#cross-document-map) · [Data models](core/data-models.md#geneax-data-models) |
| [Features](core/features.md#geneax-features) | What exists today and what is planned next. | [Roadmap](core/roadmap.md#geneax-roadmap) · [Proof standard](core/proof-standard.md#geneax-proof-standard) |
| [Roadmap](core/roadmap.md#geneax-roadmap) | Release priorities and sequencing. | [Features](core/features.md#geneax-features) · [Testing](developer/testing.md#geneax-testing) |
| [Data models](core/data-models.md#geneax-data-models) | Entity definitions organised by domain chapter. | [GEDCOM X compliance](core/gedcomx-compliance.md#geneax-gedcomx) · [Validation rules](core/validation-rules.md#geneax-validation-rules) |
| [GEDCOM X compliance](core/gedcomx-compliance.md#geneax-gedcomx) | Mapping between GeneaX and the GEDCOM X standard. | [Data models](core/data-models.md#geneax-data-models) · [API reference](core/api-reference.md#geneax-api-reference) |
| [Proof standard](core/proof-standard.md#geneax-proof-standard) | Genealogical reasoning, claims, and conclusions. | [Data models — Proof](core/data-models.md#proof-model) · [Validation rules](core/validation-rules.md#geneax-validation-rules) |
| [Validation rules](core/validation-rules.md#geneax-validation-rules) | Constraints that protect data integrity. | [Proof standard](core/proof-standard.md#geneax-proof-standard) · [Testing](developer/testing.md#geneax-testing) |
| [API reference](core/api-reference.md#geneax-api-reference) | REST endpoints, payloads, and workflows. | [Configuration](developer/configuration.md#geneax-configuration) · [Testing](developer/testing.md#geneax-testing) |

## Developer guides
| Topic | Description | Key cross-links |
| --- | --- | --- |
| [Developer landing page](developer/README.md#geneax-developer-hub) | Orientation for contributors and workflow overview. | [Installation](developer/installation.md#geneax-installation) · [Contributing](developer/contributing.md#geneax-contributing) |
| [Installation](developer/installation.md#geneax-installation) | Local environment setup and tooling. | [Configuration](developer/configuration.md#geneax-configuration) · [Testing](developer/testing.md#geneax-testing) |
| [Configuration](developer/configuration.md#geneax-configuration) | Environment variables and integration points. | [Deployment](developer/deployment.md#geneax-deployment) · [API reference](core/api-reference.md#geneax-api-reference) |
| [Deployment](developer/deployment.md#geneax-deployment) | Promotion strategy and operational expectations. | [Configuration](developer/configuration.md#geneax-configuration) · [Security policy](security.md#geneax-security) |
| [Testing](developer/testing.md#geneax-testing) | Automated and manual verification guidance. | [Validation rules](core/validation-rules.md#geneax-validation-rules) · [API reference](core/api-reference.md#geneax-api-reference) |
| [Contributing](developer/contributing.md#geneax-contributing) | Coding standards and collaboration guidelines. | [Testing](developer/testing.md#geneax-testing) · [Changelog](developer/changelog.md#geneax-changelog) |
| [Changelog](developer/changelog.md#geneax-changelog) | Release highlights and notable changes. | [Roadmap](core/roadmap.md#geneax-roadmap) |

## Meta & compliance
| Topic | Description |
| --- | --- |
| [Documentation overview](README.md) | Project story, goals, and onboarding narrative. |
| [Security policy](security.md) | Reporting process and data protection expectations. |
| [Repository README](../README.md) | Application setup instructions. |

---
Need another document? Use the chapter anchors in the [master outline](master-outline.md#master-outline) or search within the `docs/` folder.
