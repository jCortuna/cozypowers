# Screen readers and semantics

## Rules of ARIA

1. If a native element has the semantics and behavior you need, use it.
2. Don't change native semantics unless you must.
3. Interactive ARIA controls must be keyboard-operable - a role promises the full keyboard model and states.
4. Never `role="presentation"` or `aria-hidden="true"` on a focusable element.
5. Every interactive element has an accessible name.

Screen readers trust your roles, so a wrong role is worse than none.

## Button vs link vs div

| Element | For | Why |
| --- | --- | --- |
| `<a href>` | Going somewhere / changing the URL | Free new-tab clicks, copy link, Enter |
| `<button>` | Actions: submit, toggle, open, delete | Free focus, Enter *and* Space, form semantics |
| `<div onClick>` | Nothing | No role, no focus, no keyboard |

A "button" that navigates is a styled `<a>`. Where native truly isn't possible, the polyfill is `role="button"` + `tabindex="0"` + Enter and Space handlers - which is why native is always less code.

## Landmarks, headings, titles

- One visible primary `<main>`. `<header>`, `<nav>`, `<aside>`, `<footer>` are landmarks users jump between.
- Repeated landmark types need labels: `<nav aria-label="Primary">`, `<nav aria-label="Breadcrumbs">`.
- Headings are structure, not styling - style a level with CSS rather than choosing the tag by size. Don't report one-h1 or skipped levels as a standalone WCAG failure without a concrete navigation or comprehension impact.
- `<title>` matches context, most specific first: `Billing · Settings · Product`.

## Accessible names

Precedence: `aria-labelledby` > `aria-label` > native label (label element, text content, `alt`) > `title`.

- Prefer visible text or `aria-labelledby` - `aria-label` is invisible, drifts from the UI, and translates poorly.
- Icon-only buttons: `<button aria-label="Close">` with the icon `aria-hidden="true"`.
- **Label in name** (WCAG 2.5.3): a button showing "Send" with `aria-label="Submit message"` breaks voice users saying "click Send".
- Names must exist even when the design has no visible label.
- `translate="no"` on brand names, code tokens, identifiers.

```tsx
<button><TrashIcon aria-hidden="true" /> Delete</button>
<button aria-label="Delete"><TrashIcon aria-hidden="true" /></button>
```

## Common ARIA mistakes

| Mistake | Why it fails |
| --- | --- |
| `aria-label` on a plain div/span | Mostly ignored on role-less, non-interactive elements |
| `<button role="button">` | Redundant noise |
| `aria-hidden` on or above focusable content | Tab stops that don't exist for screen readers |
| `aria-labelledby`/`describedby` to a missing id | Silently no name/description |
| `role="menu"` on site navigation | Promises app-menu arrow behavior; use `<nav>` + list |

## Visually hidden content

```css
.sr-only {
  position: absolute; width: 1px; height: 1px;
  padding: 0; margin: -1px; overflow: hidden;
  clip: rect(0 0 0 0); clip-path: inset(50%);
  white-space: nowrap; border: 0;
}
```

1px, not 0 (some readers skip zero-size elements); `nowrap` stops words running together. Never `display: none` or `visibility: hidden` for this - both remove content from assistive tech. Use it for context sighted users get visually ("Opens in new tab", table captions). Skip links un-hide on focus.

## Choosing how to announce a change

Stop at the first match:

1. **Focus moves there anyway** (opened modal, first invalid field) - the move is the announcement.
2. **Tied to a control** (field error, character count) - `aria-describedby`.
3. **Non-urgent, untied** (toast, "Saved", result count, loading) - `role="status"` (polite).
4. **Urgent, untied** (form-level failure, session expiry) - `role="alert"`.

## Live regions

| Mechanism | Politeness | For |
| --- | --- | --- |
| `role="status"` (polite, atomic) | Waits for a pause | Toasts, saved, counts, loading |
| `role="alert"` (assertive, atomic) | Interrupts | Urgent errors only |

- For repeated polite updates, render a stable empty region first, then change its text; inserting a fresh region with content is announced inconsistently.
- Inserted alerts usually announce but vary - test your target browser/reader pairs.
- Default to polite; overusing assertive is the most common mistake.
- Keep messages short and self-contained (atomic regions re-read entirely).
- Never move focus to a toast. Give toasts a generous timeout or dismiss button; never the only path to an action.
- Loading: `aria-busy="true"` on the updating region, announce "Loading..." politely, then the outcome ("Loaded, 12 results").

```tsx
<div role="status" className="sr-only">{statusMessage}</div>
```

## aria-hidden

Removes an element and its subtree from assistive tech - for decorative icons and visually duplicated content. Never on or above focusable elements; hiding something interactive means removing it from the tab order too.

## Alt text

| Purpose | Alt | Example |
| --- | --- | --- |
| Decorative / redundant with nearby text | `alt=""` (present but empty) | Logo beside the company name |
| Informative | The meaning it adds | `alt="Ticket QR code"` |
| Functional (image is the link/button) | The action or destination | `alt="Search"` |
| Image of text | The exact text (better: real text) | `alt="50% off everything"` |
| Complex (chart) | Short summary; full data nearby | `alt="Revenue by quarter, detailed below"` |

A missing `alt` is worse than empty - readers fall back to the file name.

## SVG and media

- Decorative SVG: `aria-hidden="true" focusable="false"`.
- Meaningful inline SVG: `role="img"` + `aria-label`, or a first-child `<title>` referenced by `aria-labelledby`.
- Simplest reliable option: `<img src="icon.svg" alt="...">`.
- Prerecorded video needs captions; audio needs transcripts. Never autoplay with sound; always render controls.
