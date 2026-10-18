# Search strategy: where your scout looks, and why

<!--
THIS IS THE PART YOU WRITE. The scout in SKILL.md executes whatever
queries and filters you define here. It ships empty on purpose: the
strategy is your judgment about where YOUR first contribution lives,
and a scan without authored queries is just someone else's defaults.

A filled strategy must contain:

1. At least one query in the Queries section. Each query is a real
   `gh search issues` invocation, and each should trace to a sentence
   of your fit profile in scope.md: if you cannot say which sentence
   produced a query, the query is probably not yours. Search breadth
   is the point at this stage: prefer generous limits and let the
   ranking filters do the narrowing.

2. At least one ranking filter in the Ranking filters section. A
   filter is a condition or an ordering over fields the search
   results already carry (last activity date, assignee presence,
   label set, comment count, repo). It must be checkable from the
   result fields alone: if deciding it would need opening the issue
   page, it belongs in your rubric, not here. Ranking is the free
   stage; keep it free. Make at least one filter an ordering, or
   state your tie-break: with drop conditions alone, the scout takes
   the top of whatever order the searches happened to return, and
   the graded candidates stop being traceable to you.

3. The top-N line, kept or deliberately changed.
-->

## Queries

<!-- Real gh search invocations, one per line, each with a comment
naming the fit-profile sentence it came from. Example SHAPE (write
your own; these values belong to nobody):

gh search issues --label "good first issue" --language python --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
-->


```bash
# Field 1, computer vision. "My target areas are computer vision and local models" + "built a computer vision pipeline in Python"
gh search issues opencv --language python --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr

# "built a computer vision pipeline in Python (YOLO, SAM2, ByteTrack)"
gh search issues yolo --language python --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr

# "an OpenCV project" + C++ as one of "my languages"
gh search issues opencv --language c++ --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr

# Field 2, local models. "local models (Ollama and llama.cpp style projects)" (any language)
gh search issues ollama --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr

# "writing C++ in a data structures course" + "llama.cpp style projects"
gh search issues llama.cpp --language c++ --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr

# "React/TypeScript" + "local models"
gh search issues ollama --language typescript --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr

# Field 3, bigger repos (500+ stars), pinned by name. "I'd like large projects (5,000+ stars) first ... mid-size projects (500 to 5,000 stars) are also welcome"
# Computer vision: lightly-train (object detection training), dimos (robotics perception)
gh search issues --repo lightly-ai/lightly-train --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
gh search issues --repo dimensionalOS/dimos --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
# Local models: llama.cpp, open-notebook, nanocoder (a local-model-friendly TypeScript coding agent), llama_index, llm-compressor, Megatron-LM
gh search issues --repo ggml-org/llama.cpp --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
gh search issues --repo lfnovo/open-notebook --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
gh search issues --repo Nano-Collective/nanocoder --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
gh search issues --repo run-llama/llama_index --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
gh search issues --repo vllm-project/llm-compressor --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
gh search issues --repo NVIDIA/Megatron-LM --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
# "self-contained logic with locally runnable tests" + "writing C++": a C++ numerics library
gh search issues --repo stan-dev/math --label "good first issue" --state open --no-assignee --limit 100 --json title,repository,labels,assignees,commentsCount,createdAt,updatedAt,url,authorAssociation,body -- -linked:pr
```

**How to run these queries.** Run each `gh search issues` line above as its own separate Bash command, one at a time, exactly as written (leave off the `#` comment lines). Do not chain them with `&&` or `;`, wrap them in a shell function or loop, write them to a script file, or use `mkdir` or `cd` first. An allow rule like `Bash(gh search issues *)` matches one plain command; a function, loop, or script makes the whole call unmatched, so a non-interactive scan is refused. Read each result from the command's own output.

Every query ends with `-- -linked:pr`. It tells GitHub to leave out issues that already have a linked pull request, which the result fields cannot show. The `--` is needed so `gh` treats the leading hyphen as part of the search and not as a flag. It only removes issues with a formally linked PR (a closing keyword or the sidebar link), not ones another PR merely mentions, so the rubric's "No open PR on the issue" check still reads the timeline.

## Ranking filters

<!-- Conditions and orderings over the free result fields, applied in
the order written. State each so a stranger could apply it and get
your ordering. Example SHAPES (write your own):

- drop any result with an assignee
- drop any result not updated in the last 60 days
- prefer fewer comments over more
-->

The queries fall into three fields, so one field cannot crowd out the others:

