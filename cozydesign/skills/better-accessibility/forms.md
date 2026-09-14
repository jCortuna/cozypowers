# Forms

## Labels

Every control has a programmatic label - `<label for>` matching the input `id`, or a wrapping `<label>`. A placeholder is never a label: it vanishes on typing and usually fails contrast. A placeholder *alongside* a label may show an example format (`name@company.com`).

```html
<label for="email">Email</label>
<input id="email" type="email" autocomplete="email" />

<label><input type="checkbox" /> Send me updates</label>
```

The wrapping form gives label and control one hit target - no dead zone between checkbox and text. Mark required fields with native `required` plus a visible marker explained once per form.

## Errors

```html
<label for="email">Email</label>
<input id="email" type="email" autocomplete="email"
       aria-invalid="true" aria-describedby="email-error" />
<p id="email-error">Enter a valid email address.</p>
```

- `aria-invalid="true"` on the failing field; remove it when fixed.
- `aria-describedby` ties the inline error to the field so it's announced with it.
- Errors sit beside their field with text or an icon - never a red border alone.
- On submit, focus the first invalid field.
- Let incomplete forms submit so validation can surface.
- Accept free text and validate afterwards; never block keystrokes or filter characters live. Trim before validating - autofill and text expansion add trailing spaces.

## Autocomplete, type, inputmode

`autocomplete` with a meaningful `name` enables one-tap fill and is required (WCAG 1.3.5) for fields about the user.

| Field | `autocomplete` |
| --- | --- |
| Name | `name`, `given-name`, `family-name` |
| Email / phone | `email` / `tel` |
| Address | `street-address`, `address-line1`, `postal-code`, `country` |
| Card | `cc-number`, `cc-exp`, `cc-csc`, `cc-name` |
| Login | `username`, `current-password` |
| Sign-up / reset | `new-password` |
| 2FA code | `one-time-code` |

Section prefixes where relevant: `autocomplete="shipping street-address"`.

| Input | Use |
| --- | --- |
| Email / URL / phone | `type="email"` / `"url"` / `"tel"` |
| OTP, PIN, card number | `type="text" inputmode="numeric"` (text semantics, no spinner) |
| Money, decimals | `type="text" inputmode="decimal"` |
| True quantities | `type="number"` |

`spellcheck="false"` on emails, codes, and usernames. Never block paste. Stay compatible with password managers and 2FA autofill: a real `<form>`, correct tokens, no decoy inputs.

## Submitting

- Keep submit enabled until the request starts; then disable it with a spinner **beside the original label** ("Save" + spinner) so assistive tech knows which button is busy.
- Success → a polite live region. Failure → focus the first invalid field (that move is the announcement). `role="alert"` only for form-level errors not tied to a field.
- Warn about unsaved changes before navigating away; never lose typed input to a re-render (hydration must preserve focus and value).
- Enter submits from any input; Cmd/Ctrl+Enter from a textarea.

## Disabled states

Native `disabled` gives the complete platform behavior: out of the tab order, no activation, `:disabled` styling, excluded from submission. `aria-disabled="true"` only *announces* - it changes no focus, behavior, or styling.

- Don't disable submit buttons (see above).
- A natively disabled control gets no pointer events and no focus, so a tooltip explaining *why* never reaches keyboard or touch users. Put the reason in visible text nearby, or use `aria-disabled` so it stays focusable.
- With `aria-disabled="true"`: block pointer and keyboard activation in the handler, prevent submission, style it explicitly (including forced colors), and explain nearby.
- Never set both `disabled` and `aria-disabled`.
- Disabled controls are exempt from contrast minimums, but keep them legible.
