# The codebase map

The map is a background agent's report on what the code does today in the area the feature touches. Gaps and flows are drawn from it, so its accuracy sets the canvas's accuracy.

## The brief

Send this, filled in, as the agent's prompt (an Explore or general-purpose agent, in the background):

> Map how ‹the feature's concept› works today in ‹repo path›, read-only. We're planning ‹the ask, one sentence›; nothing is being changed yet.
>
> Report, citing path:line for every claim:
>
> 1. The tables and columns involved; which are required, nullable, defaulted.
> 2. Every place ‹the concept› is hard-coded or assumed, with what each one does with it.
> 3. Every action, automation, job and API route that reads or changes it, including mobile and other API consumers.
> 4. What exists for ‹each question in the ticket›, and what doesn't exist at all.
> 5. Anything that looks broken or unused in this area.
>
> Start with a one-paragraph summary, then numbered findings grouped by the headings above. Say what you checked when you report something as missing.

Add the ticket's questions to item 4 one by one. Name the related canvases' plans too, so the agent can say what they already cover.

## Evidence rules for gap cards

A gap card goes up only with:

1. **Today:** what the code does, with path:line. Cite every location that matters, not just the first one found.
2. **A disconfirming check:** before posting, look for why the gap might be wrong. Is it handled in another module, a config value or a framework default? Is there a comment, test or commit explaining it? Grep the callers. If the check undercuts the gap, drop it or say what you found.
3. **A proposal** naming the flow and decision that handle it.

When the map reports something as missing, confirm it with one search of your own before it becomes a red card. "Nothing does X" is the claim most often wrong.

Bugs the map finds that the feature didn't cause become follow-up cards, with path:line and one line on what breaks.
