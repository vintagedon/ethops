# Work Logs

Development history for the ethops project. Each milestone gets a subfolder with a README synthesizing the decisions made, outcomes achieved, and artifacts produced during that phase.

**Access:** This directory is gitignored. Contents document the execution methodology and decision-making process behind the architecture defined in `spec/`.

---

## Purpose

These logs serve two functions:

1. **Internal reference** — Capture what was decided and why, so future sessions (with any model or collaborator) can pick up context without re-deriving decisions.
2. **Execution evidence** — Demonstrate methodical project delivery: structured phases, clear decision rationale, traceable artifacts.

Worklogs are synthesis documents — outcomes and decisions, not session transcripts.

---

## Structure

```
work-logs/
├── 01-ideation-and-setup/      # M01: Architecture validation, repo scaffolding, documentation
├── [02-domain-specific]/       # Project-specific milestones (numbered as work proceeds)
└── README.md                   # This file
```

---

## Conventions

- Folder naming: `NN-phase-name` (zero-padded, hyphenated)
- Each folder contains a `README.md` documenting that phase
- Scripts, configs, and artifacts live alongside the README
- Use `docs/documentation-standards/worklog-readme-template.md` as the base template

---

## Milestone Planning

Ethops does not use GitHub Issues or Projects for tracking. Project management will move to iTop's project module once deployed. Until then, milestones are defined and tracked through these work-logs and direct collaboration sessions.

Planned milestone sequence (refined as work proceeds):

| Milestone | Phase | Status |
|-----------|-------|--------|
| 01 | Ideation and Setup | ✅ Complete |
| 02 | iTop Deployment and CMDB Population | ⬜ Planned |
| 03 | Orchestrator Skeleton and First Agent | ⬜ Planned |
| 04 | ethops-kb and Compliance Baseline | ⬜ Planned |
| 05+ | To be defined as earlier milestones complete | — |

---

## Related

| Location | Contents |
|----------|----------|
| `spec/` | Architecture specifications — what is being built and why |
| `spec/README.md` | Reading guide for the spec documents |
| `internal-files/` | GDR research outputs that informed the architecture |
| `docs/documentation-standards/milestones-one-and-two-procedures.md` | General M01/M02 methodology template |
