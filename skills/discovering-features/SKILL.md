---
name: discovering-features
description: Turn a feature ticket or idea into an agreed plan on a tldraw canvas before any spec or code is written. Maps today's code in the background, lays out a Discovery page (overview, gaps, process flows, behaviour matrix, decisions, follow-ups), walks the user through every gap and decision until each is agreed, then builds a Plan page (data, behaviour, pages) and realistic mockups from the project's real components. Use when a new feature, epic or multi-part story needs planning, when asked to flesh out, scope or pressure-test a ticket, find the gaps in a feature's logic, draw its process flows, or plan a feature on a canvas, even if tldraw or specs aren't mentioned. Not for one-line changes or bug fixes with one obvious fix.
---

# Discovering features

Say this first: `Using discovering-features to plan <feature> on <canvas path>.`

## What this guarantees

A feature reaches the spec stage with:

- every gap the feature hits in today's code, with file:line evidence, including the gaps the ask didn't mention
- a process flow for each question the ticket raises, agreed by the user
- every decision settled, with its alternatives and the reason for the pick
- a Plan page holding only the agreed outcome, and mockups built from components that already exist

The canvas is the single record. Someone opening it cold sees what was asked, what the code does today, what was decided and why.

## Skip it when

The change raises no open questions: a new column, a label, a bug with one obvious fix. Say so in one line and go straight to the project's spec or build workflow. When unsure, it isn't trivial, so run it.

## Requirements

- **tldraw Desktop and the `tldraw-offline` skill.** If either is missing, tell the user and offer to run the same sections in `docs/discovery/<feature>.md` with mermaid flows instead.
- **A structured question tool** (`AskUserQuestion` in Claude Code). Without one, ask with numbered plain-text menus.

## Working the canvas (tldraw-offline)

Load the `tldraw-offline` skill before the first canvas call. It knows how to reach the app, draw, lint and save; this skill says what goes on the canvas. Hand long or complex edits (drawing all the flows, renumbering after a removal, building the Plan page) to the `tldraw-offline` subagent with short instructions; it has the context and doesn't need asking to verify.

- **Draw flows with tldraw-offline's mermaid recipe**, never node by node. Nodes placed by hand drift and lose their arrow bindings when a flow is redrawn, and flows get redrawn often here.
- **End every edit by running the canvas lints**, fixing every new one, then saving the canvas. The canvas is the record, so an unsaved one loses decisions if the app quits. Say "lints are clean and the canvas is saved" only when both are true.
- **Screenshot after any layout change.** Cards overflow into the card below, new sections land inside another frame, edge labels sit on boxes. Fix these before reporting.
- **Write each answer to the canvas the moment it lands**, never in a batch at the end. A session can end at any turn.
- **Related canvases are read-only.** Read them for context and style; edit them only when the user asks.

## Workflow

Copy this checklist into your task list and tick it off. Long discovery sessions span dozens of turns, and an untracked step gets skipped.

- [ ] 1. Orient: related canvases read, codebase map running in the background
- [ ] 2. Discovery page: Overview filled from the ticket
- [ ] 3. Gaps and flows drawn from the map, checked against the standards
- [ ] 4. Shaping decisions asked; the rest carry recommended defaults
- [ ] 5. Review loop: every gap, decision and flow agreed or removed
- [ ] 6. Gate: the user says the flows are agreed
- [ ] 7. Plan page built
- [ ] 8. Mockups published and linked from the Plan page
- [ ] 9. Hand-off to the project's spec workflow

### 1. Orient

- **Canvas path:** the location the project's instructions name, else `~/Desktop/<Project> <Feature>.tldraw`.
- **Related canvases:** read the other canvases in that folder. Build on their deferred or "Later" items instead of re-planning them, and copy their layout, colours and card style so the set reads as one system.
- **Codebase map:** launch a background agent with the brief in [references/codebase-map.md](references/codebase-map.md). Start the Overview while it runs, but hold the flows until it reports. A flow drawn before the map encodes guesses about today's behaviour that the map then overturns, and the user ends up reviewing the guesses.

### 2–3. The Discovery page

One page named **Discovery**: Overview, Gaps, Process flows, a behaviour matrix when existing actions change, Decisions, Follow-ups. The section contents, colour keys, card templates and card states are in [references/canvas-layout.md](references/canvas-layout.md).

