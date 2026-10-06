# Contributing

Keep ClearMind useful under a real programming workload. Prefer one precise rule,
a concrete example, or a focused reference over another page of repeated warnings.

## Make a change

Describe the failure the change addresses and the intended observable behavior.
Preserve the quiet-product rule, proportional cycles, evidence-based completion,
and purposeful skill/MCP composition. Keep the main skill below 500 lines and
2,200 whitespace-delimited words; this repository's word budget is a local guardrail,
not a claim about tokenizer counts or a universal Agent Skills requirement.

Put runtime instructions in the skill. Put setup, source attribution, and evaluation
material in the repository docs. Add no automatic hooks, implicit network access,
credential requirements, or forced framework migrations.

Install development dependencies, run the commands in the README, and inspect the
actual diff. If changing the validator or packager, add a regression test that
fails without the fix. Update `VERSION` and the changelog when preparing a release;
verify host-specific instructions against current primary documentation.

## Evaluate behavior

Add or adapt a scenario and its expected evidence. Keep evaluation fixtures fair:
the agent should not see the evaluator's answer key. Compare baseline and ClearMind
runs in fresh, equivalent environments when evaluating effectiveness. Report
failures and run counts, not just the best transcript. See `evals/README.md`.

Do not report schema checks, keyword searches, or self-review as behavioral
benchmarking. A new release can pass structural checks while remaining unevaluated
in an actual coding agent; state that plainly.

## Pull requests

Explain the behavior change, relevant scenario, commands actually run, and remaining
verification gaps. Avoid broad rewording mixed with functional changes. Review
comments should identify a concrete problem; optional preferences stay optional.
