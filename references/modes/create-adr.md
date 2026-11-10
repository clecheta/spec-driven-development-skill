# Mode: create-adr

Optional add-on. Outside the create → spec → refine → architecture sequence.
Writes one Architecture Decision Record into the workspace that owns the
decision. No queue label.

## Input

Decision context (text, @files, folders, links). An item id is optional.

## When to refuse

Stop without writing a file when the ask is:

- Trivial or low-impact
- An implementation detail
- Temporary or experimental
- A config that will churn often

Say so briefly and stop.

## Boot (this mode only)

Unlike other modes, **do not** require `.cursor/rules/issue-tracker.mdc`.

1. Resolve which workspace root receives the file.
   - One clear root → use it.
   - Several roots with ADR conventions → ask once which wins.
2. If an item id is present **and** a project `issue-tracker.mdc` is available,
   open the tracker bridge later for an optional comment after write. If either
   is missing, skip tracker steps entirely.

## Locate convention

1. If the project's issue-tracker rule (when present) defines `adr_dir` and/or
   `adr_format`, those win. See
   [`../rule-contract.md`](../rule-contract.md).
2. Else scan for an existing set matching `adr-*.mdc`, `adr-*.md`, `ADR-*.md`, or
   `NNNN-*.md` under, in order:
   - `.cursor/rules/architecture/`
   - `docs/adr/`
   - `docs/decisions/`
   - `docs/architecture/decisions/`
   - `adr/`
3. One set → next sequential number, same directory, same extension, same
   section headings and language as the corpus. Match frontmatter shape when
   existing files use Cursor `.mdc` (`description`, `globs`, `alwaysApply`).
4. Two or more sets → ask once which to extend.
5. None → ask once. Default: `docs/adr/NNNN-slug.md` (Markdown, no Cursor
   frontmatter). Do **not** invent `.cursor/rules/` in a repo that does not use
   it.

For `.mdc` ADRs:

- Infer `globs` from paths cited in the decision; ask once if unclear.
- `alwaysApply: false` unless the user explicitly wants always-on.

## Steps

1. Complete Boot and Locate convention above.
2. Collect only what is missing: problem/need, the decision itself, real
   alternatives (if any were evaluated). Do not invent alternatives.
3. Draft from [`../../assets/adr.template.md`](../../assets/adr.template.md),
   adapted to the corpus headings when they differ. Omit "Alternatives
   considered" when none were evaluated. No hardcoded author; include
   decidors only if the user provides them.
4. Present the draft. **PAUSE** for explicit approval.
5. After approval, write the file. Set **Date** from the real file timestamp
   (`stat` or equivalent) in `YYYY-MM-DD HH:MM:SS`.
6. If an item id and tracker bridge are available: **New comment** with the
   relative path of the ADR. Do **not** add any queue label.
7. Confirm: path written, optional item comment link.

## Rules

- One lasting decision per file.
- Facts only — no speculative scenarios.
- Concise: clarity over completeness (humans and agents).
- Never write without the approval gate.
- Never apply `ready4Dev` or other ignored signals from SKILL.md.
