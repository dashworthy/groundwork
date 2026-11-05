# The review loop

Contents: handling an answer · the reply template · asking questions · proposals · when the user is confused · order

## Handling an answer

The user replies by ID ("G3. Yes", "agree", "Proposals for G7?"). For each answer:

1. **Check the code first when the answer names a pattern.** When the user names a kind of class or an existing convention, find an example in the project and name the new piece's class, folder, base class and how it's called, built like that example.
2. **Restate a loose answer** as one reading and say what else it could mean. Record your reading; don't wait.
3. **Update everything it touches in the same pass:** the card, every flow box and matrix cell, decisions, overview, glossary, Plan page. A stale flow beside an agreed card tells the next reader the wrong thing. List the knock-on cleanups in the reply.
4. **Name what a change gives up** when the user overrides a recommendation. They may still want it; now they know the cost.
5. **Mark it** green with the date stamp ([canvas-layout.md](canvas-layout.md#card-states)), lint, save.

When an answer adds new scope, check whether something already exists first. It often does, and the user may then move it somewhere better.

## The reply template

Each reply has these parts, in order:

1. **What changed**, in one line, ending "Lints are clean and the canvas is saved."
2. **The new state** of what changed, as a short list.
3. **The status table:**

   | Gaps | Status |
   |---|---|
   | G‹a›–G‹b› | ✅ agreed |
   | G‹n› | open, revisit later |
   | G‹x›–G‹y› | not yet reviewed |

4. **Still waiting on:** anything you need from the user, when there is something.
5. **Next:** "G‹n› (‹title›). ‹the proposal in one or two sentences›. Agree, or change?"

- The details show the new state, not the edit history.
- The status table appears in every reply. The user can't hold every gap's state in their head between turns.
- "Next" names one item and ends "Agree, or change?"

## Asking questions

- **One decision per question.** Two questions in one message get one answer and one confused reply.
- **Recommendation first, with its reason.** The user is choosing against a reasoned default, not refereeing.
- **2 to 4 concrete options**, mutually exclusive, no double negatives.
- **Make abstract questions concrete** with a short scenario using named people and places.
- Shaping decisions go through `AskUserQuestion`. Gap reviews go in the reply's "Next" line, since the user answers those by ID.

## Proposals

A request for proposals gets 2 or 3 genuinely different options, recommendation first, each with what it is, a pro, and a con with the guard that handles it. Include the cheapest credible option. If an earlier decision already settled part of it, say so first.

## When the user is confused

"I don't understand the ask" means the two of you hold different pictures. Find the assumption you don't share and name both designs side by side. Don't re-ask the same question louder. Once they pick, rewrite everything built on the other picture.

## Order

Go through items in order. When the user jumps ahead, answer what they sent, then come back to the skipped item as the next "Next". Never let an item fall out of the status table.
