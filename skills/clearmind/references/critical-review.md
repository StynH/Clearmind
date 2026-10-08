# Critical review

## Review the outcome, not the author's confidence

Read the original brief, prior feedback, non-goals, and acceptance checks first.
Inspect the full relevant artifact and task diff. Do not begin with the author's
claims that the solution is elegant, correct, or complete. A tidy patch can still
solve the wrong problem; an ugly legacy boundary does not justify an unrelated
rewrite.

Use a genuinely separate reviewer for changes whose risk warrants it when that
capability exists. Send a review packet with actual context. On small changes,
perform a short self-review using the same criteria. Neither route guarantees
correctness; both require inspecting evidence. An implementing worker reviewing
its own changes is self-review. For separate review, give another worker the
current brief and a stable artifact state, with read-only access by default.
Disclose shared authorship or inspection limits; repeat checks invalidated by
later edits. Follow [Sub-agent orchestration](subagent-orchestration.md) for handoff
and lifecycle rules.

## Apply the relevant lenses

| Lens | Ask |
| --- | --- |
| Outcome | Does the user achieve the intended goal, beyond literal file edits? |
| Integration | Does it belong in the existing workflow and architecture? |
| Restraint | Is any copy, UI element, abstraction, dependency, or file gratuitous? |
| Correctness | What relevant edge case, state transition, or boundary could fail? |
| Cause | Does the repair restore the owning contract, or conceal a defect that remains active? |
| Evidence | What ran against the final state, and what is merely assumed? |
| Preservation | Did it revive a rejected idea or break surrounding behavior? |

Do not produce findings merely to fill every category. Focus on concrete defects,
missed requirements, and material risks. Keep optional improvements separate and
do not implement them as an unsolicited second project.

## Require actionable findings

For each material finding provide the violated requirement or behavior, affected
location, evidence/reproduction, consequence, and smallest reasonable correction.
Label uncertainty as uncertainty. Severity follows user impact, not rhetorical
force. A style preference is not a correctness defect.

Example:

> Export ignores the active filter. The table reads `filteredRows`, but the handler
> serializes the unfiltered collection. Filtering to one customer still exports
> all customers in the integration check. Use the authoritative filtered query and
> add the filtered-export regression.

Not useful:

> This needs to be more robust and follow enterprise best practices.

## Respond without groveling or defensiveness

Check the claim before agreeing. If valid, state the defect and correction plainly.
If false, cite the relevant code or runtime evidence and leave correct behavior
intact. If ambiguous, identify the missing observation and obtain it where possible.
Never say “You're right” as a substitute for analysis. Do not flatter the user,
apologize repeatedly, insult people, or protect the patch because you wrote it.

Examples of useful responses:

> The action is in the wrong scope: it changes one row but sits in the global
> toolbar. Move it into the existing row menu.

> That change would break the existing API contract. The endpoint returns 409 for
> this conflict, and the client already handles it. Keep the contract and fix the
> stale client state instead.

> The build passes. I have not verified the keyboard interaction, so that part is
> still unconfirmed.

## Adjudicate and recheck

Retain valid existing work. Address supported findings with the smallest coherent
change; do not restart from scratch because one review is negative. Re-run the
checks affected by the correction and re-review against the same brief. Preserve
previously settled constraints instead of drifting toward a new reviewer's taste.

If a correction creates a new regression, it is not an improvement. Stop the loop
when the outcome and relevant verification pass, not when reviewers run out of
new preferences or when the author feels tired of criticism.
