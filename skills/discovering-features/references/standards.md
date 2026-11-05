# Standards every feature is checked against

Run the feature through this list while drafting gaps. Each standard that applies becomes a gap card or a line in a flow; one that doesn't apply needs no mention. Project instructions override any of these.

1. **One resolver.** Every hard-coded default the feature changes is replaced by one shared rule, as a single class with an ordered fallback chain that ends in today's behaviour. Scattered reads of the old default drift apart the moment one caller is missed.
2. **Existing data.** A new required column is backfilled to today's default, so existing rows behave exactly as before. A new nullable column gets no backfill; null means "from before this feature".
3. **Changes say why.** Every change to where something is, or what state it's in, records a reason. Without one, an audit can say what changed but never why.
4. **Never block the field.** When what someone finds in the field disagrees with the record, trust the field, correct the record and open a discrepancy someone resolves later. A blocked user works around the system, and then the record is wrong and nobody knows.
5. **Map the automations.** List every existing automation the feature touches and show today against proposed before agreeing the flows. Automations fire in cases nobody pictures while designing the main path.
6. **Tenants differ.** When different customers want different outcomes, record each use case and tie the behaviour to a setting instead of picking one.
7. **The backend decides.** Before adding a client change (mobile, SDK, API callers), ask whether the client needs to know at all. Usually the server can resolve it from what the client already sends, and a client release is avoided.
8. **Lifecycle guards.** Records the feature depends on can't be deleted or merged out from under it.
9. **Permissions.** Every new action gets a permission and a role that holds it.
10. **Separate processes stay separate.** A new process gets its own model and flow instead of borrowing an existing one's types. Borrowing works until the two diverge, then every change to one breaks the other.
11. **Scope with the smallest control.** A per-page filter, unscoped by default, before a global switcher or saved context. A filter is not access control; say so if the user might read it that way.
12. **Extend pages before adding them.** Add a tab, grid or panel to an existing page, reusing a layout that already works, before proposing a new page.
13. **Follow the nearest convention.** New behaviour copies how the closest existing feature does the same thing (its naming, records, error handling), unless the user says otherwise.
14. **Out of scope stays out.** Nothing the user ruled out gets a column, branch, setting or hook "for later". Planning for it shapes the design around a feature nobody agreed to.
