# Issue-tracker rule contract

The project file `.cursor/rules/issue-tracker.mdc` is the only source of
**project facts** for SDD. It does **not** list MCP tool names.

## Required fields

| Field | Purpose |
|-------|---------|
| `tracker` | Key that selects `references/trackers/<tracker>.md` (e.g. `gitlab`) |
| Project path / id | Identifier the bridge uses as `project_id` / `full_path` / `parent_id` |
| Area labels | How to classify items (repos, modules, or equivalent) |
| Queue signals | Labels or fields for `Backlog`, `Tech Spec`, `Product Spec`, `architecture` |
| Assignee policy | Usually: authenticated user on every write |

## Optional

- Base URL for human-facing item links
- Product/docs index paths for grounding create/spec
- Notes about capabilities the connected MCP does **not** support
- `adr_dir` — directory for Architecture Decision Records (mode `create-adr`);
  when set, wins over workspace discovery
- `adr_format` — `md` or `mdc` (mode `create-adr`); when set with or without
  `adr_dir`, wins over discovered extension

## Must not contain

- MCP tool catalogs or discovery instructions
- REST fallback recipes
- Queue signals this skill ignores (`interação::humano`, `dev::ok`, `ready4Dev`)
