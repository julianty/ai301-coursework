# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check                                                   | Evidence                                  | Pass condition                                                                                                                                                                                                                                      | Weight    |
| ------------------------------------------------------- | ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| Repo has recent activity                                | Repo facts: last 5 default-branch commits | All 5 commits within 3 months of captured date authored by non-bot                                                                                                                                                                                  | Required  |
| Repo has recent activity                                | Repo facts: last push to any branch       | Within last month from captured date                                                                                                                                                                                                                | Required  |
| Release is recent                                       | Repo facts: latest release                | Within last 3 months from captured date                                                                                                                                                                                                             | Preferred |
| Issue is good first issue                               | Issue: labels                             | 'good first issue' label included                                                                                                                                                                                                                   | Preferred |
| Issue describes one bounded, concrete change            | Issue: body_markdown                      | Names one concrete outcome/fix, even if delivered across several related subtasks or files; fails only if it bundles multiple unrelated changes, is an open-ended tracking list, or hinges on an unresolved design decision with no agreed approach | Preferred |
| Issue is unclaimed                                      | Repo facts: assignees                     | No listed assignee                                                                                                                                                                                                                                  | Required  |
| Issue has no comments expressing interest               | Comments:                                 | No comments in the last 6 months from capture date contain text expressing interest such as "I can take this" or "Working on it"                                                                                                                    | Required  |
| Contribution policy does not explicitly forbid AI usage | Repo facts: contribution policy           | No explicit statement forbidding AI usage                                                                                                                                                                                                           | Required  |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if every required check passes; preferred checks never change the verdict, they only rank accepted issues. Unclear counts as fail.
