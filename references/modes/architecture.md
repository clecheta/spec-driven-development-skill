# Mode: architecture (alias: arch)

Two gated phases: Analysis, then Architecture. Alias `arch` uses this same
file. After explicit approval, persist the document as a comment and add the
`architecture` label.

Follow skill **`feature-architecture`** for design depth, references, and the
proposal template. This file owns tracker persistence and the sequence gates.

## Input

Item reference plus any @files, folders, or links. If the id is missing, ask
once. Do not invent an item.

## Phase 1 — Analysis

1. Complete [Boot](../../SKILL.md#boot-every-mode).
2. Read the item (and parents/children if needed). Understand:
   - Context, goal, directional approach
   - New APIs/tools, testing, dependencies, constraints
3. Draft the 3–5 most important clarifications. Ask them while sharing your
   understanding and suggestions. **PAUSE**.
4. Ask follow-ups if needed. **PAUSE**.
5. Restate understanding as a reviewable artifact. **PAUSE** for explicit green
   light before Phase 2.
6. If discussion changes written requirements, ask permission before editing
   (structural edit or clarifying comment). Do not proceed without approval.

## Phase 2 — Architecture

1. Explore relevant source and project technical standards.
2. Run `feature-architecture` workflow (proposal sections, Mermaid when useful).
3. If anything contradicts earlier understanding, ask. **PAUSE**.
4. Present the architecture artifact; iterate. **PAUSE** for approval.
5. After approval:
   - **New comment** with the approved architecture document
   - **Edit** labels: add `architecture`; ensure area labels from the rule
   - Assignee per rule
6. Confirm: link, label `architecture`, comment posted. State any bridge limits
   (milestone/links) that were not written.
7. **Optional ADR suggestion (critical, not automatic).** Look at this project's
   rules, existing ADRs, and what the approved decision locks in for agents and
   humans going forward. Suggest mode `create-adr` **only** when that look shows
   the record is necessary or useful — e.g. the choice contradicts or extends a
   rule, sets a pattern several modules will repeat, or would otherwise be
   re-litigated. When the judgment is no, finish without mentioning ADR. Never
   end every architecture run with a stock ADR prompt. Do **not** write the ADR
   file in this mode; if the human wants it, they invoke `create-adr`.

## Research

When unsure about a library, look it up (Context7, docs, search). Do not guess.

## Rules

- Never start Phase 2 without Phase 1 approval.
- Never skip the architecture approval gate.
- Do not apply `ready4Dev` or other ignored signals from SKILL.md.
- Do not create ADR files here; only suggest `create-adr` when justified.
