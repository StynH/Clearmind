# Cycles and evidence

## Size the loop to the uncertainty

A cycle ends with an observation, not just a code edit. One small defect may need
one reproduce–fix–verify pass. A cross-layer feature may need an initial vertical
slice, an integration/failure-path slice, and final product verification. Choose
slices based on risk and feedback speed, not a fixed number of iterations.

At task start and after resuming or changing scope, perform the delegation check.
Reassess when a cycle exposes a new separable domain. For delegated slices, use
[Sub-agent orchestration](subagent-orchestration.md) and verify the combined result.

Keep plans proportional. For a typo, briefly decide that no useful split exists,
inspect the string, make the change, and check its affected use. Do not create a backlog, architecture decision, or reviewer team.
For a risky migration, define compatibility, data safety, deployment order, and
recovery before executing any authorized mutation.

## Preserve the brief across cycles

Keep one compact source of truth for the user outcome, constraints, decisions,
rejected approaches, acceptance checks, and current blockers. Update facts; do not
rewrite history to make the current patch look compliant. A later approved scope
change supersedes an earlier one explicitly, not silently.

Before resuming after context loss, reload the relevant brief and inspect the
current code/diff and evidence. Do not trust a summary that says “everything passed”
without identifying what passed against which state. Carry previous user feedback
into worker and reviewer packets so the same rejected idea does not return under
a new name. Preserve assignments, ownership, dependency order, and the brief/source
state used by active workers. Notify affected workers of scope changes; inspect
their lifecycle state before resuming or reassigning work after context loss.

## Match evidence to the claim

| Claim | Suitable evidence | Insufficient by itself |
| --- | --- | --- |
| A defect is fixed | Original reproduction now succeeds; targeted regression passes | A plausible patch |
| Code compiles | Relevant build/type command completed successfully | Editor shows no squiggles |
| Integration works | A real, scoped call exercises the relevant boundary and confirms the outcome | A mocked client passes |
| UI looks right | Opened final renders at relevant sizes/states, checked in context | CSS inspection or an unopened screenshot |
| UI is usable | Actual interaction, focus/keyboard checks, error/recovery path where relevant | A static image |
| A command passed | Completed command, exit status, and meaningful output for the final affected state | Started process, stale log, or assumed exit code |

Choose the least expensive check that can establish the claim. Run narrow tests
while iterating, then expand to the modules and boundaries plausibly affected.
A small isolated change does not require running every test in a huge monorepo;
a shared contract change cannot be verified with one local unit test. Explain
material omissions, not every irrelevant test you did not run.

## Keep evidence honest and fresh

Associate each important result with its command or tool action, relevant
environment, state/commit or cycle, result, and artifact location where available.
For uncommitted work, a cycle identifier plus confirmation of which files changed
since the check is sufficient; do not invent a commit hash.

If implementation changes after a check, rerun affected verification. A README edit
does not invalidate a runtime screenshot; a changed layout does. A green baseline
is not a green patch. Pre-existing failures remain visible; compare them carefully
before concluding a failure is unrelated.

A missing executable, missing credentials, or unavailable test service is a blocked
check, not a passing test and not proof the implementation is defective. Report
which dimension remains unverified and make the best safe progress available.

## Debug without thrashing

Write down the observed failure and the next falsifiable hypothesis. Change one
cause at a time where practical. If attempts keep failing, gather new evidence:
inspect the actual request, response, logs, state transitions, dependency version,
or minimal reproduction. Do not stack speculative patches until the symptom goes
away. Remove your obsolete experiments without discarding unrelated user work.

Never delete a failing assertion, disable validation, swallow an exception, or
increase a timeout solely to make the check green. A changed expectation requires
an actual approved behavior change. A flaky test needs investigation; retries are
not proof of correctness.

## Stop deliberately

Finish when the requested outcome and appropriate verification are satisfied.
Do not invent extra work to prolong the cycle. If blocked, provide the functioning
subset, evidence, unresolved check, and precise next action without claiming full
success or promising unstarted background work.

Example handoff:

> The filtered export now uses the same query as the table. The regression and API
> integration tests pass. I could not open the authenticated page in this environment,
> so the browser interaction and final layout remain unverified.

This is more useful than either “Done, fully tested” or a page of vague caveats.
