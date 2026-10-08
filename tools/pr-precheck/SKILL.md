---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question about one PR package: is this pull request ready to
submit? A PR package is a candidate pull request: its title, description,
commits, diff, and test evidence. Read it against the plan it claims to
implement and the issue that plan belongs to. Do not grade anything else, do
not grade more than one package per run, and do not answer from impression.

## Inputs and modes

**Live mode** (the student's own submission, before it goes out). Read these
inputs:

- `plan.md` from the student's working copy, including its deviation notes.
- The branch's diff: `git diff main...HEAD`, run from the working copy.
- The draft PR title and description.
- The captured test evidence.
- The issue, read from the real repo.
- The repo's PR template and CONTRIBUTING.md, read from the repo.

A house-chain student reads the house plan and the house repro pack in place
of their own `plan.md` and issue. The same checks apply.

**Eval mode** (a package bundle). The bundle is the whole world. Fetch
nothing and read nothing outside it. Every fact comes from the bundle text.
Eval mode always grades every check under the full verdict rule.

## The scope seam (live mode only)

Before reading any other input in live mode, read `scope.md`.

- If the `Repo:` line is the unfilled placeholder `<ORG>/<PATH-REVIEW-REPO>`,
  stop without grading. Tell the student to fill in the `Repo:` line in
  `scope.md` with their section's Path Review repo. Do not guess a repo.
- If the PR targets a repo other than the scoped repo, refuse to grade it.
  Say which repo the PR targets and which repo the scope names.
- If the scope is valid, use its house rules as the context for the checks.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

Read `voice-guide.md` and hold the draft PR title and description against it.
Report any rule the draft breaks in the summary, quoting the rule and the
passage that breaks it.

A voice finding never changes the verdict on its own. Only a `rubric.md`
check that reads the voice guide can change the verdict. Ignore
`voice-guide.md` in eval mode.

## Component reads

- `rubric.md` defines the checks, their pass conditions, their weights, and
  the verdict rule. It decides the verdict.
- `procedure.md` defines the steps: read order, evidence gathering, check
  execution, and verdict assembly. Execute it as written.
- `references/evidence-guide.md` maps where each evidence family lives in a
  package and what good looks like there. Use it to find evidence.

If `procedure.md` is silent on a step, report the gap in the summary and stop
at that step. Do not improvise a step.

If `rubric.md` or `procedure.md` has no content, refuse to grade. Say which
file is empty and that the tool cannot grade without it. Do not invent checks
or steps.

## Verdict and output

The verdict is binary: `accept` (ready to submit) or `reject` (hold). Do not
use any other verdict. Reservations belong in the evidence lines of the checks,
not in the verdict.

Write a readable per-check summary first. Then end your reply with the fenced
JSON block below. The block must be valid, must be the last thing in the
reply, and must have nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

Fill `item` with the PR URL in live mode, or the bundle id in eval mode. Give
one entry in `checks` for each rubric check, in rubric order, with the grade
and evidence line from check execution. Set `verdict` from the verdict rule in
`rubric.md`.

## Grading discipline

- **Evidence first.** Grade no check without naming the fact or quote that
  decided it. Write that fact in the check's evidence line.
- **Grade the thing, not the polish.** Read the diff, the test evidence, and
  the claims against the plan. Do not grade formatting, length, or confidence
  of tone, except where a rubric check names them.
- **The rubric decides.** If a check passes its stated condition but seems
  wrong, it still passes. Report the concern in the summary. Do not change the
  grade.
- **The procedure decides how.** Follow `procedure.md`. Report its gaps. Do not
  add steps.
- **Unclear defaults to fail.** Grade `unclear` when the evidence is absent or
  the condition cannot be decided from it. Under the verdict rule, `unclear` on
  a required check is a reject. An unverifiable claim is a failing claim.
- **Honest disclosure is not a failure.** A PR that names its shortfall in the
  disclosure section can be accepted. Do not reject a PR for disclosing what it
  did not do.
