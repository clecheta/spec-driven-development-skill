# GitLab MCP bridge

Direct calls for `tracker: gitlab`. Use the GitLab MCP already connected in the
harness (Cursor: `~/.cursor/mcp.json`, namespace often `user-GitLab`). Call tools
by the names below. **Do not** list tools, rediscover schemas, or use REST.

Project path/id comes from `.cursor/rules/issue-tracker.mdc`.

## Operations → tools

| Operation | Tool | Arguments |
|-----------|------|-----------|
| Read body | `get_work_item` | `full_path` = project path, `iid` = item id |
| Read comments | `discussion_list` | `resource_type: "issue"`, `parent_id` = project path, `resource_id` = iid (string). Once. |
| List open (dedupe) | `list_project_issues` | `project_id` = project path, `state: "opened"`, `search` = keywords, low `limit`. Do not paginate the whole board. |
| Create | `create_issue` | `project_id`, `title`, `description`, `labels` (comma-separated string), `assignee_ids` (string) |
| Edit fields/labels | `edit_issue` | `project_id`, `issue_iid`; optional `description`, `add_labels`, `remove_labels`, `assignee_ids`. Omit title/description when the mode does not change them. |
| New comment | `discussion_new` | `resource_type: "issue"`, `parent_id` = project path, `resource_id` = iid, `body` |
| Reply in thread | `discussion_add_note` | same ids + `discussion_id` + `body`. Only when the user asks to reply and `discussion_id` is already known. |
| Current user | `get_user` | no args. At most once per session; reuse `id`. |

## Budget

- If the item body was already loaded in this conversation and nothing wrote to
  it since, skip another body fetch.
- Do not call `discussion_list` only to post a new top-level comment.
- Do not call `get_user` twice in the same session.

## Not available on this connected server

Do not search for tools that provide: milestone by title, `start_date`, or
item-to-item links (`link_work_items` and similar). Do not use REST. In the
user confirmation, state what was not written.

## Forbidden legacy names

These do **not** exist on this MCP. Never call them:

`save_work_item`, `save_note`, `link_work_items`, `list_work_items`
