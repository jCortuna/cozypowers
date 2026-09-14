# Browser acceptance

Hands-on verification of a web artifact in a real browser.

## 1. Trigger gate

Run only when the developer explicitly asks for acceptance, browser QA/testing, responsive or cross-viewport checks, cross-browser inspection, visual regression, or interaction testing. "Build", "polish", "finish", "review the code", or "verify your work" get the lightweight self-check instead. A design critique request gets the critique guide, not this.

## 2. Pin down the contract

Infer before asking: entry URL or start command; critical routes/screens; the primary interaction path; viewports; target browsers if any; whether they want evidence, repairs, or a report only. Use the project's existing dev command and tooling - don't swap stacks or add a test framework without approval.

Default viewports when responsive checks are requested without targets:

| Name | Viewport |
| --- | --- |
| Small mobile | 390 x 844 |
| Tablet | 768 x 1024 |
| Small laptop | 1280 x 720 |
| Desktop | 1440 x 900 |

Fixed 16:9 artifacts: test the internal canvas plus at least one smaller outer viewport to prove the scaling doesn't distort.

## 3. Start safely

Check project docs/`package.json` for the intended command; reuse a running server if there is one; start the minimum process and wait for a genuine ready signal; note the real URL and build mode; never touch production services or external data.

## 4. Automated pass

**Runtime:** loads without fatal errors; no new actionable console errors (classify third-party noise, don't hide it); local assets, fonts, images, and primary requests succeed; no hydration mismatches.

**Layout:** no unintended horizontal overflow; nav, primary CTA, key content, dialogs, and controls reachable; text never clips, collides, or gets unreadably narrow; images keep their crop and focal point; fixed canvases scale without distortion.

**Interaction:** primary links and buttons do their job; focus is visible and ordered sensibly; forms show labels, validation, errors, and submit feedback; overlays open and close without trapping or losing the user; loading/empty/error/disabled states exercised where in scope and safely reachable.

**Motion and preferences:** animations finish and never block interaction; reduced motion preserves content and task completion; looping or autoplaying motion can be paused where the artifact requires it.

## 5. Visual pass

Capture screenshots at each requested viewport and critical state. Inspect hierarchy and focal order, spacing and alignment, token drift, repeated layout formulas, contrast and legibility, awkward folds, orphaned controls, accidental voids, and differences from supplied references. With a formal baseline, compare against it; without one, call it "visual acceptance", not "visual regression".

## 6. Repair loop (when fixes are authorized)

1. Record the failure and how to reproduce it.
2. Make the smallest causal fix.
3. Re-run the failed check at the same viewport and state.
4. Smoke-test nearby paths the change could affect.
5. Stop when the contract passes, or report the concrete blocker.

Report-only QA edits nothing and returns evidence-backed findings by severity.

## 7. Report

```text
Acceptance scope:
Environment / URL:
Viewports / browsers:
Paths exercised:
Passed:
Repaired:
Remaining issues:
Evidence:
```

Never claim browser acceptance from reading code. If the browser couldn't be driven, say exactly what was and wasn't verified.
