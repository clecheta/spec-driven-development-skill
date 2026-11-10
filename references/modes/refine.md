# Mode: refine

Produce a **Tech Spec** as a new comment. Independent of `spec`. Valid after
`create` or after `spec`; always before `architecture` / `arch`. Never change
title or description.

## Input

Item reference and/or requirement text, @files, links.

## Steps

1. Complete [Boot](../../SKILL.md#boot-every-mode).
2. Load enough context (body / prior comments) if not already in chat.
3. Ask clarifying questions until the feature goal and requirements are clear.
4. Present a summary for approval:

```text
Based on our discussion, here is my understanding of the feature requirements:
[concise summary]
Is this understanding correct? Would you like to make any changes or additions?
```

Iterate until the user approves. Research codebase or docs when needed.

5. Fill [`assets/tech-spec.template.md`](../../assets/tech-spec.template.md)
   (headings POR QUE / O QUE / COMO). Keep those headings.
6. After approval:
   - **New comment** with the filled template
   - **Edit** labels: add `Tech Spec`; ensure area labels from the rule
   - Assignee per rule
7. Confirm: link, label `Tech Spec`, comment posted.

## Rules

- Audience: AI-native engineer — concise, enough to proceed without follow-ups.
- Do not leave inventing requirements; ask.
- Do not mention or touch ignored queue signals from SKILL.md.
