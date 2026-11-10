# Mode: create

Capture a new idea or bug as an item, or complement an open item on the same
theme. Later modes (`refine`, `spec`) are independent — do not run them unless
asked.

## Input

Free text, @files, folders, or links describing the ask.

## Steps

1. Complete [Boot](../../SKILL.md#boot-every-mode).
2. Understand the request; ask only when unclear.
3. Ground product context from the project's indexed docs when the rule points
   to them. Do not preload whole doc trees.
4. **Dedupe:** **List open** items once with a focused search (bridge). Compare
   theme (area, capability/bug, technical scope). Prefer precision.
   - Likely match(es) → stop create; ask whether to complement or create new.
   - Related but not the same → note them for the description (no link API
     required; cite ids in the draft).
5. **Complement** (user confirmed same theme):
   - Read body.
   - Draft merged description (preserve existing; add only what is new).
   - Keep title unless the user wants a rename.
   - Adjust area labels from the rule.
   - Show draft; wait for approval.
   - **Edit** description/labels; set assignee per rule. Do **not** re-apply
     `Backlog` just because of a complement.
6. **Create new** (no match or user declined):
   - Draft title + description + labels (`Backlog` + area labels from rule).
   - Show draft (including related ids cited); wait for approval.
   - **Create** with assignee per rule.
7. Confirm: URL/id, what was saved, assignee, and that link/milestone/start_date
   were skipped if the bridge cannot write them.

## Rules

- Do not invent items.
- Do not run `refine` or `spec` automatically.
- If the bridge has no link operation, mention related items in the description
  and say so in the confirmation — do not hunt for another tool.
