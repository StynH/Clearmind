# ClearMind

ClearMind is a programming skill for coding agents. It covers bug fixes, new features, refactoring, and code review.

I made ClearMind because I was tired of Fable and Astra adding random text to my UI. I wanted the agent to think about the whole application and check its work before calling it done. The skill also tells it to use relevant tools and delegate work when the task has useful boundaries.

[Install](#install) · [Usage](#usage) · [How it works](#how-it-works) · [Sub-agents](#sub-agents) · [Files](#files)

## Install

Copy the complete `skills/clearmind/` folder into your coding agent's skills directory. Keep its contents together: `SKILL.md` links to the bundled references and templates.

| Host | All your projects | One project |
| --- | --- | --- |
| [Codex](https://developers.openai.com/codex/skills) | `~/.agents/skills/clearmind/` | `.agents/skills/clearmind/` |
| [Claude Code](https://code.claude.com/docs/en/skills) | `~/.claude/skills/clearmind/` | `.claude/skills/clearmind/` |

Project paths are relative to the project root. `~` is your home directory.

Run either command from this repository's root to install for all your Codex projects. For Claude Code, change `.agents` to `.claude` in the destination path. Both commands refuse to replace an existing installation.

<details>
<summary>Windows (PowerShell)</summary>

```powershell
$source = (Resolve-Path '.\skills\clearmind').Path
$target = Join-Path $HOME '.agents\skills\clearmind'
if (Test-Path -LiteralPath $target) {
    throw "ClearMind already exists at $target. Review it before replacing it."
}
New-Item -ItemType Directory -Path (Split-Path $target) -Force | Out-Null
Copy-Item -LiteralPath $source -Destination $target -Recurse
```

</details>

<details>
<summary>macOS and Linux (Bash)</summary>

```bash
(
  set -eu
  target="$HOME/.agents/skills/clearmind"
  if [ -e "$target" ] || [ -L "$target" ]; then
    printf 'ClearMind already exists at %s. Review it before replacing it.\n' "$target" >&2
    exit 1
  fi
  mkdir -p "$(dirname "$target")"
  cp -R ./skills/clearmind "$target"
)
```

</details>

No build step or package manager is needed. Other Agent Skills-compatible hosts may load the same folder; check their documentation for installation and invocation.

## Usage

In Codex CLI or the IDE extension:

```text
$clearmind Fix the stale search results without redesigning the page.
```

In Claude Code:

```text
/clearmind Fix the stale search results without redesigning the page.
```

Check that ClearMind appears in the host's skill selector; start a fresh session if it does not. Automatic activation depends on the host and the task. Invoke it explicitly to check that it loads.

Give it the task and the constraints that matter. For example:

```text
$clearmind Add CSV export to the orders table. Export the currently filtered
rows, use the existing table actions, and preserve the current permissions.
```

```text
$clearmind Review the current diff for regressions. Keep the review read-only
and check it against the requirements and corrections already in this conversation.
```

For a project default, add this to the project's existing agent guidance without replacing the rest:

```text
Use the installed ClearMind skill for programming tasks in this repository.
Load its instructions before starting work.
```

### Updating or removing it

Back up any local changes, then replace the installed `clearmind/` folder with the complete folder from the new version. To remove it, delete that installed folder and any project instruction you added to invoke it. Start a fresh session afterward.

## How it works

ClearMind asks the agent to consider the surrounding application before editing. Adding CSV export means deciding which rows to export and where the action belongs. It does not automatically justify a new "Data Export Center" panel.

New UI text needs a reason: requested wording, an existing product convention, or a necessary interaction or accessibility requirement. Necessary field labels and error messages stay. An "Improved" badge added to advertise a bug fix does not.

For UI work, the agent should try the affected interaction in the running application and inspect the final render. Reading the CSS does not count as checking the layout. If it cannot obtain a real render, it must report that gap.

The engineering guidance favors small refactorings and sound existing conventions. New abstractions or dependencies need a current reason; unrelated cleanup stays out of the patch.

For defects, the agent must establish the cause with evidence and repair the boundary that owns it. Arbitrary delays, suppressed errors, duplicate state, and temporary workarounds do not count as repairs when the underlying defect remains. It should verify the original failure and related paths; an inaccessible cause stays an explicit blocker.

Implementation follows six steps:

1. Define the outcome and acceptance checks, including earlier feedback.
2. Inspect current behavior and record any existing failures.
3. Choose a small, coherent change and add a regression test where feasible.
4. Implement it and exercise the affected workflow.
5. Run the relevant checks and review the complete diff.
6. Fix supported problems and recheck, or close when the outcome is verified.

A localized fix may take one short cycle; a change spanning several layers may need more. Working notes belong in the existing task system or internal notes unless a handoff needs them.

Reviews must identify concrete problems. The agent should challenge unsupported criticism as readily as its own assumptions. Its final response should say what changed, what it checked, and what remains unverified.

## Sub-agents

Every programming task starts with the question: "Can I delegate this to sub-agents?"

When supported, the parent should delegate useful, separate responsibilities. With an agreed API contract, a worker might handle the UI while the parent implements the endpoint. An uncertain client/server bug can start with separate read-only investigations. A one-line correction can stay local.

Workers get relevant user feedback, owned files, shared contracts, and acceptance checks. The parent must check their access to context and tools. Loading a skill or connecting an MCP server in the parent does not establish worker access.

Each writable area has one owner. The parent inspects returned work and tests the combined result. Separate passing tests do not establish integration. Workers need explicit authority for nested delegation.

See the [sub-agent guide](skills/clearmind/references/subagent-orchestration.md) for the full handoff and integration rules.

## Other skills and MCP tools

At each task start, ClearMind tells the agent to inspect its host's skill and MCP inventories, then announce the relevant candidates and what it plans to use from each category. A claim about local file or test tools does not count as that check. It should read selected skill instructions and tool schemas, verify selected connections through relevant, low-risk calls, and use complementary tools where each fills a distinct need. Unrelated servers and duplicate calls add nothing.

It does not install services or change permissions. When a capability is missing, the agent should use an available fallback and report any verification gap. Your repository rules and the host's approval requirements still apply. See [skills and MCP](skills/clearmind/references/skills-and-mcp.md).

## Files

| Path | Contents |
| --- | --- |
| [skills/clearmind/SKILL.md](skills/clearmind/SKILL.md) | The main workflow and completion rules. |
| [skills/clearmind/references/](skills/clearmind/references/) | Detailed guidance for engineering, UI work, verification, review, tools, and delegation. |
| [skills/clearmind/assets/](skills/clearmind/assets/) | Optional work records, review packets, and delegation packets. |
| [skills/clearmind/agents/openai.yaml](skills/clearmind/agents/openai.yaml) | Codex-facing display metadata and a default prompt. |

The skill contains no executable scripts or hooks. References are loaded when relevant, and templates should only be used when they help with the task.

## Limits

ClearMind depends on the model following its instructions and the capabilities available in the session. It cannot enable sub-agents, supply missing tools, or guarantee correct code. Review the skill before enabling it, especially in a workspace with access to external systems.

Version 0.2.0 has not been benchmarked in Codex or Claude Code.

## Contributing

For a behavior issue or proposed change, include the original task, what the agent did, and the expected result. A reproducible example is more useful than a broad request to "be smarter." Remove private code and credentials from anything you share.

## License

[MIT](LICENSE).
