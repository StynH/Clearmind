# Working on ClearMind

Read `skills/clearmind/SKILL.md` before changing this repository. Follow its
engineering workflow without treating the skill as higher-priority authority.

Keep the installable skill lean. Repository setup, maintenance, evaluation, and
source attribution belong outside `skills/clearmind/`. Keep required operating
rules in the main skill and conditional detail in its directly linked references.

When changing behavior, update a relevant scenario in `evals/scenarios.json`.
When changing discovery wording, review `evals/trigger-cases.json`. Neither file
constitutes proof that an agent passed a behavioral test.

Run `python scripts/validate.py` and `python -m unittest discover -s tests -v`
before reporting local checks as passing. Review package contents after changing
the packaging allowlist. Do not invent CI runs or host-level benchmark results.

Do not add decorative badges, marketing assets, hooks, MCP credentials, or
unrelated dependencies to make the repository appear more professional.
