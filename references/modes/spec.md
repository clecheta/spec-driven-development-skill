# Mode: spec

Produce a **Product Spec** as a new comment. Mode name is `spec`; the queue
signal label remains `Product Spec`. Independent of `refine`. Never change
title or description.

## Quality bar

Can a developer or agent build from the spec alone, without follow-up questions?
If the bet, success criteria, or metrics are missing, ask until clear.

## Input

Item reference and/or requirement text, @files, links.

## Steps

1. Complete [Boot](../../SKILL.md#boot-every-mode).
2. Validate requirements from title/description/comments/files. Ask when thin.
3. Every spec needs:

| Piece | Cover |
|-------|--------|
| **Problema** | Who suffers, what they do today, why now |
| **Aposta** | Testable hypothesis — target, number, deadline |
| **Critérios de sucesso** | Observable behavior when it works |
| **Avaliação** | How to measure; when to kill, scale, or promote |
| **O que construir** | Minimum scope — flows, screens, APIs, repos |

Nail the **Aposta** (e.g. metric X→Y in N days). Vague goals fail.

4. Ground **O que construir** from the project's product docs index when the
   rule points to them. Do not bulk-load docs. Do not invent surfaces from code
   unless the user attached files or they block execution.
5. Draft with [`assets/spec.template.md`](../../assets/spec.template.md). Keep
   headings. ~one page.
6. Present for approval; iterate.
7. After approval:
   - **New comment** with the filled template
   - **Edit** labels: add `Product Spec`; ensure area labels from the rule
   - Assignee per rule
8. Confirm: link, label `Product Spec`, comment posted.

## Rules

- Tech/design detail only when it blocks execution (Notas).
- Do not require a Tech Spec to exist.
