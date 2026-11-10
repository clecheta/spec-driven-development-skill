# Mode: check

Verify whether an open item still reflects real work: read the item, search
source for evidence, post one structured comment. Do not close the item or
change labels unless the user asks.

## Input

Item reference. Optional focus (e.g. "only media items").

## Steps

1. Complete [Boot](../../SKILL.md#boot-every-mode).
2. Resolve the item id (ask once if missing).
3. **Read body** + **Read comments** (enough for a verification checklist — not
   a full AS-IS dump unless the user also asked `read`).
4. Map repos from area labels in the rule (or infer from title/description and
   say so). Search only repos that exist locally for the workspace.
5. For each distinct requirement / bug claim, classify:

| Status | Meaning |
|--------|---------|
| **Corrigido** | Clear evidence in code (prefer tests too) |
| **Parcial** | Some of the ask exists |
| **Aberto** | Code still matches the bug / missing behavior |
| **Inconclusivo** | Not enough evidence |

Cite paths/symbols. When unsure, use **Inconclusivo**, not **Corrigido**.

6. Overall verdict:

| Verdict | When |
|---------|------|
| **Item ainda necessário** | Any **Aberto** / meaningful **Parcial**, or key **Inconclusivo** |
| **Item provavelmente obsoleto** | Every actionable item **Corrigido** — recommend close; do not close |
| **Escopo reduzido** | Mix of fixed and remaining work |

7. **New comment** immediately (no approval) with a table of items/status/evidence
   and the conclusion. Conversation language.
8. Confirm in chat: link, compact summary, comment posted. Do not chain other
   modes unless asked.

## Rules

- Default write: one comment only.
- Prefer evidence over optimism.
