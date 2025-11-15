# Contributing to GeneaX {#geneax-contributing}
_Last updated: 2025-11-15_

Related references: [Developer hub](README.md#geneax-developer-hub) · [Documentation home](../index.md#geneax-docs-home)

Thank you for helping GeneaX grow. This guide documents the contribution workflow so changes remain consistent, well tested, and
easier to review.

## Before you start
1. Review the [roadmap](../core/roadmap.md) to confirm priority.
2. Discuss substantial changes in an issue or discussion thread.
3. Ensure your local environment matches the [installation](installation.md) and [configuration](configuration.md) guides.

## Branching strategy
- Use short-lived feature branches: `feature/<yourname>/<summary>`.
- For bug fixes, prefer `bugfix/<yourname>/<issue-number>`.
- Keep branches focused on a single change set.

## Coding standards
- Format Python code with `black` and run `isort` when touching imports.
- Include type hints where practical; run `mypy` if optional tooling is configured.
- Follow Django best practices for migrations and model changes.
- Update or add tests in line with the [testing guide](testing.md).

## Commit and review process
1. Run the full test suite: `pytest`.
2. Document user-facing changes in the [changelog](changelog.md).
3. Open a pull request that includes:
   - A clear, action-oriented title.
   - A summary of changes and rationale.
   - Links to relevant issues or documentation sections.
4. Request review from at least one maintainer.
5. Address feedback promptly; squash commits if asked to keep history clean.

## Documentation expectations
- Update relevant guides in `docs/` when behaviour or workflows change.
- Cross-link new content from the [documentation home](../index.md#geneax-docs-home) when appropriate.
- Ensure examples use current environment variables and command syntax.

Questions? Mention the maintainers in your issue or pull request, and include links back to the sections above for context.