Two rules carry most of the value:

- **Every gap has evidence.** Today's behaviour with file:line, and a disconfirming check (is it handled somewhere else?) before the card goes up. A gap that turns out to be wrong costs the user a review round and makes them doubt the rest.
- **Hunt the gaps the user didn't raise.** Run the feature against [references/standards.md](references/standards.md); each standard that applies becomes a gap card or a line in a flow. Call these out in the reply as "gaps your ask didn't cover". They are why this beats the user thinking alone.

### 4. Shaping decisions

Most decisions have an obvious default. Ask only the 3 or 4 that change every flow, one decision per question, recommendation first with its reason (`AskUserQuestion`). Give the rest a recommended default on their card, and let the user accept them all at once.

### 5. The review loop

The user answers by ID ("G3. Yes", "agree", "Proposals for G7?"). Each answer is checked against the code, written to every card and flow it touches, and followed by the status table and the next item. The steps, reply template and how to handle confusion are in [references/review-loop.md](references/review-loop.md).

### 6. The gate

Mockups, the Plan page and any spec wait until every gap, decision and flow is agreed or removed, and the user has said the flows are agreed. This is the one hard rule. Mockups drawn on unagreed flows get redrawn when the flows change, and a spec written from them carries decisions nobody made.

When the user asks to skip ahead, answer with the list of items not yet agreed, not a verdict. If they still want to go on, that's their call: mark the skipped items OPEN on the canvas and label anything built on them as provisional.

### 7. The Plan page

Add a page **Plan** holding only the agreed outcome: Data, Behaviour, Pages and mockups. Discovery keeps the history; Plan is what gets built. Layout is in [references/canvas-layout.md](references/canvas-layout.md).

### 8. Mockups

One Artifact with every screen, linked from the Plan page:

- Inventory the project's components first (a component catalog if one exists) and the existing pages nearest each screen. Read an earlier canvas's mockup Artifact for styling.
- Label every region with the real component it uses, or mark it **NEW** or **MODIFIED**.
- Reuse an existing page layout. Propose a new layout only where none fits, and say why on the screen.
- If the project has a page-design skill (for example `designing-pages`), a screen with a new layout or new component still goes through it before its tasks are written.

### 9. Hand-off

- Break the Plan page into slices and hand each to the project's spec workflow (for example `openspec-propose` or `engineering:spec`), linking the canvas.
- Approved follow-ups become their own slices, never folded into the feature's.
- When later work deviates from the canvas (schema, pages, flows, removed or renamed features), update the canvas in the same piece of work, so it stays the record.

## Resuming

Open the canvas and rebuild the status table from the card states. Target unreviewed and open items; agreed items are settled context, so build on them without re-asking. If the files the gaps cite have changed since the canvas was drawn, re-check those gaps' evidence first.

## What this does not do

- Write specs, tasks or code. Its output is the agreed canvas.
- Design single components in depth. That's the project's page-design skill.
- Fix bugs it finds in today's code. Those become follow-ups.
- Edit related canvases.

## Red flags

| Thought | Reality |
|---|---|
| "The map is slow; I'll sketch the flows now." | Flows drawn from guesses get reviewed as if they were facts. Wait. |
| "This gap is obvious, no need for file:line." | Obvious gaps are the ones most often handled somewhere else. Cite and check. |
| "I'll record these three answers together at the end." | Write each one now, everywhere it applies. A stale flow beside an agreed card misleads. |
| "Two quick questions in one message saves a turn." | Stacked questions get one answer and one confused reply. One at a time, with an example. |
| "They want mockups; the open gaps are minor." | List what's open and let them choose. Don't decide for them. |
| "They ruled it out, but a hook for it later is cheap." | Out of scope means no columns, branches or hooks for it. |
| "Numbering gaps after a removal is fine." | Delete, renumber and fix every reference, then report a Was → Now table. |

## References

- [references/canvas-layout.md](references/canvas-layout.md): sections, colour keys, card templates and states, removing a topic, the Plan page.
- [references/review-loop.md](references/review-loop.md): handling each answer, the reply template, asking questions, proposals, confusion.
- [references/standards.md](references/standards.md): the standards every feature is checked against, with why and a worked example each.
- [references/codebase-map.md](references/codebase-map.md): the background agent's brief and the evidence rules for gap cards.
