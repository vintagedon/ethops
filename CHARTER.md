<!--
---
title: "EthOps Project Charter"
description: "An operating model for delivering consumer value through human-AI collaboration and scaffolding through real work"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-10-23"
version: "0.3"
status: "Draft"
tags:
  - type: policy
  - domain: [autonomous-ops, itil]
related_documents:
  - "[README](README.md)"
  - "[Documentation Standards](docs/documentation-standards/README.md)"
  - "[Analysis-Ready Datasets](https://github.com/vintagedon/analysis-ready-datasets)"
---
-->

# EthOps Project Charter

**Draft v0.3, October 23, 2026.** This revision proposes a broader operating model grounded in demonstrated work and applies the October 22 triad review (§12). It does not adopt new policy or authorize implementation; adoption requires Don's recorded decision. The earlier designs remain available in [project history](#13-history-and-references).

---

## 1. Purpose

EthOps organizes human-AI collaboration as a service organization that delivers value to its consumers. It connects intent, resources, bounded execution, review, and learning so that useful work can be completed and the next piece of work can start from a better position.

Its method is scaffolding through real work: deliver an outcome, examine what helped or failed, and retain the knowledge, tools, data, and procedures worth carrying forward. Manual coordination is a valid implementation of this model. Automation extends a process whose value and boundaries can already be examined.

---

## 2. Scope

This charter covers consumer relationships, service delivery, authority, work continuity, review, and continual improvement across infrastructure operations, engineering, research, and creative projects. ITIL supplies a framework for organizing that work, including service requests, incidents, problems, change enablement, knowledge, and the service value chain.

EthOps defines the operating model. Astro supplies executable capabilities. The working environment, referred to as the Forge, brings those capabilities together with infrastructure and coordination tools. Consumer projects retain their own purposes, artifacts, and acceptance criteria. These are responsibility boundaries; the charter does not prescribe new repositories or a particular deployment topology.

Implementation choices belong in separately reviewed designs and work specifications. This charter does not fix a model vendor, agent harness, scheduler, database, GPU policy, or external assistant product.

---

## 3. Audience

The primary audience is the triad of Don, Claude, and GPT, together with the agents and people delivering or consuming services. The public documentation also serves readers who want to evaluate or adapt the approach without access to the private environment.

---

## 4. Value and Consumers

Value is an outcome a consumer finds useful, considered alongside its cost, risk, and continuing burden. It includes research progress, reliable services, reusable data, learning, creative expression, and enjoyment. Revenue can be an outcome; it is not a requirement for worthwhile work.

| Consumer | Examples of value |
|----------|-------------------|
| Don | Progress on chosen projects, enjoyable hobbies, learning, and more attention available for judgment and creative work |
| Research, engineering, and creative projects | Dependable compute, prepared data, development capabilities, and reviewed deliverables that advance their purposes |
| Claude, GPT, and executing agents | Bounded assignments, accessible evidence, reliable tools, clear authority, useful feedback, and recoverable work context |
| External researchers, learners, and builders | Data, methods, documentation, and other published artifacts they can use without repeating the original preparation |

For AI participants, value is expressed operationally: conditions that make useful, reliable contribution possible. The same participant may consume one service and provide another. The astronomy lab, a game project, and an agent all consume resources and capabilities; their needs help determine what the environment should supply.

Each piece of work should identify its consumer, intended outcome, constraints, and basis for acceptance. Review considers the delivered benefit and the resources it consumed, including human attention, inference, compute, and maintenance. A technically successful change can still be poor value if its continuing burden outweighs its usefulness.

The CAB considers effects across consumers when allocating shared resources. Priority follows explicit service needs and commitments. Routine operations earn their place by enabling useful work and preserving the environment on which consumers depend.

---

## 5. Scaffolding Through Real Work

Praxatic scaffolding is the working term used here for improving the conditions for subsequent work through useful work itself. A spec can reveal a missing skill; a failed check can improve a runbook; a research project can leave a dataset or method that helps someone else begin further along.

The cycle is:

