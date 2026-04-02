<!--
---
title: "Phase 01: Ideation and Setup"
description: "Architecture validation, repository scaffolding, and documentation"
author: "VintageDon"
date: "2026-03-21"
version: "1.0"
status: "Complete"
tags:
  - type: worklog
  - category: architecture
related_documents:
  - "[Spec Directory](../../spec/README.md)"
  - "[Project README](../../README.md)"
---
-->

# Phase 01: Ideation and Setup

## Summary

| Attribute | Value |
|-----------|-------|
| Status | ✅ Complete |
| Duration | 2026-03-21 (single intensive day) |
| Sessions | 6 (across multiple Claude and Gemini instances) |
| Artifacts | 6 spec documents, 4 GDR research outputs, 10 documentation templates, full repo scaffolding |

**Objective:** Validate the architecture for an ITIL-driven autonomous DevOps team, establish the repository, and produce implementation-ready specifications.

**Outcome:** Architecture validated through four Gemini Deep Research iterations and multiple extended design sessions. Repository scaffolded with documentation standards, public README, and a comprehensive private spec directory containing the full system design. Project is ready for implementation work to begin.

---

## 1. Contents

```
01-ideation-and-setup/
└── README.md               # This file (synthesis document)
```

Supporting artifacts live in their permanent locations:
- `spec/` — Architecture specifications (6 documents + human interaction surfaces subdirectory)
- `internal-files/` — GDR research outputs (4 documents)
- `docs/documentation-standards/` — Templates and standards (10 files)
- Root-level files — README.md, AGENTS.md, CONTRIBUTING.md, SECURITY.md, CODE_OF_CONDUCT.md

---

## 2. Key Decisions

### Architecture

| Decision | Rationale |
|----------|-----------|
| ITIL ticket-driven coordination over agent-to-agent communication | Produces audit trails, SLA metrics, and change records as byproducts. Aligns with established IT governance frameworks. |
| Ephemeral agents over persistent daemons | Clean context per invocation, no state accumulation, minimal resource consumption. Only the SDM orchestrator is persistent. |
| iTop as ITSM backbone | Open-source community edition with full ITIL processes, REST API, CMDB, webhooks, SLA calculation, and data sync collectors. Zero licensing cost. |
| Interface abstraction (7+1 contracts) | Every input behind an abstract protocol. Makes the system portable to any operational stack. Also the core commercial differentiator. |
| Agent personas as ITIL roles | Agents are employees with job titles, RBAC, and audit trails — not tools with capabilities. Six defined personas with least-privilege access. |
| Neo4j knowledge graph for topology | Graph traversal replaces LLM inference for RCA and impact assessment where the graph is current. Reduces hallucination surface in dependency reasoning. |
| CIS v8 hardening + NIST AI RMF governance | CIS v8 IG1 as security baseline, NIST AI RMF for AI system governance, CIS-RAM for risk methodology, Duty of Care as the "why." Compliance evidence as a byproduct of operations. |
| MkDocs + git for KB over wiki platforms | Agent-writable via PR API, human-readable via static site. No wiki overhead. Frontmatter tags enable structured retrieval. |

### Project Organization

| Decision | Rationale |
|----------|-----------|
| Three-tier content model (public / IP / ephemeral) | Public layer demonstrates expertise, IP layer holds the architecture, ephemeral layer is working space. |
| No GitHub Issues/Projects | Too much ceremony for a highly iterative pre-implementation phase. iTop will own project tracking once deployed. |
| Spec directory as primary IP container | All architecture documents gitignored, with interior README providing reading order and relationship map. |
| Commercial content in dedicated document | Extracted from engineering specs into `commercial-positioning.md` to avoid diluting either the engineering argument or the market argument. |
| Work-logs as due diligence material | Demonstrates methodical execution to evaluators, not public consumption. |

### Tooling

| Decision | Rationale |
|----------|-----------|
| Greptile for AI code review | SOC 2 compliant, no training on customer code, scans AGENTS.md for context. $30/month. |
| LiteLLM/Olla for GPU queue | Priority proxy in front of Ollama is a solved problem. Not custom development. |
| CISO Assistant for GRC | 100+ frameworks, API-first, Docker deployment, cross-framework mapping engine. Selected over OpenGRC (license issues) and Eramba (too heavy). |
| PostgreSQL SKIP LOCKED for task queue | Already running, transactional, concurrent queue management. RabbitMQ reserved for real-time event routing only. |

