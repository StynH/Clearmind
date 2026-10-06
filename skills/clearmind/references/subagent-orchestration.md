# Sub-agent orchestration

## Make the startup decision real

The parent always asks: "Can I delegate this to sub-agents?" Read only enough task,
repository, and capability context to identify a useful split before committing to
substantial solo work. Revisit the decision after resuming, approved scope changes,
or a new cycle exposes another domain. This applies to investigation and review
as well as implementation.

Choose one outcome: delegate a bounded assignment now; stage it after an explicit
prerequisite; or keep it local for a concrete reason. In a larger task, retain the
choice and ownership in the existing plan. A trivial task needs only a brief
internal decision. Do not expose private reasoning or create a tracked planning
file just to demonstrate that the check happened.

Where a useful, clearly separable domain and authorized host capability exist,
actually dispatch the work. A sentence proposing a team is insufficient. If the
host lacks the capability or denies the call, continue safely with local work or
another available method and describe material limits accurately. Do not install
an orchestration service or change host permissions to satisfy this workflow.

## Find genuine boundaries

An assignment should have a bounded outcome, necessary context, an owner, explicit
dependencies, and an observable acceptance check. Split by responsibility and risk,
not by arbitrary file count or a fixed roster of impressive job titles.

| Situation | Useful delegation | Coordination required |
| --- | --- | --- |
| A defect may span client and server | Separate read-only reproduction and trace analysis | Parent reconciles evidence before choosing a fix |
| A feature has settled API and UI contracts | API implementation and UI interaction in separate owned surfaces | Agree fields, errors, state transitions, and interface ownership first |
| A data change has a separate migration risk | Focused compatibility and recovery review | One owner controls schema and migration ordering |
| A patch has security or regression risk | Independent read-only review or bounded test work | Supply the brief and an identified patch state |
| A correction touches one localized string | Local implementation and check | No useful split; do not create a team |

Folders can still be coupled through contracts or state. When the boundary is
unclear, delegate bounded discovery first. Keep final product placement, shared
interfaces, and cross-domain decisions with the parent until ownership is explicit.
Once a contract is stable, delegate suitable implementation; do not restrict all
workers to commentary when safe implementation work is available.

## Check the host, then form the smallest useful team

Use the host's actual agent discovery, spawn, messaging, wait, and stop mechanisms
where available. Verify identifiers and lifecycle results. Do not invent tool names,
pretend that a second persona is another agent, or report parallel execution when
work was performed sequentially.

Check whether workers share the worktree, tools, permissions, skill access, and
conversation context. Do not assume that the parent's MCP connections or loaded
skills are usable by a worker. Confirm the access needed for its assignment; pass
permitted relevant content when direct access is missing. Never forward credentials
or private material to an unapproved service.

Choose complementary workers and respect host concurrency, depth, and task budgets.
Reuse an appropriate existing worker when supported. The parent continues useful
non-overlapping work, including the critical path, while workers run. Do not repeat
the delegated investigation in parallel or wait idly when other useful work remains.
Focused inspection of returned evidence is still the parent's responsibility.

Nested delegation is off by default for an assigned worker. Each worker considers
possible splits, but returns proposals to its parent unless the assignment explicitly
authorizes descendants and supplies a bounded budget. Any authorized nesting must
respect the actual host limits and account for all descendant results before return.
ClearMind's startup rule must not cause recursive agent multiplication.

## Send a complete, compact assignment

Use the optional [delegation packet](../assets/delegation-packet.md) or the existing
task system. Include the original outcome and relevant user corrections, approved
decisions, rejected approaches, non-goals, repository rules, and acceptance checks.
Retain exact wording for sensitive constraints or approved UI copy.

Specify the worker's domain, deliverable, allowed edits and no-touch paths, shared
contracts, dependencies, starting state, and stop/escalation conditions. Identify
which skills it must load and which authorized tools can establish the result.
Include accessible file paths, approved design references, and evidence locations;
inspect actual renders for visual assignments. Supply the relevant content directly
if those references cannot be read in the worker's environment.

Provide enough surrounding workflow for sound judgment without copying unrelated
chat history. Require the worker to surface missing context or a boundary collision
before guessing or expanding scope. Workers follow ClearMind's quiet-product rules,
short verification cycles, critical review, and truthful evidence requirements.

## Prevent collisions and stale work

Assign one active writer per overlapping surface. The parent must obey the same
ownership rule. Shared DTOs, generated clients, lockfiles, migrations, routing, and
configuration need a named owner or serial access. Two cleanly separated branches
can still implement incompatible behavior; isolated worktrees do not settle design.

Use host-supported isolated worktrees or branches when appropriate and permitted;
otherwise use strict disjoint ownership or serial writes. Respect unrelated user
edits. Coordinate shared resources too: test databases, browser sessions, ports,
fixtures, caches, and generated output can race even when source files differ.
Run review against a stable snapshot or repeat checks invalidated by concurrent edits.

If a dependency is unfinished, label the assignment blocked or stage it behind that
prerequisite. Do not implement against an invented contract. A worker needing an
out-of-scope edit reports the reason and proposed handoff before changing it.

When the user changes direction, update the shared brief and notify affected workers.
Pause or cancel obsolete work through supported mechanisms; confirm a writer has
stopped before reassigning its files. Preserve useful partial results and unrelated
edits. Track which brief and source state each returned result used. Re-review stale
work against the current requirements instead of accepting its earlier verdict.

## Integrate and challenge every return

A return includes outcome, changed or inspected paths, relevant state identifier,
actual checks and results, inspectable evidence, assumptions, dependencies, and
unresolved gaps. Distinguish completed, partial, blocked, failed, and cancelled work.
A timeout or an empty response does not imply success.

Inspect the returned patch and material evidence against the assignment and original
brief. Resolve conflicting proposals using requirements, observed behavior, and
reproducible checks. Neither majority vote nor a confident specialist overrides the
evidence. An author checking its own patch is self-review; use another actual worker
for an independent review when appropriate, with read-only access by default.

Integrate accepted work in dependency order. Recheck shared contracts, end-to-end
behavior, regressions, UI fit, and relevant final renders on the combined state.
Workers passing isolated tests does not establish that the assembled feature works.
Rerun verification invalidated by integration or later edits.

Before closing, collect required returns or explicitly resolve their assignments.
Confirm active writers cannot still alter the claimed final state. Record accepted,
rejected, superseded, and incomplete work in the existing plan only as needed. If a
worker fails, inspect partial changes before retrying, resuming, or safely taking
over; never launch a competing writer against an unconfirmed running task.

The parent owns the final result and applies ClearMind's completion gate. Report
verified outcomes and material limitations without a team roster, invented sign-off,
or announcements in the product interface.