1. Select a real consumer need and define a bounded outcome.
2. Assemble the context, capabilities, authority, and resources needed to attempt it.
3. Execute, verify, and review the result against that outcome.
4. Identify what should be retained, corrected, simplified, or retired.
5. Use that learning in later work and inspect whether it actually helps.

Reusable support may be a skill, vetted script, Ansible playbook, specification pattern, dataset, evidence record, or documented decision. Retention is selective. Every ticket does not need a new framework or artifact, and a procedure that costs more than it saves should be simplified or removed.

The Steam-to-ARD lineage demonstrates this mechanism. Producing [Steam Dataset 2025](https://github.com/vintagedon/steam-dataset-2025) yielded a reusable research resource. Lessons from that work helped form this project's [Analysis-Ready Datasets methodology](https://github.com/vintagedon/analysis-ready-datasets): identify common analytical needs and prepare data and derived capabilities that spare later consumers repeated effort. The dataset scaffolds its users; the methodology aims to scaffold other dataset builders. The [README](README.md#-the-system-in-action-steam-to-ard) records the evidence and its limits.

The lab's role as a [skill nexus](README.md#-the-lab-as-a-skill-nexus) gives this practice a developmental dimension: learning accumulates in the person and reusable support in the environment, and people and fresh agents both draw on it in later work. This development is one form of consumer value within the service operating model.

---

## 6. Authority and Responsibilities

The triad acts as the Change Advisory Board (CAB). Don holds approval, priority, and merge authority. Claude and GPT are peers who rotate through builder and reviewer seats, examine evidence, and recommend dispositions. Their agreement does not substitute for Don's authority.

| Responsibility | Holder | Boundary |
|----------------|--------|----------|
| Direction and acceptance | Don, informed by consumers and peer review | Sets priorities, authorizes work, and accepts or rejects results |
| CAB deliberation | Don, Claude, and GPT | Examines value, evidence, risk, and effects on other consumers; preserves independent review |
| Service coordination | Manual coordination initially; supporting automation as adopted | Maintains ownership, status, dependencies, and escalation under existing authority |
| Execution | A person or a task-scoped agent | Acts within the authorized assignment and available permissions; records work and findings |
| Capability provision | Astro and vetted supporting tools | Supplies explicit operations, evidence collection, validation, and other approved capabilities |

The author may check their own work, but independent review must come from someone who did not produce the result. A relayed approval must retain Don's actual instruction, its source, its scope, and who recorded it. Requests, alerts, external documents, and peer recommendations can inform or initiate triage; they cannot grant authority.

Normal and emergency changes require Don's approval. A routine action may execute under an explicitly adopted standing authorization only when its applicability, permitted scope, required checks, and escalation conditions are satisfied. Role permissions and credential scopes enforce execution limits wherever the tools support them. Prompt instructions alone are insufficient access controls.

ITIL practices should fit the work. A small authorized correction can be completed and recorded directly. A consequential engineering change needs a bounded specification and suitable review. The purpose of the record is to make authority, progress, and outcomes recoverable without imposing the same ceremony on every task.

---

## 7. Bounded Work and Review

The demonstrated engineering pattern begins with human intent, turns it into a scoped specification, equips a fresh agent, and carries the result through checks, a commit, a pull request, and triad review. Corrections and amendments are part of that process. A completed execution or an opened pull request is not acceptance.

The proposed general lifecycle is:

| Stage | What must be clear |
|-------|--------------------|
| Intake and triage | Consumer, need, owner, urgency, affected services, and whether this is authorized work or a proposal |
| Definition and authorization | Outcome, boundaries, acceptance evidence, allowed actions, applicable spec or runbook, and escalation path |
| Context preparation | Role, workload guidance, assigned skills, task specification, and the evidence needed for the next action |
| Execution and verification | What ran, what changed, what checks found, and what remains uncertain |
| Review and disposition | Whether the result meets the need; accept, correct, amend, defer, or stop, with the decision's authority preserved |
| Delivery and closure | Consumer-facing outcome, evidence, documentation, and any remaining obligations assigned to an owner |

Context is selected for the job and expanded when needed within scope. This bounds the information and actions offered to an agent; it does not guarantee control over all of a model's prior knowledge or behavior. Missing evidence, an inadequate skill, or a permission limit should surface as a finding or escalation. Newly discovered work is linked and triaged instead of silently enlarging the assignment.

Mechanical validation precedes LLM review where it applies. For an Ansible change, that includes the applicable YAML, Ansible, and policy checks. Code, data, and documentation need their own appropriate checks. Review can assess meaning and adequacy; it cannot turn a failed required check into a passing result.

Observations and model interpretations remain distinguishable. A collector reports what it observed and how; a named analysis skill may reason over that evidence through a suitable runtime and record its inputs, output, and uncertainty separately. This keeps deterministic collection inspectable while allowing model-assisted analysis.

Consumer resolution and internal closure can occur at different times. A restored service may still need documentation or problem investigation. Remaining obligations keep an owner and a visible state until completed or explicitly disposed of.

---

## 8. Durable State and Replaceable Tools

Necessary work state must survive an agent session. Task-scoped execution is ephemeral; intent, evidence, decisions, and recoverable progress live in durable records. An authorized correction may continue an existing execution session when the applicable procedure allows it. A session is not the unit of business authority.

Work items, specs, execution attempts, runtime sessions, pull requests, and decisions are distinct records with explicit links. One work item may span several attempts and reviews. Stable identifiers connect them without requiring one product's identifier to become the identity of everything else.

For work to be recoverable, an authorized replacement must be able to determine:

- What was requested, for whom, and under whose authority.
- The current owner, state, dependencies, and next permitted action.
- Which spec, skill, runbook, and relevant versions governed the attempt.
- What actually happened, including changes, checks, evidence, and unresolved uncertainty.
- What was decided, by whom, and what remains to be delivered or closed.

Each kind of state has a named authoritative home. Other surfaces link to it or carry dated evidence snapshots. Conversation supports deliberation, but consequential decisions and handoffs must enter the durable work record; hidden agent exchanges cannot become a competing source of authority.

iTop is the intended ITSM and CMDB integration for richer service records, relationships, change management, and shared work views. Filesystem records and existing coordination tools can implement the operating model before that integration is complete. Astro capabilities, knowledge stores, inference providers, execution runtimes, and user interfaces should likewise have explicit boundaries and replaceable adapters.

Losing iTop or another coordination product should reduce convenience or speed while leaving the triad able to resume manually from preserved records. This requires usable exports, evidence references, and recovery procedures, alongside backups. A backup preserves material; a recovery exercise establishes whether someone can understand and resume the work. Lost authority evidence or unavailable physical capabilities may still pause a particular action. Recovery does not waive those requirements.

---

## 9. Demonstrated Practice and Intended Capability

The operating practice has advanced beyond the original repository's narrow autonomous-operations design. The current basis is real delivered work, a functioning spec-to-review process, modular skills and tools, and durable coordination records. The fully integrated service platform remains work ahead.

| Evidence level | Position at this revision |
|----------------|---------------------------|
| Demonstrated outputs | Steam Dataset 2025 is published and downloaded; a university has announced its selection for an upcoming event. ARD captures the method emerging from the work. |
| Demonstrated operating practice | Fresh agents execute scoped engineering work through verification, commits, PRs, and review. Corrections expose gaps in specs, skills, and execution. This is experience-based evidence, without a measured general success rate. |
| Developing capabilities | Astro and the surrounding tools are being developed and reviewed against real assignments. Their individual status belongs with their implementations. |
| Intended integration | iTop-backed service delivery, broader recurring operations, richer work views, and more automated coordination require separate implementation and acceptance evidence. |

The Steam result predates this charter and the completed integration envisioned here. It demonstrates the underlying practice of producing and retaining value. It does not establish that a complete autonomous EthOps platform is already deployed.

---

## 10. Development and Evaluation

Development proceeds through useful service increments. The next increment should address a real consumer need and expose a specific gap in the operating model or its capabilities. A manual step may remain manual when automation would add more cost than value.

The candidate first pilot is the [daily log digest](README.md#-first-pilot-daily-log-digest): a recurring, low-risk service that exercises the route from intake to closure. It proceeds in small steps, beginning with a probe of the inference provider, and each step's evidence scopes the next. Automation follows demonstrated friction, repetition, or reliability needs. Broader autonomy requires evidence that the relevant controls and recovery paths work.

For each increment, evaluate the consumer's result, delivery cost, review effort, rework, and continuing obligations. Where reuse is a goal, inspect actual reuse or saved effort. Where continuity is a goal, exercise handoff or recovery. Record the measurement period and limitations; output volume, agent activity, and download counts alone cannot establish value.

The model should also remain useful where execution privileges or connectivity are restricted. In those settings, the deliverable may be analysis, evidence, or a prepared change for an authorized operator. Adapting the route to delivery preserves the same boundaries around authority and acceptance.

---

## 11. Publication Boundary

This repository explains the operating model and publishes selected evidence, results, and reusable material. Operational implementation details, private skills and prompts, work specifications, raw execution evidence, credentials, and personal or sensitive context remain private by default. Publication is an explicit selection and review step.

Published claims must identify whether they describe observed practice, operator experience, a design requirement, or a planned capability. Public artifacts should carry enough provenance and limitations for their intended use. Reusable value includes helping a reader understand what an artifact can and cannot support.

---

## 12. Triad Review and Adoption

Claude and GPT reviewed version 0.2 on October 22, 2026, each also reviewing the other's findings, and Don dispositioned them. This version applies that review: it names a candidate pilot, defines Astro and the Forge for public readers, trims material duplicated in the README, and replaces the README's responsibility diagram with the record relationships of §8. The same revision aligned [AGENTS.md](AGENTS.md) with this draft and marked the earlier infrastructure notes and diagrams as historical.

The review should continue to test three points: whether this captures the consumer relationships and value commitments; whether the boundary between EthOps, Astro, the environment, and consumer projects is clear; and whether the proposed continuity and proportionality requirements are practical.

Adoption requires Don's recorded decision. Until then, this charter is the working direction rather than adopted policy. Specific adapters, service targets, automation policies, and additional execution authority remain decisions for the work that needs them. Charter changes follow the same review discipline, with reasons and superseded decisions preserved.

---

## 13. History and References

EthOps began as an ephemeral operations team design for the Proxmox Astronomy Lab. This revision retains bounded roles, durable records, least privilege, change control, and ephemeral execution while broadening the purpose to service delivery and cumulative learning across consumers.

| Resource | Relationship |
|----------|--------------|
| [README](README.md) | Public introduction, Steam-to-ARD evidence, and current project status |
| [Original README](https://github.com/vintagedon/ethops/blob/59da2c52f25ad53280ab4ccb070c29003ea910ec/README.md) | Earlier autonomous DevOps design, preserved at its prior revision |
| [September charter draft](https://github.com/vintagedon/ethops/blob/e3331102add1ffa0ebb7983a643f9ae60d85e8c8/CHARTER.md) | Previous proposed refinement; historical design rather than evidence of deployment |
| [Proxmox Astronomy Lab](https://github.com/radioastronomyio/proxmox-astronomy-lab) | Infrastructure and research environment from which the practice developed |
| [Steam Dataset 2025](https://github.com/vintagedon/steam-dataset-2025) | Delivered data product and precursor to the ARD methodology |
| [Analysis-Ready Datasets](https://github.com/vintagedon/analysis-ready-datasets) | Methodology for preparing reusable analytical capabilities |

---

## 14. Document Info

| | |
|---|---|
| Owner | VintageDon |
| Draft prepared by | GPT, from Don's direction and source review (v0.2); revised by Claude from the triad review (v0.3) |
| Reviewers | Claude and GPT (October 22, 2026), with Don's dispositions |
| Created | 2026-09-27 |
| Updated | 2026-10-23 |
| Version | 0.3 |
| Status | Draft; triad review applied; not adopted |
