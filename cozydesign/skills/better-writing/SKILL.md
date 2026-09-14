---
name: better-writing
description: Improve interface copy - consistent voice and terminology, tone matched to stakes, plain words, verb-first buttons, consistent flow vocabulary, descriptive links, one capitalization policy, positive toggle labels, fix-oriented errors, forward-pointing empty states, and placeholders as examples. Use when writing or reviewing UI text (buttons, labels, errors, empty states, toasts, settings, onboarding), when the developer asks for "better copy" or microcopy, and as the writing pass inside better-interface reviews.
---

# Better Writing

Clear and brief beats clever; consistent beats varied. The best error message is an interaction redesigned so the error can't happen.

How copy *renders* (capitalization via CSS, truncation, smart punctuation) belongs to **better-typography**; error markup and announcements to **better-accessibility**; room for translated strings to **better-layout**.

## Principles

### Learn the existing voice first

Read nearby copy before writing or reviewing: terminology, localization conventions, any voice or content guide. A deliberate brand voice isn't a defect - flag a departure from plain language only when it causes inconsistency, ambiguity, translation risk, or a tone the stakes don't support.

### One voice, tone that flexes

The product has one voice, set by its existing copy; a local edit doesn't invent a new one. Terms stay consistent - "Archive" in the menu is not "Move to storage" in the toast.

| Context | Tone |
| --- | --- |
| Success, onboarding, empty states | Warm; can be light |
| Routine actions, settings | Neutral, minimal |
| Errors, destructive confirmations | Calm, plain, no playfulness |
| Data loss, security | Serious, explicit |

### Speak to the reader

Instructional copy says "you", not "the user". In errors, "we" reads as ambiguous deflection - "Unable to load content" beats "We're having trouble loading this". An established first-person voice can stay in low-stakes copy. Go light on possessives ("Favorites", not "Your Favorites") and keep one perspective across a flow.

### Plain words

Words a tired reader gets first time; delete every word doing no work. No idioms, colloquialisms, or humor that won't translate. Avoid needless gender ("Subscribers can post recipes"). Match the device: "tap" on touch, "click" with a pointer, "select" when both apply.

Never build sentences from fragments around a variable (`"You have " + n + " new messages"`) - word order changes by language. Use a full template with proper pluralization.

### Buttons start with a verb

"Send", "Save draft", "Delete project" - never "OK!", "Let's go!", or bare "Yes"/"No" on a consequential action. Confirmation buttons repeat the consequence so the dialog can be answered without reading the body: "Delete this project?" → `Delete project` / `Cancel`.

### One vocabulary per flow

"Get started" to enter, one of "Continue"/"Next" to advance, "Done" to finish. Alternating synonyms makes people wonder whether the buttons differ.

### Links name their destination

Link text must make sense out of context (screen-reader users browse a list of links): "Read the billing docs", never "Click here". Multiple "Learn more" links get suffixes: "Learn more about exports".

### One capitalization policy

Choose title or sentence case per element type and apply it everywhere. Sentence case is the safer default - calmer, rule-free, localizes cleanly. "Save Changes" beside "Discard changes" reads as sloppy.

### Toggles describe the ON state

"Send read receipts", not "Don't send read receipts" (a double negative when off). Link directly to referenced settings instead of narrating the path ("Notification settings", not "Go to Settings > Notifications > Email").

### Errors say how to fix it, where it broke

| Bad | Good |
| --- | --- |
| That password is too short | Choose a password with at least 8 characters |
| Invalid name | Use only letters for your name |
| Oops! Something went wrong. | Unable to save. Check your connection and try again. |

Beside the failing field. No blame, no "oops", no exclamation marks. Phrase hints positively and show them before the mistake. If an error fires constantly, redesign the interaction rather than reword it.

### Empty states point forward

Say what this place is, how it fills, and offer one next action:

```html
<p class="font-medium">No projects yet</p>
<p class="text-sm text-zinc-500">Projects keep your tasks and files together.</p>
<button>Create a project</button>
```

Search/filter empties name the query and offer an exit: "No results for 'quarterly'. Clear filters". Never park persistent information in an empty state - it vanishes once content exists.

### Placeholders are examples

`name@example.com`, `DD/MM/YYYY` - a format hint, never the only label.

## Reporting (standalone)

**Severity.** HIGH: misleads the user or hides how to recover from an error. MEDIUM: breaks voice, terminology, or capitalization consistency. LOW: isolated wording polish.

**Verification.** Source is enough: every label against the action it triggers, every error for a stated fix, terminology against surrounding copy.

**Format.** Grouped by principle, severity-ordered, one row per root cause with all locations:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

End with **Block** (any HIGH) or **Approve**. Nothing found → "No actionable writing findings", plus verification.
