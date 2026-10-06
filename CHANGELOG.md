# Changelog

## 0.2.0 - 2026-10-06

Added a mandatory startup delegation decision and active use of sub-agents for
useful, clearly separable programming domains when the host supports them.
Reassess delegation after resuming, scope changes, and newly discovered domains.

Added focused orchestration guidance and an optional delegation packet covering
shared contracts, ownership, context/skill/tool access, dependency ordering,
resource limits, stale requirements, failed workers, and integrated verification.
Parent-side completion now accounts for returned work and remaining active writers.
Workers consider further splits but need explicit authority for nested delegation.

Updated the core skill, related references and packets, invocation metadata,
documentation, source attribution, packaging allowlist, and evaluation coverage.
Added eight behavioral scenarios, two activation cases, and structural regression
tests. Live host-level sub-agent behavior has not been benchmarked.

## 0.1.0 — 2026-10-06

Initial ClearMind release: a portable programming skill with quiet-product rules,
coherent integration checks, visual verification, deliberate engineering,
purposeful skill/MCP use, critical review, and short evidence-driven cycles.

Includes optional work/review templates, repository validation and packaging,
automated tool tests, behavioral evaluation cases, source attribution, and CI.
Host-level behavioral effectiveness has not yet been benchmarked.
