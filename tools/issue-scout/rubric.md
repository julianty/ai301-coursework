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

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| Maintainers are active | Repo facts: last 5 default-branch commits (author names and dates) | At least one of the last 5 commits was authored by a human, or is a bot merge of a human's PR, within 90 days of the capture date. Bot-only housekeeping (dependency bumps, pre-commit autoupdates, generated-content commits) does not count. "No maintainer comment" entries in the maintainer first-response sample never fail this check by themselves | required |
| Push is recent | Repo facts: last push to any branch | Within last month from captured date | required |
| Release is recent | Repo facts: latest release | Within last 3 months from captured date | preferred |
| Issue is good first issue | Issue: labels | 'good first issue' label included | preferred |
| Issue filed by a human | Issue: the "opened by" line | The issue author is not a bot account (username ending in `[bot]`) | required |
| Issue is one settled piece of work | Issue: body_markdown and comment thread | Fails only if (a) the issue calls itself a tracking, umbrella, meta, or mega issue, or is a checklist of items meant to become separate PRs; (b) the thread contains an actual unresolved debate (people proposing competing approaches, or a maintainer questioning whether or how to do it) that no maintainer has settled; or (c) the issue itself leaves a required input or decision open that the contributor cannot supply (e.g. "asset TBD", "we need to decide X first"); or (d) the issue has been open more than a year and has 2 or more closed, unmerged PRs (repo facts linked PRs, or PRs mentioned in the thread): repeated abandoned attempts mean it is harder than it looks. Does NOT fail for: an issue no maintainer has replied to yet (silence is not a debate), a feature or regression request whose desired behavior is stated, even if phrased as a wish ("would be good if..."), an "etc." in a list of examples, several candidate causes in a bug report, several related files or pages to touch, or a short or unpolished body | required |
| Issue is unclaimed | Repo facts: assignees | No listed assignee | required |
| No open PR on the issue | Repo facts: linked PRs, plus any PR mentioned in the comment thread | No linked or mentioned PR is in the open state. Closed or merged PRs are not claims | required |
| Issue has no comments expressing interest | Issue comment thread — all comments | No comments in the last 6 months from capture date contain text expressing interest such as "I can take this" or "Working on it" | required |
| Contribution policy does not explicitly forbid AI usage | Repo facts: contribution policy | No explicit statement forbidding AI usage | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if every required check passes; preferred checks never change the verdict, they only rank accepted issues. Unclear counts as fail.