---

## 3. Research Iterations

| Round | Model | Focus | Key Contribution | Limitations Identified |
|-------|-------|-------|-------------------|----------------------|
| GDR #1 | Gemini | Multi-agent landscape survey | Framework landscape mapping, ephemeral agent pattern validation | Overclaimed novelty, wrong infrastructure topology |
| GDR #2 | Gemini | Scientific operations architecture | PostgreSQL over RabbitMQ for state, honest GPU queue design | Still assumed wrong topology (all services on ML01) |
| GDR #3 | Gemini | ITIL-driven IT operations | iTop as backbone, two-team model, ITIL workflow mapping, collector discovery | Over-engineered GPU queue (custom proxy vs LiteLLM) |
| GDR #4 | Gemini | Pending — Ops/Research team split | Not yet executed | — |
| RAV sessions | Claude (Opus) | Interface abstraction, personas, KB, compliance, commercial positioning | Produced all spec documents from architectural insights | — |

Each GDR iteration corrected the previous one's assumptions. The RAV sessions produced the refined specifications from the validated research.

---

## 4. Artifacts Produced

### Spec Documents (gitignored)

| Document | Description |
|----------|-------------|
| `spec/README.md` | Interior README — reading order, relationship map, evolution narrative |
| `spec/autonomous-devops-team-one-pager.md` | Anchor architecture document (v1.2) |
| `spec/interface-abstraction-strategy.md` | Seven interface contracts with abstract protocols |
| `spec/agent-persona-registry.md` | Six agent personas with RBAC, workflows, tamper-evident action log |
| `spec/layered-infrastructure-knowledge-graph.md` | Neo4j topology graph (eighth interface) |
| `spec/commercial-positioning.md` | Market analysis, ServiceNow comparison, packaging models |
| `spec/ai-governance-integration.md` | AI governance framework integration — Pacific AI, NIST AI RMF, CIS-RAM, trustworthiness mapping, lifecycle checkpoints |
| `spec/human-interaction-surfaces/` | Five operator-facing surfaces (KB, observability, GRC, dispatch, research) |

### Research Inputs (gitignored)

| Document | Description |
|----------|-------------|
| `internal-files/gdr01-python-agentic-framework-blueprint.md` | GDR #1 output |
| `internal-files/gdr02-scientific-operations-agent-system-architecture.md` | GDR #2 output |
| `internal-files/gdr03-it-ops-autonomous-infrastructure-operations.md` | GDR #3 output |
| `internal-files/gdr04-it-agents-for-scientific-computing.md` | GDR #4 output |
| `internal-files/review-gpt-codex-architectural-2026-03-21.md` | GPT Codex architectural review — two-pass (commercial framing, then corrected internal ops framing) |

### Public Documentation (pushed)

| Document | Description |
|----------|-------------|
| `README.md` | Public portfolio README with architecture overview, Mermaid diagram, design decisions |
| `AGENTS.md` | Agent context loading and architectural constraints (also consumed by Greptile) |
| `CONTRIBUTING.md` | Contribution guidelines tailored to ethops |
| `SECURITY.md` | Security policy |
| `docs/data-science-infrastructure.md` | Cluster topology and connection reference |
| `docs/documentation-standards/` | 10 template files (frontmatter, READMEs, script headers, commenting, worklogs) |

---

## 5. Next Phase

**Handoff:** Architecture is validated and documented. Repository is scaffolded. The system is ready for implementation work to begin.

**Next steps (not yet sequenced into a formal milestone):**

1. Run GDR #4a (Ops team) and #4b (Research/Dev team) for remaining research
2. Multi-model review of spec documents (Gemini/GPT for independent architectural critique)
3. Provision iTop VM on cluster, initial configuration and CMDB population
4. First implementation code — orchestrator skeleton or ethops-kb, depending on priority assessment

---

| | |
|---|---|
| Author | VintageDon + Claude (Opus) |
| Created | 2026-03-21 |
| Version | 1.0 |
| Status | Complete |