- **Computer vision:** the three queries that search `opencv` (Python), `yolo` (Python), and `opencv` (C++).
- **Local models:** the three queries that search `ollama` (any language), `llama.cpp` (C++), and `ollama` (TypeScript).
- **Bigger repos:** the nine queries pinned to one repository each with `--repo`, all with 500+ stars. I measured 973 open issues (82 at 5,000+ stars, 94 at 500 to 4,999) and found a median of 5 comments at large repos, 3 at mid-size ones and 0 under 500 stars. Any one ordering by comment count fills the list with tiny repos, so the size preference in the profile has to come from the queries. My first version pinned only 5,000+ star repos, but their "good first issue" labels mostly sit on issues more than a year old, so I widened the list to 500+ and chose repos that fit the profile.

Rules 1 to 5 are applied separately within each field, after merging that field's queries and removing duplicate issue URLs. Rule 6 orders what is left, and rule 7 picks the graded list:

1. Drop any result with an assignee (the `--no-assignee` flag should already do this; check anyway).
2. Drop any result not updated in the last 60 days (`updatedAt` before 2026-08-15 on a scan run in mid-October; recompute the cutoff as today minus 60 days on later scans). A stale issue is likely abandoned or already resolved.
3. Drop any result created more than 12 months ago (`createdAt` before 2025-10-15 on a scan run in mid-October; recompute as today minus 12 months). A recent update on a years-old issue is usually a bump, not a sign of life.
4. Drop any result with more than 3 comments in the computer vision and local models fields, and more than 8 in the bigger repos field. In a sample of 45 issues with 1 to 8 comments, about two thirds had a claim-like comment, so the cap of 3 stays where most repos are small. Bigger repos get a higher cap because their median is higher, and the rubric's "no comments expressing interest" check reads the thread for real claims.
5. Keep at most 2 results per repository in the computer vision and local models fields, taking the ones that sort first under rule 6. The bigger repos field has no per-repository limit, because its repos are pinned by name and I chose each one; a limit only throws away good issues from them (the first scan graded 9 of 40 survivors under a limit of 1).
6. Order the rest by these keys, each applied only to break ties in the one before it:
   1. Created in the last 30 days (`createdAt` on or after 2026-09-15 on a scan run in mid-October) ahead of older.
   2. Has a "documentation", "tests", "test", "docs", or "bug" label (any of them) ahead of none.
   3. A body of at least 300 characters that contains one of "done when", "acceptance", "expected", "steps to", "where to look", or "how to" ahead of a thinner body.
   4. Issue author's `authorAssociation` is OWNER, MEMBER, or COLLABORATOR ahead of anyone else.
   5. Fewest comments first.
   6. Most recently updated first.
7. Keep the top 2 of each field, then interleave the three lists (bigger repos #1, computer vision #1, local models #1, bigger repos #2, and so on). If one field has fewer than 2 survivors, fill the gap from the next-best result of another field.

Star count is not a field `gh search issues` returns, so it is not a ranking filter. The bigger repos field gets the size preference through its queries instead. Comment count is the last tie-break, not the primary order, because claims are checked by the rubric's "unclaimed" and "no comments expressing interest" checks, which read the thread.

## How many to grade

Grade the top **6** ranked results per scan: 2 from each of the three fields. I'm raising this from 5 on purpose, to keep the three fields balanced, and I accept the extra cost of about $0.20, which makes a scan about $1.20.

**Backfill on reject.** When a graded candidate is rejected, grade the next-ranked survivor in the same field in its place, so each field aims for 2 accepted issues. Prefer a different repository for the replacement: take the highest-ranked survivor in the field from a repository that has no candidate graded yet in this scan, and only if every remaining survivor is from a repository already graded, take the highest-ranked of those. If a candidate is rejected on a check about the whole repository (maintainers not active, push not recent, release not recent, or a contribution policy that forbids AI), skip every other issue from that repository, because they would fail the same check. A rejection about the single issue (an open PR, a claim comment, not one settled piece of work) does not rule out the repository's other issues. Stop backfilling a field when it has 2 accepted issues or no survivors left, and stop the whole scan after 10 backfilled candidates in total. I accept the worst case of 16 graded candidates, about $3.20 per scan. A typical scan costs less, because a candidate stops being checked as soon as it fails one check. I chose backfilling over raising the per-field count because most of the cost should go where candidates actually get rejected, which in the last scan was the bigger repos field (2 of 2 rejected).

<!-- Five is the default because grading is the only stage that costs
money: about $0.20 per candidate, so a scan is about $1, and you can
iterate the strategy several times for less than one full regression
run. You need one good issue, not ten. Raising this number is
allowed, but it is a decision you state here in a sentence, with the
cost you are accepting; it is not a number you bump because a scan
disappointed you once. -->
