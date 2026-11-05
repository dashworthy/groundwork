---
tags: [groundwork]
max_turns: 8
timeout_seconds: 600
allowed_tools: [Read, Glob, Grep, Skill]
---

We're mid-review on the discovery canvas for recurring service pauses. tldraw isn't open in this session, so tell me what you'd change on the canvas and reply the way you normally would during the review.

Where the canvas stands:
- G1 Pauses have no start or end date: AGREED
- G2 Skipped visits aren't recorded: AGREED
- G3 Pause state is worked out in 4 places. Proposal: one ResolvePauseWindowQuery returning a query builder, so the dispatch board can resolve every service's pause in one database call. Used by F0 and F2.
- G4 Billing keeps charging during a pause. Proposal: invoices skip any period fully inside a pause. Not reviewed.
- G5 A pause can overlap a holiday skip. Not reviewed.
- G6 Nothing stops a pause with no end date. Not reviewed.
- Flows F0 (which pause applies) to F3 are drawn but not agreed.

G3: make it an Action class, not a Query.
