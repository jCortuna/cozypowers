# Review output format

The format for reviews orchestrated by better-interface. Domain skills used standalone have their own smaller format in their Reporting section.

## Scope and coverage

State the exact scope, the stack and styling conventions, the convention documents found during recon, and any review boundary. Then:

| Domain | Evidence inspected | Result |
| --- | --- | --- |
| Accessibility | Files, components, states, or checks | Findings count, or Clear |
| Layout | ... | ... |
| Writing | ... | ... |
| Typography | ... | ... |
| Colors | ... | ... |
| UI | ... | ... |

**Clear** = inspected with no actionable finding. **Not reviewed** must say why.

## Findings

One table, ordered by severity, then reach:

| Severity | Domain | Location | Before | After | Why |
| --- | --- | --- | --- | --- | --- |
| HIGH | Accessibility | `src/Dialog.tsx:42` | `<button><XIcon /></button>` | Add `aria-label="Close"`; hide the icon from the accessibility tree | Icon-only control has no accessible name |

- **Severity** from better-interface's ranking rules.
- **Location** as `path/to/file:line`; name the exact screen and component when there are no source files.
- **Before / After** in the same row - never separate "Before:" / "After:" lines.
- **Why** names the violated principle and the user impact.
- **Domain** is the owning skill without the `better-` prefix.

One row per root cause; list all locations of a systemic issue in that row. Respect the cap. With no findings, omit the table and write "No actionable interface findings."

## Verification

Each check or interaction, the exact command or steps, and the observed result. Separate passed checks from **Not verified** ones.

## Verdict

- **Block** - one or more HIGH findings remain; don't ship until fixed.
- **Approve** - no HIGH findings; MEDIUM and LOW stay in the table as work to do.

Approve claims the coverage you reported - never issue it for a domain you didn't inspect.

## Change-scoped reviews

When interface-review resolved the scope from version control, it supplies the scope block, a status on every finding, and its change-scoped format. Severity, ranking, cap, and verdict are the ones above, applied to `Introduced` and `Regression` findings only.
