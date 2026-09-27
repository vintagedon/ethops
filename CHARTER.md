<!--
---
title: "Ethops Project Charter"
description: "Purpose, scope, operating principles, roles, and milestones for running autonomous agents as an ITIL operations team"
author: "VintageDon (https://github.com/vintagedon/)"
date: "2026-09-27"
version: "0.1"
status: "Draft"
tags:
  - type: policy
  - domain: [autonomous-ops, itil]
  - tech: [itop, postgresql]
related_documents:
  - "[README](README.md)"
  - "[Writing Style Guide](docs/documentation-standards/writing-style-guide.md)"
---
-->

# Ethops Project Charter

This charter records the refined direction for ethops as of September 2026. Where it and the March 2026 design in the [README](README.md) disagree, this document governs.

---

## 1. Purpose

Ethops runs autonomous agents as an ITIL operations team. Each agent fills a defined role, works assigned tickets in an open-source ITSM, and hands work on through the same queues, approvals, and records a human IT team would use. Engineering work executes through a spec lifecycle that already functions as change control.

Most multi-agent systems coordinate through conversation between agents. That approach produces text but not the things operations depends on: ownership, current state, change history, approvals, and an audit trail. The March 2026 design had the right organizational model but no mature engineering workflow underneath it. That workflow now exists and runs every night: gated specs, one commit per gate, a pull request reviewed by automated code reviewers and the operator, worklogs, and standalone amendment specs. Ethops puts an operations layer above it.

---

## 2. Scope

In scope for v1:

- iTop as the operations record: tickets, queues, CMDB, approvals, and handoff history
- The virtual employee model: roles with queues, permitted state changes, skills, and credential scopes
- One employee working end to end (the Overnight Sysop)
- Linking the spec lifecycle to tickets
- An append-only action log
- Mail ingress for requests and alerts
- Recurring operational tickets

Out of scope for v1:

- iTop as the queue the dispatcher reads from. The existing file-based spec queue stays in place, with iTop above it.
- The external assistant receiving assignments. It waits on that product shipping its own email address.
- Any infrastructure change executed by an agent without CAB approval. v1 employees produce reports and records.
- GPU scheduling, a message bus, a graph database, and per-role directory identities. The March design needed these; this one does not.

---

## 3. Audience

The operator, the AI peers who review and build with the operator, future contributors, and anyone evaluating the approach. It assumes familiarity with ITIL basics and with the idea of an LLM coding agent.

---

## 4. Architecture

Ethops has three layers. Work crosses between them only through tickets and email.

