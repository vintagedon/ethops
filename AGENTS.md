# Agent Instructions

## Repository Identity

Ethops (ephemeral ops) is an ITIL-organized autonomous DevOps team framework for scientific computing infrastructure. Two agent teams (IT Ops and Research/Dev) share iTop as their work surface, coordinated by a persistent Service Delivery Manager orchestrator on the [Proxmox Astronomy Lab](https://github.com/vintagedon/proxmox-astronomy-lab) research cluster.

## Context Loading

Agents working on this repository should load context in this order:

1. This file (`AGENTS.md`) — Repository identity and conventions
2. `README.md` — Project overview and architecture
3. `docs/documentation-standards/` — Templates and standards to follow
4. `docs/data-science-infrastructure.md` — Cluster topology and connection details

## Architectural Constraints

Greptile and other review tools scan this file for context. Key constraints that must not be violated:

- Agents are ephemeral — no persistent daemon agents except the SDM orchestrator
- All agent work flows through iTop tickets — never agent-to-agent communication
- Mechanical validation first — yamllint → ansible-lint → OPA/Rego conftest runs before any LLM review
- GPU queue priority — IT Ops inference > RAG embedding > Research tasks
- PostgreSQL SKIP LOCKED for task queue coordination, not RabbitMQ
- iTop is the backbone — ITSM, CMDB, change management, and shared work surface
- Astronomy Team is CAB — normal and emergency changes require human approval

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

1. Load context (this file + README)
2. Work within defined scope
3. Document changes appropriately