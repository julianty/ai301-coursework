# Procedure: how this tool grades a PR package

## Read order

1. **Live mode only:** read `scope.md`. If the `Repo:` line is still the
   bracketed placeholder, stop and tell the student to fill it in. If the
   PR's target repo is not the scoped repo, stop and refuse to grade.
2. Read `rubric.md` in full. Note the checks, their weights, and the verdict
   rule before reading any evidence.
3. Read the plan: `plan.md` in live mode (its scope, boundary, test plan, and
   deviation notes), or the plan-context block in eval mode. Write down the
   scope list and the deviation notes. Do this before opening the diff, so
   the diff is read against the plan and not the other way round.
4. Read the diff: `git diff main...HEAD` in live mode, or the candidate's diff
   in eval mode. Write down every changed file and hunk.
5. Read the test evidence and the repo's check commands.
6. Read the PR title and description, then the PR template and the repo's
   contributing instructions (live mode: from the repo; eval mode: the
   repo-facts block).
7. Read the commit messages.
8. Read `voice-guide.md` in live mode only, and hold the title and description
   against it. Its findings go in the summary, not the verdict.

## Evidence gathering

Use `references/evidence-guide.md` to find each family. Record what you find
before grading anything.

- **Plan fidelity:** list each changed file and check it against the plan's
  scope list or a deviation note. Record files outside both. Then read the
  description's claims and record each one, with whether the diff contains it.
- **Test evidence:** pair each behavior in the plan's test plan with its test
  or recorded run. Record the repo's check commands and whether their output
  is in the package.
- **Diff quality:** scan every hunk for debris: debug output, commented-out
  code, stray files, formatting churn, unrelated edits. Record each one with
  its file and line.
- **Standards and comms:** list the PR template's sections and record whether
  each has content, "not applicable" with a reason, or placeholder text. Check
  the disclosure section against the known shortfalls in the deviation notes
  and the test evidence.

If the evidence for a check is absent from the package, record it as
"not present" and grade the check `unclear`. Do not search outside the
package in eval mode. In live mode, you may look in the repo for the
template or contributing instructions, and nowhere else.

## Check execution

Run the checks in rubric order. For each check:

1. Read the evidence you recorded for it.
2. Apply the pass condition from `rubric.md` to that evidence only.
3. Grade it `pass`, `fail`, or `unclear`. Write one line of evidence: the fact
   or quote that decided it.

A check can be graded without re-reading the whole package, as long as its
evidence was recorded in the gathering step. If a check needs evidence you did
not record, go back to the evidence gathering step for that family. Do not
grade from memory.

Grade `unclear` when the evidence is absent or when the pass condition cannot
be decided from it. Never grade `pass` on an assumption.

## Verdict assembly

1. Apply the verdict rule from `rubric.md`: accept if every `required` check
   is `pass`; reject otherwise. `preferred` checks never change the verdict.
   `unclear` on a required check counts as fail.
2. Pick the deciding check for a reject: the first `required` check, in rubric
   order, that is `fail` or `unclear`. Quote its evidence line in the output.
   For an accept, there is no deciding check.
3. Assemble the output: the per-check summary, then the fenced JSON block from
   `SKILL.md`, last, with nothing after it. Use the grades and evidence lines
   exactly as recorded.
4. Given the same grades, the verdict is always the same. Do not change a
   grade during assembly.

## Gaps

If this procedure does not say what to do at a step, report the gap in the
summary and stop at that step. Do not invent a step.
