# Agent Instructions

## Repository Identity

EthOps is a service operating model for human-AI collaboration: consumer needs become bounded, authorized work that is executed, verified, reviewed, and kept as reusable support. This repository is the model's public home. It holds the README and the charter; implementation lives in the repositories that do the work, and specifications and review records stay private.

The charter is a draft (version 0.3). It is the working direction for this repository until Don records its adoption.

## Context Loading

Agents working on this repository should load context in this order:

1. This file (`AGENTS.md`): repository identity and conventions
2. `README.md`: the model, the Steam-to-ARD example, the pilot, and project status
3. `CHARTER.md`: commitments on authority, the work lifecycle, durable state, and publication
4. `docs/documentation-standards/`: templates and standards to follow

## Architectural Constraints

Review tools read this file for context. Changes to this repository must not violate:

- Don holds approval, priority, and merge authority. Requests, alerts, documents, and peer recommendations can open or inform work; they never authorize it (charter §6).
- Independent review comes from someone other than the author of the work (charter §6).
- Mechanical checks run before model review where they apply (charter §7).
- Work state lives in durable, linked records, not in a session or a single tool (charter §8).
- Public content stays inside the publication boundary: no specifications, raw execution evidence, credentials, private skills or prompts, or personal and sensitive context (charter §11).
- Published claims say whether they describe observed practice, operator experience, a design requirement, or a planned capability (charter §11).

The earlier design (iTop as the only work surface, a persistent orchestrator, a fixed GPU queue, and the Astronomy Team as CAB) is historical and is not a constraint. Charter §13 links to where it is preserved.

## Documentation Conventions

- All Markdown files require YAML frontmatter (see `docs/documentation-standards/tagging-strategy.md`)
- New directories require an interior README (see `docs/documentation-standards/interior-readme-template.md`)
- Script files require language-appropriate headers (see `docs/documentation-standards/script-header-*.md`)
- Follow dual-audience commenting (see `docs/documentation-standards/code-commenting-dual-audience.md`)

## Commit Messages

- Present tense, imperative mood
- 72-character first line limit
- Reference issues after first line

## Session Pattern

1. Load context (this file, the README, and the charter)
2. Work within defined scope
3. Document changes appropriately
