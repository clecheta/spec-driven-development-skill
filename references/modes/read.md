# Mode: read

Read-only. Load the item AS-IS into the conversation. Do not create, edit,
comment, or change labels.

## Input

Item id (`42`, `#42`), tracker URL, or the item already in chat context. If
ambiguous, ask once. Do not guess.

## Steps

1. Complete [Boot](../../SKILL.md#boot-every-mode).
2. **Read body** (tracker bridge).
3. **Read comments** (tracker bridge) once. Flatten threads; sort by time ascending.
4. Present:
   - Header: link, title, state, labels, assignees, milestone if present
   - Full description (verbatim)
   - Timeline of notes (verbatim; light structure ok)
   - One line: item loaded; ready for other SDD modes if the user asks
5. If there are no comments, say so after the description.

## Rules

- Do not paraphrase description or comments.
- Do not invent board state.
- Include useful system notes (label changes, closes) when present.