| Layer | Occupant | Holds | Boundary |
|-------|----------|-------|----------|
| External | Administrative assistant (currently Meta's Muse) | Web research, email, calendar, SaaS work, external monitoring | No network route into the cluster and no cluster credentials. Communicates by email only. |
| Operations | iTop 3.3 on the cluster | Tickets, queues, CMDB, approvals, handoff history | The single source of workflow state |
| Execution | Short-lived agents working through specs, skills, Ansible, and Git on the cluster's control node | Engineering artifacts and execution evidence | Acts only on tickets assigned to its role |

The CMDB fills from two sources. Combodo's Proxmox data collector synchronizes cluster, node, virtual machine, and storage records automatically. Agents add application-level records and employee registrations through iTop's API.

---

## 5. Operating Principles

1. One unit of engineering intent is one ticket. The ticket covers the original spec, every amendment spec, review cycles, documentation, and final acceptance. Specs remain fixed execution contracts inside it; an amendment is a new standalone spec that names its parent, never an edit to an archived one.
2. Not every ticket needs a spec. A nightly log review is a fresh ticket each night that follows a standing runbook.
3. Git holds the engineering record: specs, amendments, commits, worklogs, code, and documentation. iTop holds workflow state: who has the work, why it exists, which CMDB items it affects, and where it stands. Ticket notes are short checkpoints that link to the evidence; they never replace worklogs.
4. The ticket number travels with the work. It appears in spec frontmatter, commit messages, pull request descriptions, worklogs, and the work registry, so one identifier traces a change across every system.
5. External input can open work but never authorize it. A request from email, an alert, or the external assistant arrives as a new ticket in triage. It cannot approve a change or mark work ready to execute. iTop account profiles enforce this, not prompt instructions.
6. An employee is a role, not a model. The Overnight Sysop might run on one model today and another next month; the role's queue, permissions, and records stay the same.
7. iTop keeps its standard ticket states. A ticket's stage is shown by which team queue holds it, so the lifecycle needs no data-model customization that every iTop upgrade would have to carry.
8. Work that touches a CMDB item is a Change. Everything else, including most code work, is a User Request.
9. Agents are short-lived and hold no state that matters. If one fails mid-task, a replacement rebuilds its job from the ticket, the Git record, and the action log.
10. A failure during execution opens its own Incident, linked to the originating ticket. Newly discovered work gets its own ticket, linked as a follow-up, so no ticket grows past its original intent.

---

## 6. Roles

| Role | Holder | Authority |
|------|--------|-----------|
| Operator | The project owner (human) | Sole approver. Sets priority and holds merge authority. |
| Change Advisory Board | The operator and two AI peers (currently Claude and GPT) | The peers review and recommend; approval stays with the operator. Whoever builds a change does not review it. An approval relayed by a peer counts only when the operator's exact words, time, and the relaying peer are logged. |
| Virtual employees | Roles filled by short-lived agents | Work tickets assigned to their queue, within the state changes their iTop profile allows. No employee approves its own work. |
| Administrative assistant | An external agent (currently Meta's Muse) | Performs external work and requests internal work by email. Never authorizes anything. |

Each virtual employee is defined by an iTop identity and profile, an assignment queue, the state changes it may make, the skills it uses, the execution surfaces it may touch, a credential scope, and its escalation path.

Planned employees, in order:

| Employee | Work |
|----------|------|
| Overnight Sysop | Nightly log review and routine operational checks |
| Software Engineer | Executes code specs |
| Documentation Engineer | Updates documentation after the CAB accepts implementation |
| Validation Engineer | Post-change verification |
| Research Analyst | Research and data work for the astronomy projects |

---

## 7. Work Lifecycle

Work enters iTop through one of several paths and always starts in triage.

| Source | Arrives as |
|--------|------------|
| Alertmanager, through the alerts mailbox | Incident |
| Mail to the operations mailbox, including from the external assistant | User Request |
| The operator asking for work | User Request or Change |
| An agent detecting needed remediation | A candidate Request or Change for triage |
| The scheduler | A recurring operational ticket |
| An issued engineering spec | A linked User Request or Change |
| A failure during execution | An Incident linked to the originating ticket |

From triage, a ticket moves between queues. For spec work, the path is: the ticket is assigned to an engineering employee with a link to the spec; the employee executes it, archives the spec, writes the worklog, adds a ticket note, and reassigns the ticket to the CAB queue. If the CAB finds a defect, an amendment spec is issued on the same ticket and the cycle repeats. Once implementation is accepted, the ticket can pass to documentation and return to the CAB before closing. Not every ticket uses every stage.

Recurring tickets come from a scheduled job that creates each occurrence through iTop's REST API. Each night gets its own ticket so each run keeps its own evidence and state.

---

## 8. Records and Accountability

Approvals are recorded on the iTop ticket they apply to.

Every agent action is written to an append-only log in a PostgreSQL instance on the cluster before it executes. Each row carries a hash of the row before it, so an edited or deleted record breaks the chain and shows. A row captures the employee and agent instance, timing, action type, context (ticket, affected CMDB items, documents consulted), outcome, and inference cost (model, tokens, latency).

Engineering artifacts stay in Git, as described in principle 3.

---

## 9. Identity, Credentials, and Mail

iTop receives mail through two shared mailboxes on the project's Microsoft Entra tenant: one for operations requests, which also sends iTop's notifications, and one for alerts. Shared mailboxes need no license and have no sign-in of their own. Virtual employees do not need mailboxes because they work through iTop.

Each employee gets credentials scoped to its role from the project's secrets manager. Widening an employee's access means issuing a new credential, which is a change record the CAB sees. Revoking one role must be a single action that leaves the others running.

---

## 10. Milestones

| Milestone | Delivers | Depends on |
|-----------|----------|------------|
| M1 | iTop running on a rebuilt container host, before the Proxmox 9 migration, so the migration becomes the first real change record | iTop 3.2.3 or later (see section 11) |
| M2 | Ticket linkage in the spec lifecycle: a `ticket:` field in the spec template and the closeout procedure | M1 |
| M3 | The Overnight Sysop end to end: a scheduled ticket, a log review run, the report attached, a ticket note, CAB review, closure | M1, M2, and the log review runbook |
| M4 | Mail ingress for requests and alerts | The move of project mail to Entra |

After v1: iTop as the dispatcher's queue, assignments to the external assistant, and the Documentation Engineer.

---

## 11. Dependencies and Risks

Dependencies:

- iTop versions before 3.2.3 allow unauthenticated code execution (CVE-2026-39975). The deployment targets 3.3.
- Project mail is moving from Google Workspace to Microsoft Entra. Mail ingress is built on Entra only, after the move.
- The Overnight Sysop depends on a log review runbook that is specified but not yet executed.
- The secrets manager is under evaluation; section 9 states the requirement, not the product.

| Risk | Mitigation |
|------|------------|
| iTop customization drifting with each upgrade | Standard ticket states; stages shown by queue (principle 7) |
| The external assistant's vendor changes or withdraws the product | The role belongs to ethops and the runtime can be replaced. Its persona and memory are exportable. |
| Connector churn on the external assistant | Treated as a lost capability, not a lost role |
| Malicious or mistaken input through mail or alerts | Ingress can only create tickets in triage (principle 5) |
| Credential scope creeping over time | Scope changes require a new credential and a change record |
| A single human operator | Durable state lives in iTop and Git, not in any person's or agent's memory |

---

## 12. Open Decisions

- The secrets manager: the current Doppler setup or a move to 1Password Business, pending a trial.
- Whether iTop's mail integration authenticates cleanly against an Entra shared mailbox. To be tested at M4.
- Whether the external assistant's Outlook connector accepts a Microsoft 365 work account. To be tested before project mail moves.
- Whether employees work tickets through Combodo's official MCP server for iTop or through skills that call the REST API. The MCP server's write tools are unrestricted, so either way the iTop profile behind each credential enforces the limits.

---

## 13. Related Work

Several projects now treat agents as staff. Ethops differs from each in what sits underneath.

| Project | Approach | Difference |
|---------|----------|------------|
| [Paperclip](https://github.com/paperclipai/paperclip) | Open-source; agents as employees in a company org chart, tickets as their communication channel, per-agent budgets, human board approval | A company metaphor with its own task tracker; no ITIL ticket classes, CMDB, or change control |
| [ServiceNow Autonomous Workforce](https://newsroom.servicenow.com/press-releases/details/2026/ServiceNow-brings-Autonomous-Workforce-to-every-major-business-function/default.aspx) | Role-scoped AI specialists that own tickets end to end on the ServiceNow platform | Closed, enterprise-priced platform |
| [Jira agents](https://support.atlassian.com/jira-software-cloud/docs/collaborate-on-work-items-with-ai-agents/) | Agents assigned to work items or triggered by workflow transitions | Agents as features of a tracker, not an operations model |

Ethops combines an open-source ITSM with real ITIL classes and a CMDB, a spec lifecycle as change control, email as the boundary to an external assistant, and roles that outlive the models filling them.

---

## 14. Public and Private Boundary

This repository publishes the charter, the operating model, the repository structure, iTop skills, and templates. Documentation and skills are licensed CC-BY-4.0.

Implementation code, cluster specifics (addresses, hostnames, topology), execution evidence, and the external assistant's personal context stay private.

---

## 15. Status

Planning. Nothing described here is deployed yet. The README's status table tracks progress.

---

## 16. References

| Resource | Description |
|----------|-------------|
| [MCP Server for iTop](https://www.itophub.io/wiki/page?id=extensions%3Aitop-mcp) | Combodo's official MCP server for iTop |
| [CVE-2026-39975](https://www.strix.ai/cve/CVE-2026-39975) | Unauthenticated code execution in iTop before 3.2.3 |
| [Introducing Muse](https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/) | Meta's announcement of the external assistant's current runtime |
| [Agent users in Microsoft Entra Agent ID](https://learn.microsoft.com/en-us/entra/agent-id/agent-users) | The licensed per-agent identity option this charter does not use |
| [Paperclip](https://github.com/paperclipai/paperclip) | Closest open-source relative |

---

## 17. Document Info

| | |
|---|---|
| Author | VintageDon |
| Created | 2026-09-27 |
| Updated | 2026-09-27 |
| Version | 0.1 |
