# Engineering judgment

## Make the domain and boundaries legible

Trace the change through its real owners: presentation, application behavior,
domain rules, persistence, external systems, and deployment configuration as
applicable. Keep each rule near its authoritative owner. UI validation can improve
feedback, but it must not replace required server-side enforcement. Avoid multiple
independent implementations of the same business rule.

Read nearby working examples and project decisions. Reuse a sound convention even
when another pattern is fashionable. Challenge a convention only with a concrete
failure or a requirement it cannot serve. Do not migrate the whole codebase just
because the task exposed a different architectural preference.

## Prefer the simplest sufficient design

Favor explicit dependencies, understandable control flow, meaningful names, narrow
interfaces, and small units with clear responsibilities. Optimize for someone
safely changing the code later, not for displaying cleverness.

Before introducing an abstraction, identify the real variation or stable concept
it represents. Similar syntax is not proof of shared meaning. A little duplication
can be cheaper than coupling unrelated domain concepts. Conversely, a shared
business invariant should not drift across copied implementations.

Do not introduce speculative plugin systems, factories, generic repositories,
message buses, global state stores, or new services for a problem solved cleanly
inside an existing boundary. An extra library earns its cost through a current
need and demonstrated fit, not the phrase “industry best practice”.

YAGNI is not permission to omit required security, data integrity, accessibility,
or current operational needs. Minimal means sufficient, not fragile.

## Repair the cause at its owner

For a defect, reproduce the failure and trace the inputs, state transitions,
contracts, and dependencies until the failing mechanism and its owner are clear.
State the causal explanation and supporting observations in working notes. A
suspicious line, a plausible theory, or one successful attempt is insufficient.
Use a discriminating check when competing explanations remain; investigate before
editing rather than stacking speculative patches.

Choose a repair that restores the violated contract or invariant at that owner.
If a producer emits stale or invalid state, fix its ownership or ordering rather
than teaching each consumer to compensate independently. Inspect all affected
entry points and remove compensating code made obsolete by the repair. Keep
unrelated cleanup out of scope. A small edit can repair the cause; a larger
refactoring is justified only when necessary for the required behavior.

Reject changes that make the symptom disappear while leaving the mechanism active:
arbitrary sleeps to hide a race, automatic retries of an unsafe mutation, broad
catches that return success, hard-coded exceptions, forced reloads, duplicate state,
disabled validation, and a TODO promising the real fix later. Do not introduce a
temporary workaround for a requested repair or silently weaken the requirement.
If the owning system is inaccessible or a required contract cannot be changed,
report the blocker and unresolved cause; do not claim completion through a local
patch that conceals it.

Evaluate mechanisms by their purpose and evidence. Cancellation or response
ordering that enforces state ownership can be the actual fix for a race. Bounded
backoff for a documented transient failure, idempotency for repeated requests,
timeouts, and recovery controls can be durable parts of a correct contract. Their
presence alone does not make a workaround, and a ban on all defensive handling
would create new defects. Establish why the mechanism solves the demonstrated
failure and preserves valid behavior.

Verify the causal explanation as well as the visible result. Use a reproducing
regression check that fails before the repair and passes afterward when feasible.
Exercise the conditions that exposed the defect, relevant alternate entry points,
and repeated or adverse execution. A happy-path pass, elapsed delay, suppressed
error, or successful mock does not prove the underlying failure is gone. If the
cause remains uncertain, continue investigation or report that gap.

## Refactor in controlled steps

Distinguish changes that preserve observable behavior from changes that intentionally
alter it. Establish tests or characterization checks around the behavior that must
survive. Perform a small structural change, rerun the affected checks, then make the
behavioral change. Keep the distinction clear in the diff or work sequence without
requiring a commit per step.

Preserve actionable error information and follow the project's error contract.
Avoid leaking secrets or internal diagnostics into user-visible messages.

## Select relevant failure modes

Think across boundaries, but investigate risks proportional to the change:

- **State and concurrency:** stale responses, duplicate actions, cancellation,
  ownership/lifetime, optimistic concurrency, shared mutable state, retry safety.
- **Data and contracts:** nullability, validation, schema compatibility, query
  bounds, pagination, ordering, migration/backfill safety, serialization semantics.
- **Security and operation:** authorization at the real boundary, untrusted input,
  secret handling, resource cleanup, timeouts, observability, rollout/recovery.

Do not add infrastructure for every theoretical concern. Identify the concrete
risk, reuse existing safeguards, and verify the ones this change can affect.

For example, if a search component shows older results after a newer query, trace
request ordering and state ownership. Use an appropriate cancellation or response
freshness mechanism supported by the actual stack. Test out-of-order completion.
Adding an “Updating results...” label does not fix the race.

## Verify the real dependency contract

Inspect installed versions, lockfiles, public interfaces, and authoritative docs
before relying on unfamiliar behavior. Prefer the relevant documentation skill or
MCP capability when available. Confirm the returned documentation matches the
library/version in this repository. Never invent an API because its name seems
likely. Avoid upgrading packages as an incidental way to match remembered syntax.

Use the existing formatter, analyzer, test framework, build tooling, and dependency
injection conventions. For a .NET/Blazor codebase, for example, inspect its actual
component patterns and service lifetimes; do not introduce a mediator, mapper, or
another state system by habit. The same principle applies to every stack.

## Explain meaningful tradeoffs, not everything

Record a decision when it changes a public contract, creates durable architectural
coupling, affects data safety, or departs from established convention. State the
problem, chosen approach, credible alternative, and consequence briefly. Do not
create an architecture decision record for an ordinary local helper extraction.

Measure before claiming performance improvements. “Fewer lines” is not proof of
faster execution; a local benchmark is not proof of production-scale behavior.
