# Product and interface

## Start with the existing experience

Inspect the real route or screen, its neighboring screens, and the existing
components/design tokens before choosing placement. Follow the user's journey:
entry point, action, feedback, resulting state, and recovery. Read the code to
understand constraints, but use the running interface to judge the interface.

For a new product, establish a small coherent initial flow and inspect its first
working render before expanding. Do not compensate for missing requirements by
inventing dashboard cards, marketing copy, settings, or navigation sections.

## Make each addition earn its place

Before adding an element, identify its user purpose and natural scope. A row action
usually acts on that row; a table action acts on the current collection; a global
action belongs at application scope. Treat these as starting hypotheses and check
the actual product conventions. Prefer the existing action group over a new panel.

Check whether the new feature duplicates an existing capability, creates a second
source of state, hides a common action, or introduces inconsistent behavior across
similar screens. Do not trade a coherent workflow for local implementation ease.

Example: adding CSV export to a filtered table should answer which rows and columns
are exported, respect relevant permissions, and fit the table's action area. A new
“Data Export Center” card with an explanatory subtitle is not a default solution.

## Apply a copy admission test

For every new visible string, answer: where did this wording come from, and what
necessary user decision or action does it support?

| Situation | Expected treatment |
| --- | --- |
| Fix an incorrectly enabled Save button | Correct the behavior; do not add a “Save is now fixed” message |
| Add a requested action | Use its established or requested name, not an extra heading and subtitle |
| Fix a race condition | Correct state handling; keep technical explanations out of the product |
| Icon-only control has no accessible name | Add a concise semantic name; do not add promotional copy |
| Submission can fail | Preserve or add necessary, actionable error feedback in the existing pattern |
| Existing product uses “Saved” confirmation | Preserve normal outcome feedback; it is not an announcement about your work |
| User explicitly requests a release notice | Provide the requested notice; do not treat the quiet-product rule as a ban |

No generic “enhanced experience”, unnecessary feature badges, explanatory text that
only compensates for bad placement, or extra tooltips on already obvious controls.
Do not remove valid labels, error details, or feedback solely to reduce word count.
Use proper semantic HTML/components and the existing localization mechanism.

## Verify by seeing and using

Use the available browser, desktop, device, preview, or screenshot tools that fit
the application. Navigate to the actual changed view with representative data.
Compare before and after when possible. Open the captured output and inspect it.

Exercise the relevant normal, empty, loading, error, disabled, and success states;
choose states affected by the change, not an indiscriminate checklist. Consider
long content, narrow viewports, zoom, and theme variants when those are supported
or at risk. Look for clipping, jumps, overlap, misplaced emphasis, duplicated
controls, accidental visual redesign, and unnecessary text.

Use keyboard navigation, visible focus, appropriate names/labels, and sensible
focus restoration for affected interactions. A screenshot cannot establish screen
reader behavior; an accessibility tree cannot establish visual quality. Use the
right evidence for each dimension. Do not claim accessibility certification from
one automated scan.

Interact, not just inspect: trigger the action, confirm its result, and check that
state remains consistent after navigation or refresh where relevant. Use the
existing test stack for reproducible checks. Keep screenshot baselines stable
with controlled data, viewport, fonts, and animation where applicable. Inspect
changes before accepting a new baseline; never refresh snapshots blindly.

## When visual tooling is missing

Attempt the available preview or locally runnable test route within the task's
permissions. An unavailable browser integration may have a safe existing CLI
fallback; it does not justify silently abandoning visual checks. Do not install
new infrastructure or send private screenshots to a new service without approval.

If no real render can be obtained, implement cautiously using existing conventions
and complete the checks available. State that visual verification was not performed.
Do not substitute imagined appearance, a generated mockup, or source inspection for
a claim that the shipped UI was seen.
