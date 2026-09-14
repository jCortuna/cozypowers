# Keyboard and focus

## Focus rings

Style `:focus-visible` - browsers show it for keyboard and assistive-tech focus and suppress it for mouse clicks. `outline: none` (or `focus:outline-none`) without a visible replacement strands sighted keyboard users.

Order of preference:

```css
/* 1. Keep the browser's ring; just add breathing room */
:focus-visible { outline-offset: 2px; }

/* 2. Custom ring when the design demands one - with a verified token */
:focus-visible {
  outline: 2px solid var(--focus-ring);
  outline-offset: 2px;
}
```

An `outline: 2px solid` with no color renders `currentColor`, which is not automatically visible against whatever the ring crosses. Check the whole perimeter against every adjacent color: component fills, page surfaces, images, gradients, hover and selected states. A token or brand color passes only when that rendered check does.

In `forced-colors: active`, keep the default adjustment or use a system color such as `Highlight`. `forced-color-adjust: none` freezes authored colors - use only after checking the control stays perceivable.

Use `:focus-within` when a wrapper should light up while an inner input is focused (a search field with an icon inside its border).

## Skip link

```css
.skip-link { position: absolute; inset-inline-start: -999px; }
.skip-link:focus { inset-inline-start: 16px; top: 16px; }
```

```html
<a class="skip-link" href="#main">Skip to content</a>
<header>...</header>
<main id="main">...</main>
```

Give in-page anchor targets `scroll-margin-top` (e.g. `80px` beneath a sticky header).

## tabindex

- `0` - joins the natural tab order; only for custom interactive elements that aren't natively focusable.
- `-1` - focusable from script only; for headings you move focus to, dialog containers, roving members.
- Positive values - never. They hijack the whole page's order. Fix the DOM order instead.

**Roving tabindex.** Tabs, menus, toolbars, and radio groups are one Tab stop. The active item has `tabIndex=0`, the rest `-1`; arrow keys move both focus and the `0` (wrapping).

```tsx
<div role="tablist">
  {tabs.map((tab, i) => (
    <button
      role="tab"
      tabIndex={i === active ? 0 : -1}
      aria-selected={i === active}
      onKeyDown={onArrowKeys}
    >
      {tab.label}
    </button>
  ))}
</div>
```

## Trapping and restoring focus

Prefer native `<dialog>` with `showModal()` - trap, inert background, and Escape come free. A custom overlay needs `role="dialog"`, `aria-modal="true"`, and a name via `aria-labelledby`, plus:

- On open: set `inert` on the background container; focus the first focusable element (for destructive confirmations, the *least* destructive action).
- On close: remove `inert`; return focus to the trigger, or the nearest logical container if the trigger is gone.
- `overscroll-behavior: contain` on the dialog so its scroll never scrolls the page.

## Keyboard patterns (ARIA Authoring Practices)

A role is a promise: `role="tab"` means users expect the full tab keyboard model.

| Widget | Keys |
| --- | --- |
| Dialog | Tab / Shift+Tab cycle inside, wrapping; Escape closes |
| Tabs | Arrows move between tabs (wrap); Home/End first/last; Tab exits to the panel |
| Menu button | Enter/Space/ArrowDown open and focus first item; ArrowUp opens on last; arrows navigate; Escape closes and refocuses the button |
| Disclosure / accordion | Header is `<button aria-expanded>`; Enter/Space toggle |
| Combobox | ArrowDown opens/enters the list; Enter accepts; Escape closes back to input; typing filters |
| Listbox / radio group | Arrows move selection; one Tab stop for the group |

Universal:
- Escape dismisses the most recently opened layer (tooltip → menu → dialog).
- Arrows within composite widgets; Tab between widgets.
- Tabs activate automatically on arrow focus when panels render instantly; manually (Enter/Space) when switching is expensive.
- Enter submits the focused input's form; in a `<textarea>` Enter is a newline and Cmd/Ctrl+Enter submits.

## Single-page app route changes

Client-side navigation resets nothing and announces nothing. On route change: update `document.title`, then move focus to the new view's `<h1>` (with `tabindex="-1"`) or `<main>`. Restore scroll on back/forward; scroll to top on forward navigation.
