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

## Refactor in controlled steps

Distinguish changes that preserve observable behavior from changes that intentionally
alter it. Establish tests or characterization checks around the behavior that must
survive. Perform a small structural change, rerun the affected checks, then make the
behavioral change. Keep the distinction clear in the diff or work sequence without
requiring a commit per step.

Fix causes, not presentation of symptoms. Do not silence failures with broad catches,
null defaults, hidden retries, or arbitrary delays. Preserve actionable error
information and follow the project's error contract. Avoid leaking secrets or
internal diagnostics into user-visible messages.

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
