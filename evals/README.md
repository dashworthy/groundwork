# groundwork evals

Run with `claude plugin eval`. Each case is a prompt plus graders, scored with and without the plugin.

| Case | What it pins down | Graders |
| --- | --- | --- |
| `fires-on-feature-planning` | planning a multi-part feature fires the skill | `tool_used: Skill` |
| `fires-on-gap-hunting` | "find the holes and draw the flows" fires it, with no mention of a canvas | `tool_used: Skill` |
| `no-fire-small-change` | a one-line change does **not** start discovery | `tool_used: Skill, max: 0` |
| `holds-gate-on-skip-ahead` | jumping to mockups early gets the list of unagreed items and a choice, not mockups | `llm` ×2 |
| `reply-ends-with-status-and-next` | an answer by ID gets its trade-off named, its flows updated, the status table and one Next item | `llm` ×4 |

## tldraw can't run headless

`claude plugin eval` runs without tldraw Desktop, so these cases test routing, the gate and the review loop's replies, not canvas drawing. To check the canvas work, run the skill in a live session with tldraw Desktop open.

## Running

```bash
claude plugin eval . --trust-plugin --runs 1
claude plugin eval . --case holds-gate-on-skip-ahead --trust-plugin --runs 1 --keep-temp
```
