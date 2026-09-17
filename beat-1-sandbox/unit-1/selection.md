# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

> https://github.com/codepath/pathreview-ai301-fa26-s1/issues/71

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```JSON
Summary

Repo-level facts (apply to all three): last 5 commits all by human author "Andrew Burke" within the last week — pass. Last push 2026-09-16 (yesterday) — pass. No releases ever (0 found) — preferred fail, doesn't affect verdict. No CONTRIBUTING.md/AGENTS.md/AI policy files found (404 on all) — silence passes per rubric.

All three issues: unassigned, 0 comments (no claim signals), no "good first issue" label.

┌────────────────────────────────────┬──────┬──────┬──────┐
│               Check                │ #71  │ #27  │  #2  │
├────────────────────────────────────┼──────┼──────┼──────┤
│ Repo alive (required)              │ pass │ pass │ pass │
├────────────────────────────────────┼──────┼──────┼──────┤
│ Unclaimed (required)               │ pass │ pass │ pass │
├────────────────────────────────────┼──────┼──────┼──────┤
│ No interest comments (required)    │ pass │ pass │ pass │
├────────────────────────────────────┼──────┼──────┼──────┤
│ AI policy not forbidden (required) │ pass │ pass │ pass │
├────────────────────────────────────┼──────┼──────┼──────┤
│ Bounded scope (preferred)          │ pass │ pass │ pass │
├────────────────────────────────────┼──────┼──────┼──────┤
│ Good-first-issue label (preferred) │ fail │ fail │ fail │
├────────────────────────────────────┼──────┼──────┼──────┤
│ Release recent (preferred)         │ fail │ fail │ fail │
└────────────────────────────────────┴──────┴──────┴──────┘

All three accept. Ranked by scope/complexity (no personal fit profile available): #71 (1–2 hr, single-file test/bug fix) is simplest and most bounded → best first pick; #27 (5–8 hr, adds a tone-check step across two files) and #2 (5–8 hr, new web parser + pipeline + schema changes across three files) are larger, multi-file features of similar size, with #2 slightly more complex due to introducing a new external-fetch parser.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/71",
    "checks": [
      {"name": "Repo has recent activity (commits)", "grade": "pass", "evidence": "Last 5 commits all by Aburke225, dated 2026-08-24 to 2026-09-16, well within 3 months"},
      {"name": "Repo has recent activity (last push)", "grade": "pass", "evidence": "pushed_at: 2026-09-16T21:48:27Z, within last month of capture date 2026-09-17"},
      {"name": "Release is recent", "grade": "fail", "evidence": "0 releases found in repo"},
      {"name": "Good first issue label", "grade": "fail", "evidence": "labels: ['bug', 'ingestion', 'tier-2'] — no 'good first issue' label"},
      {"name": "Bounded, concrete change", "grade": "pass", "evidence": "Body names one concrete fix: 'Remove the indentation' and remove the xfail marker, in two named files"},
      {"name": "Issue is unclaimed", "grade": "pass", "evidence": "assignees: []"},
      {"name": "No comments expressing interest", "grade": "pass", "evidence": "comments count: 0"},
      {"name": "Contribution policy does not forbid AI", "grade": "pass", "evidence": "No CONTRIBUTING.md, AGENTS.md, or AI policy file found (404s) — silence passes"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/27",
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/2",
    "checks": [
      {"name": "Repo has recent activity (commits)", "grade": "pass", "evidence": "Last 5 commits all by Aburke225, dated 2026-08-24 to 2026-09-16, well within 3 months"},
      {"name": "Repo has recent activity (last push)", "grade": "pass", "evidence": "pushed_at: 2026-09-16T21:48:27Z, within last month of capture date 2026-09-17"},
      {"name": "Release is recent", "grade": "fail", "evidence": "0 releases found in repo"},
      {"name": "Good first issue label", "grade": "fail", "evidence": "labels: ['enhancement', 'devops', 'ingestion', 'tier-2'] — no 'good first issue' label"},
      {"name": "Bounded, concrete change", "grade": "pass", "evidence": "Body names one concrete outcome: ingest a portfolio URL into the vector store, via one new parser plus pipeline/schema wiring in three named files"},
      {"name": "Issue is unclaimed", "grade": "pass", "evidence": "assignees: []"},
      {"name": "No comments expressing interest", "grade": "pass", "evidence": "comments count: 0"},
      {"name": "Contribution policy does not forbid AI", "grade": "pass", "evidence": "No CONTRIBUTING.md, AGENTS.md, or AI policy file found (404s) — silence passes"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

```
agreement: 12/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in clear-accept)
full results written to results.json
agreement: 5/8 scored items
agreement: 1/3 scored items
agreement: 3/3 scored items
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

> issue-20
> My rubric decided to accept issue-20, the gold label was reject.
> The issue passed all of my required checks, so it couldn't find a grounds to rject.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

> | Check                                        | Evidence             | Pass condition                                                                                                                                                                                                                                      | Weight    |
> | -------------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
> | Issue describes one bounded, concrete change | Issue: body_markdown | Names one concrete outcome/fix, even if delivered across several related subtasks or files; fails only if it bundles multiple unrelated changes, is an open-ended tracking list, or hinges on an unresolved design decision with no agreed approach | Preferred |

> The idea of having a bounded change is good to keep the scope small. <br>
> The reason why it's a preferred weighting is that the LLM incorrectly rejected many of the gold labeled accept issues. The threshold seems to be biased against 'list' as a possible issue. For instance, it flagged a list of suggested fixes from the issue as a rejectable criteria.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

> The check covers the scope-fit idea. This was the strongest case for rejecting issue-20. <br>
> 2-3 of the runs I did were iterations on this rule in particular. It was initally a Required rule, but rejected too many of the golden-labeled accept issues, so I demoted it to preferred. <br>
> The tradeoff for keeping it as is will be seeing issues that might lie out of scope and will eventually need to be rejected once I can read and understand the issue.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
   > I have some fun working with markdown (you might see this through the formatting I'm using) so working on markdown is within my interests. 1-2 hours is a good amount of time, I think (estimated effort is suggested in the issue post).
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
   > The directly verifiable criteria were all identified correctly, e.g. last push, latest release, so on.
   > I think that it won't be able to judge my capability in completing the issue successfully, but given that the estimated effort is around 1-2 hours, I think it is within my capability.
3. The anticipated difficulty in claiming it.]
   > Related to the last two points, it's within my interests, and relatively low effort <= 2 hours, I suspect I won't have too much difficulty.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
