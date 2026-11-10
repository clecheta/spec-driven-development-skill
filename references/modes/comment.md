# Mode: comment

Post one comment. Do not change title, description, labels, assignees, or state
unless the user explicitly asks in the same message (prefer dedicated modes for
structured updates).

## Input

Item reference + comment text or intent. If the item is already in context, the
id may be omitted when unambiguous.

## Steps

1. Complete [Boot](../../SKILL.md#boot-every-mode).
2. Resolve the item id (ask once if missing).
3. Prefer the user's body verbatim. If they gave only intent, draft a concise
   comment in the conversation language. Do not invent facts or commitments.
4. Optional light **Read body** only when needed for accuracy (e.g. current
   title). Do not dump the full item unless the user also asked `read`.
5. **New comment** immediately — no approval gate.
6. Reply to an existing thread only when the user names a discussion and
   `discussion_id` is known → bridge reply operation. Default is always a new
   top-level comment.
7. Confirm briefly: link, posted, optional short quote of the body.

## Rules

- Post as soon as id and body are clear.
- On failure, report the error and stop.
