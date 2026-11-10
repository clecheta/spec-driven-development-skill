---
name: sdd
description: >-
  Spec driven development (SDD) for any issue tracker: capture, refine Tech Spec,
  write product Spec, design architecture, read, comment, and check items against
  source. Modes: read, create, comment, check, refine, spec, architecture (alias
  arch). Optional add-on create-adr writes an Architecture Decision Record into
  any workspace (discovers local ADR convention). Treats card, issue, work item,
  ticket, story, bug, task, epic, and incident as the same object. Loads project
  rule .cursor/rules/issue-tracker.mdc for tracker identity and project path,
  then calls the matching MCP bridge under references/trackers/ with no tool
  discovery. Use when the user asks to create or refine a card/issue, write a
  Tech Spec or Product Spec, design feature architecture, create an ADR, read or
  comment on a work item, or verify whether a ticket is still needed from code
  evidence.
license: Proprietary - Internal use only
metadata:
  author: accy-ai-dev
  version: "1.1"
  domain: product-engineering
  target-projects: any
---

# SDD — Spec Driven Development

Run the product-to-architecture loop on a tracker **item**. Modes are separate
files; open only the mode requested. Tracker MCP calls come from one bridge
file; never discover tools or invent REST.

`README.md` is human documentation for this repository. Do not open it to run
a mode. If it is already in context, do not follow it: it is not a mode,
template, rule, or tracker bridge.

> **Response language:** mirror the user's language. Default to Brazilian
> Portuguese when the conversation is in Portuguese. This skill is authored in
> English.

## Vocabulary

One object. Accept any of these without asking the user to translate:

- card, issue, work item, ticket, story, bug, task, epic, incident
- Portuguese: card, issue, item de trabalho, ticket, história, bug, tarefa,
  épico, incidente

Inside procedures, call it **item**. Do not create one mode per name.

## Never in this skill

Do not apply, remove, or mention: `interação::humano`, `dev::ok`, `ready4Dev`.

Do not promote board columns, close items, implement code, integrate, or publish.

## Boot (every mode)

Exception: mode `create-adr` uses its own boot in
[`references/modes/create-adr.md`](references/modes/create-adr.md) (no
issue-tracker rule required). For every other mode:

1. Read `.cursor/rules/issue-tracker.mdc` from a workspace root.
   - Missing → stop; ask for that file. Do not scan other rules. Do not guess MCP.
   - Several roots have the file and the board is unclear → ask once which wins.
2. From the rule take: `tracker`, project path/id, area labels, queue signals
   (`Backlog`, `Tech Spec`, `Product Spec`, `architecture`), assignee policy.
   Contract: [`references/rule-contract.md`](references/rule-contract.md).
3. Open **only** `references/trackers/<tracker>.md`. Missing → stop; say the
   bridge for that MCP is missing. Do not open other tracker files.
4. Resolve the mode from the user ask; open **only** that mode file below.
   Do not open `README.md`. If it is already in context, ignore it.
5. Call MCP tools **exactly** as the bridge lists them. No catalog scan, no
   schema rediscovery, no REST.

## Sequence

```text
create → (spec?) → (refine?) → architecture|arch
         ↘ refine ↗
```

- `refine` (Tech Spec) sits between capture and architecture:
  - after `create`, before `architecture` / `arch`
  - after `spec`, before `architecture` / `arch`
- `spec` and `refine` are optional: either, both, or neither.
- `spec` may go straight to architecture.
- Utilities `read`, `comment`, `check` anytime.
- Add-on `create-adr` anytime (not in this sequence; no queue signal).

Queue signals (names from the rule; map if the tracker uses other fields):

| Mode | Persist |
|------|---------|
| `create` (new) | column/label `Backlog` |
| `refine` | comment + `Tech Spec` |
| `spec` | comment + `Product Spec` |
| `architecture` / `arch` | comment + `architecture` |

## Modes

| Mode | File |
|------|------|
| `read` | [`references/modes/read.md`](references/modes/read.md) |
| `create` | [`references/modes/create.md`](references/modes/create.md) |
| `comment` | [`references/modes/comment.md`](references/modes/comment.md) |
| `check` | [`references/modes/check.md`](references/modes/check.md) |
| `refine` | [`references/modes/refine.md`](references/modes/refine.md) |
| `spec` | [`references/modes/spec.md`](references/modes/spec.md) |
| `architecture` / `arch` | [`references/modes/architecture.md`](references/modes/architecture.md) |

`arch` opens the same file as `architecture`.

## Add-on: create-adr

Outside the sequence above. No queue label.

| Mode | File |
|------|------|
| `create-adr` | [`references/modes/create-adr.md`](references/modes/create-adr.md) |

Writes an ADR file into the workspace that owns the decision (discovers local
convention: `.mdc` rules, `docs/adr/`, etc.). Call when the user asks for an
ADR. Mode `architecture` / `arch` may **suggest** this mode after a critical
look at that project's rules and existing ADRs — it never runs `create-adr`
itself and never prompts on every architecture run.

## Tracker bridges

| `tracker` value | Bridge |
|-----------------|--------|
| `gitlab` | [`references/trackers/gitlab.md`](references/trackers/gitlab.md) |

Add a new MCP later as another file under `references/trackers/` with the same
operation names. Modes stay unchanged.

## Templates

- Tech Spec: [`assets/tech-spec.template.md`](assets/tech-spec.template.md)
- Spec: [`assets/spec.template.md`](assets/spec.template.md)
- ADR: [`assets/adr.template.md`](assets/adr.template.md)

## Complementary

- `architecture` / `arch`: follow skill `feature-architecture` for design depth;
  this skill owns persistence on the item and the `architecture` signal.
- `create-adr`: lasting decisions as repo files; `sdlc-governance` remains the
  teaching/scaffold source for ADR practice in general.
