# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity: no silent drift | The diff's changed files, read against the plan's scope and its deviation notes | Every changed file falls inside the plan's named scope, or is listed in the plan's deviation notes. Fails if the diff does work the plan does not mention. | required |
| description-fidelity: claims match the diff | The PR description's claims, read against the diff contents | Every behavior the description says the change adds or fixes is present in the diff. Fails if the description claims a fix the diff does not contain. | required |
| test-evidence: claims are observable | The test evidence, read against the plan's test plan | The behavior the plan's reproduction targets is shown with a before and after: the steps run, the observed result before, and the expected result after. Other results the test plan names (control runs, the integration test) must be stated with their result. A stated result without output is noted in the evidence line but does not fail this check. Fails if the reproduction has no before and after, or if a named result is missing entirely. | required |
| repo-checks-run | The test evidence and the description, read against the checks the repo's PR template or contributing docs name | Each check the template or contributing docs names is stated as run and passing, with its result where the test evidence gives one. Recorded output is not required. Fails if a named check is not mentioned, or if it was skipped without the description saying so. | required |
| no-unrelated-hunks: reviewable diff | The diff's changed files and hunks | Every hunk serves the plan's change. Fails on debris (stray files, commented-out code, unrelated formatting, leftover debug output). | required |
| template-sections-filled | The PR template's sections, read against the description | Every template section has content, or an explicit "not applicable" with a reason. Fails on any empty section or placeholder text. | required |
| disclosure-present-where-due | The PR template's disclosure section, read against the plan's deviation notes and the test evidence | Any known shortfall (a skipped test, a partial implementation, a deviation from the plan) is named in the disclosure section. Fails if a shortfall the evidence shows is absent from the disclosure. | required |
| description-states-scope | The PR description's opening lines, read against the diff | The description states what the change does and what it does not do, in terms the diff backs up. | preferred |
| commit-messages-describe-change | The branch's commit messages, read against the diff | Each commit message names the change it contains. | preferred |

## Verdict rule

Accept if every `required` check passes. Reject if any `required` check fails.
`preferred` checks never change the verdict.
`unclear` counts as fail. An unverifiable claim is a failing claim.

A PR that honestly discloses a shortfall can be accepted. Disclosure passes the
disclosure check. A shortfall that is disclosed does not, by itself, fail the
test-evidence or plan-fidelity checks.
