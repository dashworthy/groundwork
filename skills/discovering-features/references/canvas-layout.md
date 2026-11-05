# Canvas layout

Contents: the Discovery page · card templates · card states · removing a topic · the Plan page · layout hygiene

When a related canvas already sets a style (colours, card widths, heading text), copy it over these defaults.

## The Discovery page

One frame per section, top to bottom, each starting with its number and a one-line colour key.

| # | Frame | Holds | Colour key |
|---|---|---|---|
| 1 | Overview | The ask (the ticket quoted verbatim, grey card), questions to answer (Q1…), draft story statements, today (from the codebase map), the proposed shape, glossary, out-of-scope line | — |
| 2 | Gaps | G1… cards | red = blocks the ask, orange = needed for correct data, grey = can come later |
| 3 | Process flows | F0… mermaid flows, one per ticket question plus the cross-cutting ones | — |
| 3b | Behaviour matrix | Only when the feature changes existing actions or automations | grey = unchanged, blue = changes, orange = open |
| 4 | Decisions | D1… cards, then O1… open questions | blue = recommended default |
| 5 | Follow-ups | FU1… cards | grey = proposed, green = approved |

- **F0 is the shared rule** every other flow calls. Draw it first; the rest reference it by name.
- **The behaviour matrix:** rows are the states the data can be in, columns are the existing actions and automations. Each cell shows today, then proposed.
- **The out-of-scope line** lists what the user ruled out as a future consideration. Leave it out for topics the user removed outright.

## Card templates

**Gap**

> **G‹n›** ‹the problem, in today's terms›
> - **Today:** ‹what the code does› (‹path:line›)
> - **Proposal:** ‹the fix›. Handled by F‹n›, D‹n›.

Keep "Today" when the card is later agreed; it's the evidence the decision rests on.

**Decision**

> **D‹n›** ‹the question›
> - **Recommended:** ‹the default› (F‹n›)
> - **Alternative:** ‹the other answer›

After the user picks, add a "Rejected: ‹option› (‹why›)" line for each option not taken, so the reasoning survives.

**Follow-up**

> **FU‹n›** ‹what's broken›
> - ‹what breaks, in one line›
> - ‹path:line›

**Open question (O)**: the question, the options so far, and which flow box it blocks.

## Card states

| State | Look | Stamp added to the card |
|---|---|---|
| Proposed | its section colour | none |
| Agreed | green | `AGREED, <Mon D>: <the answer in one line>` |
| Already planned elsewhere | green | `ALREADY PLANNED, <Mon D>: <which canvas or slice>` |
| Open | orange | `OPEN, revisit later`, plus an O card under Decisions |
| Context from the user | violet | their use cases or reasoning, verbatim where possible |

A flow box that depends on an open item turns orange too, so the flows show what is still unsettled.

## Removing a topic

When the user drops something from scope:

1. Find every mention first: cards, flow boxes, matrix cells, glossary, overview, Plan page.
2. Delete the cards outright. Strip the topic from every other shape.
3. Renumber everything after the deleted cards in each series (G, D, F, Q) with no skipped numbers, and update every cross-reference in text.
4. Re-pack the grids to close the holes.
5. Report a Was → Now table so the user can follow references they remember.

Add an out-of-scope line only when the user calls it a future consideration. "Like it was never discussed" means no trace at all.

## The Plan page

A second page, **Plan**, built after the gate. It holds only the agreed outcome; history stays on Discovery.

1. **Data.** One card per table. Grey = existing and changed, blue = new. Each column with its type, required or nullable, backfill, and a short comment. A line at the top naming dependencies on other plans' slices.
2. **Behaviour.** One card per area: the shared rule (F0), each action that changes, each new process, the automations.
3. **Pages and mockups.** One violet card per page or component change, naming the real components, plus the mockup Artifact link at the top.

## Layout hygiene

- A card's text fits inside it; trim the "Today" paragraph before growing a card into its neighbour.
- A new section goes below the frames it follows, never inside one. Push later frames down to make room.
- Grow a frame when a redrawn flow outgrows it, and move the frames below.
- Check with a screenshot and the canvas lints after every layout change.
