# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives.**
- Eval mode: the plan-context block's scope pair (the files or boundary the
  plan names) and its deviation notes. Read the candidate PR's unified diff
  for the files and hunks actually changed. Read the candidate PR's
  description for its claims about what the change does.
- Live mode: `plan.md` in the working copy, in its scope list and its
  deviation notes. Read `git diff main...HEAD` for the changed files. Read the
  draft PR description for its claims.

**What good looks like.** Every changed file falls inside the plan's stated
scope, or is named in a deviation note. Every behavior the description says
the change adds or fixes appears in the diff. Silent drift is either direction
without a note: the diff does more than the plan, or the description claims
more than the diff delivers. An honest deviation that is written down re-ties
the mismatch and is not drift.

## Test evidence (harness category: not-tested)

**Where it lives.**
- Eval mode: the candidate PR's test-evidence section, read against the
  plan-context block's test plan and the reproduction steps it built on.
- Live mode: your captured test output, read against the test plan in
  `plan.md`. The repo's own check commands are named in the repo's
  CONTRIBUTING.md or README.

**What good looks like.** Each behavior the test plan names has a test or a
recorded run whose output shows it. Decisive evidence names the observable
behavior, states the expected result after the change, and shows the actual
output. "Tests pass" with no output, or output for a different test than the
one named, is not evidence. The repo's standard checks were run on this branch,
and their output is present. A skipped check is acceptable only if the
description names the skip and the reason.

## Diff quality (harness category: unreviewable)

**Where it lives.** The candidate PR's unified diff and its commit list in
eval mode. In live mode, `git diff main...HEAD` and `git log main..HEAD`.

**What good looks like.** Every hunk serves the plan's change, and the fix is
visible without scrolling through unrelated edits. Debris tells you the diff
is not reviewable: debug output or print statements left in, commented-out
code, stray files (editor backups, build output, notes), formatting churn in
lines the change does not touch, and drive-by edits to other files. Each
commit message names the change it contains.

## Standards and comms (harness category: standards-wall)

**Where it lives.**
- Eval mode: the repo-facts block's PR template sections, its contributing
  instructions, and its stated policy, including any AI-use disclosure rule.
  Read the candidate PR's description against those sections.
- Live mode: the repo's PR template (`.github/pull_request_template.md` or
  equivalent), its CONTRIBUTING.md, and its stated AI-use policy. Read your
  draft description against them.

**What good looks like.** Every template section has real content, or an
explicit "not applicable" with a reason. Placeholder text left in a section is
a failure. Any AI-use disclosure the policy asks for is present and says what
was done with the AI tool. A shortfall the evidence shows is named in the
disclosure section. Whether the description's claims match the diff is plan
fidelity, not this family.
