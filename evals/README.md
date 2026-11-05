# groundwork evals

Run with `claude plugin eval`. Each case is a prompt plus graders, scored with and without the plugin.

| Case | What it pins down | Graders |
| --- | --- | --- |
| `fires-on-feature-planning` | planning a multi-part feature fires the skill | `tool_used: Skill` |
| `fires-on-gap-hunting` | "find the holes and draw the flows" fires it, with no mention of a canvas | `tool_used: Skill` |
| `no-fire-small-change` | a one-line change does **not** start discovery | `tool_used: Skill, max: 0` |
| `holds-gate-on-skip-ahead` | jumping to mockups early gets the list of unagreed items and a choice, not mockups | `llm` ×2 |

## tldraw can't run headless

`claude plugin eval` runs without tldraw Desktop, so these cases test routing and the gate, not canvas drawing. To check the canvas work, run the skill in a live session with tldraw Desktop open.

## Running

```bash
claude plugin eval . --trust-plugin --runs 1
claude plugin eval . --case holds-gate-on-skip-ahead --trust-plugin --runs 1 --keep-temp
```
