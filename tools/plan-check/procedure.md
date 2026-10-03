# Procedure: how to grade a plan package

The rubric (`rubric.md`) says what to decide. The evidence guide
(`references/evidence-guide.md`) says where to look. This file says
what to do, in order.

## Read order

Read the evidence before the plan, so the plan is judged against the
facts instead of shaping how you read them. Take notes as you go; every
check grades from these notes.

1. **Issue.** Note the one behavior it reports and the version or build
   it targets.
2. **Thread highlights.** For each comment from the project's side
   (OWNER, MEMBER, COLLABORATOR, or a CONTRIBUTOR who proposes,
   chooses, or rejects an approach), write one line: what they found,
   asked for, chose, or ruled out. Also note any cause anyone proposes.
3. **Repo facts.** Copy the contribution policy line and match it to a
   row of the AI-policy table in the rubric. Note the template asks.
4. **Repro evidence.** Note the environment, the failing step, and each
   control run with what it showed. Then write a short list: **what
   the evidence rules out.**
5. **Candidate plan**, then **candidate plan comment.**

## Evidence gathering

For each check, collect these before grading:

| Check | What to write down |
|---|---|
| grounded-diagnosis | The plan's stated cause (quoted), next to the "rules out" list |
| bounded-scope | Each proposed change, numbered, marked needed or not needed for the fix |
| buildable-plan | Files and approach named; any phrase that defers a decision; the test, and which repro step it re-runs |
| thread-aware-comment | Each maintainer line from step 2, marked engaged or ignored by the comment |
| ai-policy-compliance | The policy row from step 3, and whether the comment has what that row requires |
| honest-certainty | Each strong claim, next to the artifact that backs it (or "none") |
| template-asks | Each template item, marked present, explained, or missing |

## Check execution

1. Grade the checks in rubric order, starting with grounded-diagnosis.
2. Grade every check, even after one fails. The output needs all seven.
3. Grade from your notes. Go back to the package only if a note is
   missing or two notes disagree.
4. Use only the rubric's pass condition. If a check passes but feels
   wrong, it still passes; mention the tension in the summary.
5. Use `unclear` only when the evidence is genuinely absent. Evidence
   that is present but bad is a `fail`.
6. In eval mode, the bundle is the whole world. Never look up the live
   issue.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required check
   passes; `unclear` counts as fail.
2. In the summary, name the deciding check. For a reject, quote the
   plan or comment line and the package fact it conflicts with. For an
   accept, say all required checks passed.
3. In live mode, add voice-guide notes and any gaps in this procedure.
4. End with the JSON block: all seven checks, each with a grade and a
   one-line evidence note, then the verdict.
