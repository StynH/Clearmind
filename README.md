# ClearMind

A skill I made because of my annoyances with working with Fable and Astra.
This skill makes them actually think about what they're doing, be critical about their work, spread it out among sub-agents and prevents it from adding random text to your UI for no reason.

## Install

The installable unit is **`skills/clearmind/`**, not this entire repository and not
`SKILL.md` alone. Copy the complete folder to your host's skill directory.

| Host | Personal installation | Project installation |
| --- | --- | --- |
| Codex | `~/.agents/skills/clearmind/` | `.agents/skills/clearmind/` |
| Claude Code | `~/.claude/skills/clearmind/` | `.claude/skills/clearmind/` |

These paths follow the official host documentation checked on October 6, 2026;
see [sources](docs/sources.md). Other Agent Skills-compatible hosts can use the
same skill contents, but their installation and invocation behavior may differ.
The optional `agents/openai.yaml` provides Codex-facing display metadata; no
MCP dependencies or permissions are silently provisioned.

### PowerShell: personal Codex installation

Run from this extracted repository's root. The command refuses to replace an
existing ClearMind installation; review and back it up before an intentional update.

```powershell
$source = (Resolve-Path '.\skills\clearmind').Path
$target = Join-Path $HOME '.agents\skills\clearmind'
if (Test-Path -LiteralPath $target) {
    throw "ClearMind already exists at $target. Review it before replacing it."
}
New-Item -ItemType Directory -Path (Split-Path $target) -Force | Out-Null
Copy-Item -LiteralPath $source -Destination $target -Recurse
```

For a personal Claude Code installation, change `.agents` to `.claude` in the
`$target` line. For a project installation, copy into that project's path from
the table instead. No package manager or Python is needed to use the skill.

### Invoke and confirm loading

In Codex, use:

```text
$clearmind Fix the stale search results without redesigning the page.
```

In Claude Code, use:

```text
/clearmind Fix the stale search results without redesigning the page.
```

Start a fresh session if the installed skill is not discovered. Confirm ClearMind
is listed and that the agent actually reads its instructions. Automatic activation
depends on the host and model; explicit invocation is the clearest check. Copying
a folder does not prove activation or access to any MCP service.

To make it the default programming workflow in a project, add a short instruction
to the project's existing agent guidance that says to load the installed ClearMind
skill for programming tasks. Preserve the rest of that guidance; do not replace it.

## What it changes

**Quiet interfaces.** New text or UI elements need a real reason. A bug fix is not
an excuse for “Improved” badges, announcement panels, explanatory subtitles, or a
redesign. Necessary labels, accessible names, and useful interaction feedback stay.

**Engineering judgment.** Understand domain boundaries, reuse sound conventions,
refactor in safe steps, and reject abstractions built for imaginary requirements.
Judge a feature in the whole workflow, not just the component being edited.

**Observed results.** Use actual renders and interactions for UI work. Exercise
real boundaries when claiming integration works. Run appropriate checks against
the final affected state and explicitly identify verification gaps.

**Useful composition.** Discover and use relevant installed skills and MCP tools.
Verify integrations through real calls. Use every useful authorized capability,
not every unrelated server; no tool-call quotas or automatic installation.

**Deliberate delegation.** Always assess sub-agents before substantial work.
Dispatch useful, clearly separable domains when the host supports them, with
bounded ownership, shared contracts, relevant history, and acceptance checks.
Keep trivial or inseparable work local after the check. The parent inspects
every return and verifies the integrated result.

**Critical cycles.** Frame, inspect, implement a coherent slice, verify, review,
and adapt. Carry prior feedback into delegation. Reject both self-congratulation
and unsupported criticism. Stop when the outcome is verified, not when every
requested file was edited—and not after an endless polishing loop.

Read the [main skill](skills/clearmind/SKILL.md) for the complete contract.

### Sub-agent behavior in 0.2.0

The first planning decision is **"Can I delegate this to sub-agents?"** The agent
revisits it after resuming, changing scope, or discovering a new independent domain.
Routine authorized delegation does not require another user request.

For a feature with agreed API and UI contracts, the parent can delegate one surface
and implement the other, then exercise the combined workflow. For an uncertain
cross-layer bug, separate read-only investigations can establish where the cause
lives before anyone changes a shared contract. A localized typo stays local after
a brief assessment.

The [orchestration guide](skills/clearmind/references/subagent-orchestration.md)
covers assignment boundaries, dependency ordering, skill/tool access, conflicting
writes, changing requirements, failed workers, nested-agent limits, and integrated
verification. The optional [delegation packet](skills/clearmind/assets/delegation-packet.md)
provides a reusable handoff without adding process files to the target project.

ClearMind does not enable sub-agents or bypass host permissions. It uses the actual
capabilities exposed in the current session. A missing capability results in a
truthful local fallback. No agent configuration or new service is installed.

To update an existing installation, back it up and replace the complete skill
folder with `skills/clearmind/` from this release. Copying only `SKILL.md` would omit
the new orchestration reference and delegation packet.

## Repository layout

```text
skills/clearmind/   Installable skill, metadata, focused references, optional templates
scripts/           Repository validator and reproducible ZIP packager
tests/             Automated tests for the repository tools and package contract
evals/             Behavioral scenarios, trigger cases, and evaluation rubric
docs/              Design decisions, source attribution, and delivery verification
.github/           Validation CI, dependency updates, and contribution templates
```

The installed skill contains no executable code, hooks, external endpoints, or
mandatory tool installations. Repository tooling is separate from runtime guidance.

## Validate and package

Repository development requires Python 3.10+ and the pinned development dependency.
Run from the repository root:

```bash
python -m pip install -r requirements-dev.txt
python scripts/validate.py
python -m unittest discover -s tests -v
python scripts/package.py --output-dir dist
```

The packager validates the repository, runs the unit tests, and produces a full
repository ZIP, an installable skill ZIP, and SHA-256 checksums. It uses an explicit
allowlist and fixed ZIP metadata. Identical source produces identical bytes in the
same Python/zlib environment. It refuses symlinks and unintended overwrites.

The GitHub Actions workflow runs validation and tests on Linux and Windows with
Python 3.10 and 3.13. Those remote jobs run after publishing; they are not claimed
as executed in this delivery. See [verification](docs/verification.md) for the
checks actually performed and [evaluation instructions](evals/README.md) for
behavioral tests.

## Limits and trust

This is an instruction-based skill, not an enforcement engine. It cannot grant
tools, guarantee model compliance, supply an independent reviewer, or establish
code correctness by itself. Behavioral scenarios are included for real host-level
evaluation; their presence is not a benchmark result. Version 0.2.0 has
not been benchmarked in Codex or Claude Code.

Review unfamiliar skills and integrations before enabling them. ClearMind does
not authorize production writes, credential changes, repository uploads, or
unrequested installation. See [security](SECURITY.md).

## Maintenance and provenance

See [contributing](CONTRIBUTING.md), [design](docs/design.md),
[primary sources](docs/sources.md), and [changelog](CHANGELOG.md).
The wording is original; public specifications and professional repositories
informed its structure and workflow. ClearMind is not affiliated with or endorsed
by Martin Fowler, OpenAI, Anthropic, or the referenced repository maintainers.

Licensed under [MIT](LICENSE).
