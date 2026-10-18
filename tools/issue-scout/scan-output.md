# Scan 1 (2026-10-15): first strategy, 6 candidates, ranked fewest comments first

I ran the scan and graded the top six. Five were accepted and one was rejected. I couldn't write `scan-notes.md` because the write needed permission I didn't have, so the friction notes are at the end of this message instead.

## Ranked read-out

Accepted, in fit order. Every issue was surfaced by the query named in its line:

1. **cairn-kb/cairn#13** — `cairn model --provider <unknown>` gives a misleading error instead of naming the valid providers.
   - **Surfaced by:** query 3 (ollama, any language). It was ranked #1 of the local-models field because it has 0 comments and was updated 2026-10-15, the most recent.
   - **Fit:** it's an input-validation fix in TypeScript, and the issue's acceptance criteria require a test for the new error.
   - **Check results:** a human maintainer (Qwertic) committed within hours, and v0.7.0 shipped today. There are no open PRs and no AI ban.
2. **openapi/gknowledge#19** — detect a local Ollama server and offer its models in Preferences.
   - **Surfaced by:** query 3. It's local-models #3 (0 comments, updated 2026-10-14).
   - **Fit:** the issue points to the exact file (`gknowledge/ui/preferences.py`), and `make test` runs locally. The CONTRIBUTING file welcomes AI-assisted work, with disclosure and understanding of the code required.
3. **pyronear/pyro-train#32** — add CodeCarbon to the YOLO training stage.
   - **Surfaced by:** query 2 (yolo, Python). It's CV #3 (0 comments, updated 2026-10-02).
   - **Fit:** it matches your YOLO background. It ranks below the others because it's DVC pipeline work that needs AWS credentials, and the repo has no release (that preferred check fails).
4. **openapi/gknowledge#5** — the parent of #19, with the same work and a one-line body.
   - **Surfaced by:** query 3. It's local-models #2 (0 comments, updated 2026-10-14).
   - **Fit:** take #19 instead; the two overlap.
5. **Thakay/sako#2** — try SAKO in Gemini CLI and record the result.
   - **Surfaced by:** query 2. It's CV #1 (0 comments, updated 2026-10-05).
   - **Fit:** the rubric accepts it, but it's a manual interactive trial that ends in one docs row, so it's judged by feel. That is what your profile ranks lowest.

Rejected:
- **Kiraliang954321/Industrial-Part-Pose-Detection#1** fails "Issue is one settled piece of work". It's a recruiting post that lists five separate "Starter tasks" and several contribution areas.
  - **Surfaced by:** query 2. It's CV #2 (0 comments, updated 2026-10-03).

## Friction for `scan-notes.md`

- All six candidates are in repos with 0 to 16 stars. Your profile wants 5,000+ (or at least 500) stars first, but star count isn't a search field and no rubric check covers it. Consider a preferred rubric check or a strategy filter for repo size.
- Rule 5's tie-break puts recency before label, so the label preference never applied.
- The ollama query returned about 90 survivors, versus 7 or fewer for each CV query, and `llama.cpp` with C++ returned none.
- Two accepted candidates are duplicates of each other (gknowledge #5 and #19), and the rubric has no duplicate check.
- You should claim the issue upstream the moment you commit to it. For gknowledge#19, its body says to comment on the issue to claim it.

```json
[
  {"item":"https://github.com/cairn-kb/cairn/issues/13","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"Qwertic (human) committed 2026-10-15; 5 recent commits"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-15"},
    {"name":"Release is recent","grade":"pass","evidence":"v0.7.0 on 2026-10-15"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"labels include 'good first issue'"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"author Qwertic, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"one fix with explicit acceptance criteria; no comments, no debate"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"no open PRs in repo; none linked or mentioned"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"CONTRIBUTING.md and AGENTS.md have no ban; AGENTS.md exists"}
  ],"verdict":"accept"},
  {"item":"https://github.com/openapi/gknowledge/issues/19","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"francescobianco (human) committed 2026-10-15"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-15"},
    {"name":"Release is recent","grade":"pass","evidence":"v0.2.2 on 2026-10-13"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"labels include 'good first issue'"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"author francescobianco, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"one bounded UI change; 'Where to look' file named; 0 comments"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"open PRs #30, #31 are unrelated (Flatpak, re-ingestion); none mentions the issue"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"CONTRIBUTING.md: 'AI-assisted contributions are welcome'"}
  ],"verdict":"accept"},
  {"item":"https://github.com/pyronear/pyro-train/issues/32","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"MateoLostanlen (human) merged PR #36 on 2026-10-13"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-13"},
    {"name":"Release is recent","grade":"fail","evidence":"releases/latest returned 404; no release"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"labels include 'good first issue'"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"author MateoLostanlen, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"single 'Done when' list for one pipeline stage; 'part of the epic' is a child, not itself an umbrella"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"open PR #34 unrelated; no CodeCarbon PRs found"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"no CONTRIBUTING; repo ships CLAUDE.md for AI agents"}
  ],"verdict":"accept"},
  {"item":"https://github.com/openapi/gknowledge/issues/5","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"francescobianco (human) committed 2026-10-15"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-15"},
    {"name":"Release is recent","grade":"pass","evidence":"v0.2.2 on 2026-10-13"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"labels include 'good first issue'"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"author francescobianco, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"'Probe localhost:11434 and prefill the endpoint' states the desired behavior; #19 is the narrower child (overlap noted)"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"open PRs #30, #31 unrelated"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"CONTRIBUTING.md: AI-assisted contributions welcome"}
  ],"verdict":"accept"},
  {"item":"https://github.com/Thakay/sako/issues/2","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"Thakay (human) committed 2026-10-05"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-05, within a month"},
    {"name":"Release is recent","grade":"pass","evidence":"v0.5.1 on 2026-09-30"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"labels include 'good first issue'"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"author Thakay, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"one trial plus one docs row, with step-by-step instructions and acceptance criteria"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"no open PRs in repo"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"AGENTS.md written for agents; requires Co-authored-by trailers for AI tools"}
  ],"verdict":"accept"},
  {"item":"https://github.com/Kiraliang954321/Industrial-Part-Pose-Detection/issues/1","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"5 commits 2026-09-29 to 2026-10-03, human-style messages (author login blank)"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-03"},
    {"name":"Release is recent","grade":"fail","evidence":"releases/latest returned 404; no release"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"labels include 'good first issue'"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"author Kiraliang954321, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"fail","evidence":"'Starter tasks' lists 5 separate tasks (dataset QA, CV baseline, Recipe Wizard schema, ...) plus 8 contribution areas"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"unclear","evidence":"not checked; verdict already decided"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"unclear","evidence":"CONTRIBUTING.md not read; verdict already decided"}
  ],"verdict":"reject"}
]
```


---

# Scan 2 (2026-10-15): three fields, new order, 12-month drop rule, 6 candidates

I ran all 15 queries separately and graded the top 6. Four candidates are accepted and two are rejected.

**Funnel:** the three fields had 174 (computer vision), 243 (local models) and 92 (bigger repos) unique issues. After the ranking filters 15, 94 and 9 were left. I graded the top 2 per field.

**Accepted, in fit order**
1. **adivishall/two-wheeler-safety #21**, API input validation. It came from the `opencv` Python query and ranked on: created in the last 30 days, `bug` label, "acceptance" and "how to" in the body, owner as author, 0 comments. The best fit for your profile: input checks with locally runnable pytest tests, in a CV app. It has no release, which only costs it a preferred check.
2. **gabe-santana/saccade #22**, minimal examples including Ollama. It came from the `ollama` query and ranked on: created Oct 7, `documentation` label, "Done when" in the body, owner as author, 0 comments. Python docs and examples for a local-model workflow, with a recent v0.1.0 release. The CONTRIBUTING file says to comment before starting.
3. **hoslift/ranu.js #174**, a local Ollama and Docker docs recipe. It came from the `ollama` TypeScript query and ranked on: `documentation` label, "acceptance" in the body, member as author, 0 comments. Docs-only and low-risk. The repo has an `AGENT.md` and no AI ban.
4. **Thakay/sako #2**, trying SAKO in Gemini CLI. It came from the `yolo` Python query and ranked on: created Oct 5, `documentation` label, "expected" in the body, owner as author, 0 comments. It passes the rubric but fits least: it is a manual trial that needs Gemini CLI and a long step list, and the contribution is one table row. The repo explicitly welcomes AI-assisted PRs.

**Rejected**
- **Nano-Collective/nanocoder #1692** (`nanocoder` query, `--repo` pin): fails "No open PR on the issue". Open PR #1694 by Zaygal fixes this exact bug.
- **lfnovo/open-notebook #1451** (`open-notebook` query, `--repo` pin): fails "no comments expressing interest". VirenSumbly asked on Oct 4 to be assigned, and no maintainer has replied.

**Friction for the strategy**
- The computer vision and local-model winners are all tiny repos (0–2 stars), so the size preference in your profile isn't reaching those fields.
- Both bigger-repo picks were rejected. Under the one-per-repo rule, the next candidates (lightly-train #982 and llama_index #23339) were not graded.
- Two of your 15 queries came back empty or nearly so: llm-compressor returned about 1 KB, and Megatron-LM returned only a few issues.

If you commit to one, the scope rules say to claim it on the issue right away.

```json
[
  {"item":"https://github.com/adivishall/two-wheeler-safety/issues/21","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"Last 5 commits by adivishall, newest 2026-09-17"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-02"},
    {"name":"Release is recent","grade":"fail","evidence":"No releases (404)"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"Labels: bug, good first issue"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"Author adivishall, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"One theme (boundary validation) with a table and acceptance criteria; no debate"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"Only cross-reference is open issue #15, not a PR"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"No CONTRIBUTING or AI policy file"}],
   "verdict":"accept"},
  {"item":"https://github.com/gabe-santana/saccade/issues/22","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"gabe-santana merged PRs #27 and #28 on 2026-10-08"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-11"},
    {"name":"Release is recent","grade":"pass","evidence":"v0.1.0 on 2026-10-07"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"Labels: documentation, good first issue"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"Author gabe-santana, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"Three example files plus README, with a 'Done when' checklist"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"Timeline shows no cross-referenced PRs"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"CONTRIBUTING.md has no AI restriction; AGENTS.md and CLAUDE.md present"}],
   "verdict":"accept"},
  {"item":"https://github.com/hoslift/ranu.js/issues/174","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"Last 5 commits by draj256, newest 2026-10-10"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-15"},
    {"name":"Release is recent","grade":"pass","evidence":"v0.1.6 on 2026-10-10"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"Labels: documentation, good first issue"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"Author draj256, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"Single docs section with a task list and acceptance criteria"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"No cross-references; open-PR search returned []"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"CONTRIBUTING.md has no AI ban; AGENT.md present"}],
   "verdict":"accept"},
  {"item":"https://github.com/Thakay/sako/issues/2","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"Last 5 commits by Thakay, newest 2026-10-05"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-05"},
    {"name":"Release is recent","grade":"pass","evidence":"v0.5.1 on 2026-09-30"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"Labels: documentation, good first issue"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"Author Thakay, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"One trial and one docs row, with acceptance criteria; no open decisions"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"No cross-references on the timeline"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"pass","evidence":"CONTRIBUTING.md: 'Pull requests made with AI tools are welcome'"}],
   "verdict":"accept"},
  {"item":"https://github.com/lfnovo/open-notebook/issues/1451","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"lfnovo commits on 2026-10-05"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-13"},
    {"name":"Release is recent","grade":"pass","evidence":"v1.15.0 on 2026-10-04"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"Labels include good first issue, ready"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"Author lfnovo, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"Single 409 fix with acceptance criteria"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"pass","evidence":"No PR linked or mentioned"},
    {"name":"Issue has no comments expressing interest","grade":"fail","evidence":"2026-10-04 VirenSumbly: 'I'd like to work on this issue... Could you assign this issue to me?'"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"unclear","evidence":"Not checked: the issue was already rejected on the claim comment"}],
   "verdict":"reject"},
  {"item":"https://github.com/Nano-Collective/nanocoder/issues/1692","checks":[
    {"name":"Maintainers are active","grade":"pass","evidence":"akramcodez merged PRs on 2026-10-15"},
    {"name":"Push is recent","grade":"pass","evidence":"pushed_at 2026-10-15"},
    {"name":"Release is recent","grade":"pass","evidence":"v1.31.0 on 2026-09-26"},
    {"name":"Issue is good first issue","grade":"pass","evidence":"Labels: bug, good first issue"},
    {"name":"Issue filed by a human","grade":"pass","evidence":"Author addyCooks, is_bot false"},
    {"name":"Issue is one settled piece of work","grade":"pass","evidence":"One bug with a suggested fix and a test"},
    {"name":"Issue is unclaimed","grade":"pass","evidence":"assignees: []"},
    {"name":"No open PR on the issue","grade":"fail","evidence":"Open PR #1694 (Zaygal) adds the same missing specs for autoCommit, formatters, hooks and sandbox"},
    {"name":"Issue has no comments expressing interest","grade":"pass","evidence":"0 comments"},
    {"name":"Contribution policy does not explicitly forbid AI usage","grade":"unclear","evidence":"Not checked: the issue was already rejected on the open PR"}],
   "verdict":"reject"}
]
```


---

# Scan 3 (2026-10-15): same strategy as scan 2 plus backfill on reject (14 graded, 9 backfills), no per-repo limit in bigger repos

The scan found five accepted issues. Four are from the computer vision and local models fields. The fifth is stan-dev/math #3349, a C++ issue in the bigger-repos field. Grading came to 14 candidates, 9 of them backfills, and I stopped before the 10-backfill cap. The bigger-repos field ended with 1 accepted issue of its target 2, because every repo in it had been graded.

## Accepted, in fit order

1. **stan-dev/math #3349, "add is_even and is_odd here and to Stan"** (bigger repos, 842 stars, backfill).
   - **Query:** the pinned `--repo stan-dev/math` query.
   - **Why it fits:** it's self-contained C++ logic with unit tests that run locally.
   - **Tension:** the issue also asks for the Stan-language part, which lives in a different repo. I passed the "one settled piece of work" check because the Math part stands alone, but you should confirm that scope with the maintainers.
   - **Policy:** the Stan AI policy requires disclosure and a human who understands the change. It doesn't ban AI.
2. **adivishall/two-wheeler-safety #21, "API input validation: wrong JSON types return 500"** (computer vision).
   - **Query:** the `opencv` Python query.
   - **Why it fits:** it has a table of failing requests and acceptance criteria that ask for tests.
   - **Weakness:** the repo has 1 star, no release and no contribution policy.
3. **gabe-santana/saccade #22, "More minimal examples: search-only (offline), OpenAI, Ollama"** (local models).
   - **Query:** the `ollama` query.
   - **Why it fits:** it has a "Done when" list.
   - **Weakness:** it's examples and docs work. The repo has 2 stars and merges contributions fast, so claim it quickly.
4. **hoslift/ranu.js #174, "[Docs] Add local LLM setup recipe with Ollama and Docker"** (local models).
   - **Query:** the `ollama` TypeScript query.
   - **Why it fits:** it's a docs-only change with clear acceptance criteria.
   - **Weakness:** the repo has 2 stars.
5. **Thakay/sako #2, "Try SAKO in Gemini CLI and record the result"** (computer vision).
   - **Query:** the `yolo` query. It surfaced only because the repo mentions YOLO.
   - **Weakness:** it's a manual trial that needs Gemini CLI, and it's the weakest fit with your profile.

## Rejected

| Issue | Check that sank it |
| --- | --- |
| nanocoder #1692 | An open PR (#1694) is linked to it. |
| nanocoder #1774 | A claim comment from `ducanhnguyen223` on 2026-10-15. |
| open-notebook #1451 | A claim comment and open PRs #1463 and #1464. |
| open-notebook #1452 | The same open PRs, plus a comment that describes a fix. |
| lightly-train #982 | A claim comment and open PR #983. |
| llama_index #23339 | A maintainer says it needs an upstream fix, and PR #23365 is open. |
| llm-compressor #3290 | A comment from `evanliuuu` asks to be assigned. |
| Megatron-LM #5766 | Open PR #6926 is the chosen implementation. |
| dimos #3399 | Two claim comments and open PR #4540. |
| llama.cpp #17488 | Several claim comments and open PR #30530. |

## Friction for `scan-notes.md`

- The comment cap of 8 lets through issues that already have a claim. Of the first 10 bigger-repos candidates I graded, 9 failed on a claim comment or an open PR. That cost 9 backfills, and the cap could drop to about 3.
- Both top-2 bigger-repos picks came from nanocoder, because that field has no per-repo limit.
- Linked-PR detection works from the issue timeline's cross-references. I didn't check for PRs that mention an issue only by number in their own text.

I haven't posted anything upstream. Whichever issue you pick, `scope.md` says to comment on it the moment you commit.

```json
[
  {"item": "https://github.com/stan-dev/math/issues/3349", "checks": [
    {"name": "Maintainers are active", "grade": "pass", "evidence": "Last 5 commits by SteveBronder/jgabry, 2026-10-13 to 2026-10-15"},
    {"name": "Push is recent", "grade": "pass", "evidence": "pushed 2026-10-15"},
    {"name": "Release is recent", "grade": "pass", "evidence": "v5.4.0 on 2026-09-16"},
    {"name": "Issue is good first issue", "grade": "pass", "evidence": "label 'good first issue' present"},
    {"name": "Issue filed by a human", "grade": "pass", "evidence": "author bob-carpenter (User, MEMBER)"},
    {"name": "Issue is one settled piece of work", "grade": "pass", "evidence": "Single bounded request by a maintainer; the Stan-language part lives in another repo (noted)"},
    {"name": "Issue is unclaimed", "grade": "pass", "evidence": "assignees: none"},
    {"name": "No open PR on the issue", "grade": "pass", "evidence": "timeline has no cross-referenced PRs; no is_even/is_odd PR found"},
    {"name": "Issue has no comments expressing interest", "grade": "pass", "evidence": "0 comments"},
    {"name": "Contribution policy does not explicitly forbid AI usage", "grade": "pass", "evidence": "Stan AI Contribution Policy: 'We welcome AI-assisted contributions'; disclosure required, fully agentic PRs not accepted"}
  ], "verdict": "accept"},
  {"item": "https://github.com/adivishall/two-wheeler-safety/issues/21", "checks": [
    {"name": "Maintainers are active", "grade": "pass", "evidence": "Human commits by adivishall on 2026-09-16/17, within 90 days"},
    {"name": "Push is recent", "grade": "pass", "evidence": "pushed 2026-10-02"},
    {"name": "Release is recent", "grade": "fail", "evidence": "no releases (preferred only)"},
    {"name": "Issue is good first issue", "grade": "pass", "evidence": "label present"},
    {"name": "Issue filed by a human", "grade": "pass", "evidence": "author adivishall (User, OWNER)"},
    {"name": "Issue is one settled piece of work", "grade": "pass", "evidence": "One validation boundary with a request table and acceptance criteria"},
    {"name": "Issue is unclaimed", "grade": "pass", "evidence": "assignees: none"},
    {"name": "No open PR on the issue", "grade": "pass", "evidence": "only cross-reference is issue #15, not a PR"},
    {"name": "Issue has no comments expressing interest", "grade": "pass", "evidence": "0 comments"},
    {"name": "Contribution policy does not explicitly forbid AI usage", "grade": "pass", "evidence": "no CONTRIBUTING or AI policy file"}
  ], "verdict": "accept"},
  {"item": "https://github.com/gabe-santana/saccade/issues/22", "checks": [
    {"name": "Maintainers are active", "grade": "pass", "evidence": "gabe-santana merged PRs #27 and #28 on 2026-10-08"},
    {"name": "Push is recent", "grade": "pass", "evidence": "pushed 2026-10-11"},
    {"name": "Release is recent", "grade": "pass", "evidence": "v0.1.0 on 2026-10-07"},
    {"name": "Issue is good first issue", "grade": "pass", "evidence": "label present"},
    {"name": "Issue filed by a human", "grade": "pass", "evidence": "author gabe-santana (User, OWNER)"},
    {"name": "Issue is one settled piece of work", "grade": "pass", "evidence": "'Done when' lists three short example scripts plus a README update"},
    {"name": "Issue is unclaimed", "grade": "pass", "evidence": "assignees: none"},
    {"name": "No open PR on the issue", "grade": "pass", "evidence": "no cross-referenced PRs"},
    {"name": "Issue has no comments expressing interest", "grade": "pass", "evidence": "0 comments"},
    {"name": "Contribution policy does not explicitly forbid AI usage", "grade": "pass", "evidence": "AGENTS.md written for AI coding agents; no ban in CONTRIBUTING.md"}
  ], "verdict": "accept"},
  {"item": "https://github.com/hoslift/ranu.js/issues/174", "checks": [
    {"name": "Maintainers are active", "grade": "pass", "evidence": "draj256 commits 2026-10-08 to 2026-10-10"},
    {"name": "Push is recent", "grade": "pass", "evidence": "pushed 2026-10-15"},
    {"name": "Release is recent", "grade": "pass", "evidence": "v0.1.6 on 2026-10-10"},
    {"name": "Issue is good first issue", "grade": "pass", "evidence": "label present"},
    {"name": "Issue filed by a human", "grade": "pass", "evidence": "author draj256 (User, MEMBER)"},
    {"name": "Issue is one settled piece of work", "grade": "pass", "evidence": "One docs section expanded, with a task checklist and acceptance criteria"},
    {"name": "Issue is unclaimed", "grade": "pass", "evidence": "assignees: none"},
    {"name": "No open PR on the issue", "grade": "pass", "evidence": "no cross-referenced PRs"},
    {"name": "Issue has no comments expressing interest", "grade": "pass", "evidence": "0 comments"},
    {"name": "Contribution policy does not explicitly forbid AI usage", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI restriction"}
  ], "verdict": "accept"},
  {"item": "https://github.com/Thakay/sako/issues/2", "checks": [
    {"name": "Maintainers are active", "grade": "pass", "evidence": "Thakay commits 2026-09-26 to 2026-10-05"},
    {"name": "Push is recent", "grade": "pass", "evidence": "pushed 2026-10-05"},
    {"name": "Release is recent", "grade": "pass", "evidence": "v0.5.1 on 2026-09-30"},
    {"name": "Issue is good first issue", "grade": "pass", "evidence": "label present"},
    {"name": "Issue filed by a human", "grade": "pass", "evidence": "author Thakay (User, OWNER)"},
    {"name": "Issue is one settled piece of work", "grade": "pass", "evidence": "One documented trial procedure with an evidence checklist"},
    {"name": "Issue is unclaimed", "grade": "pass", "evidence": "assignees: none"},
    {"name": "No open PR on the issue", "grade": "pass", "evidence": "no cross-referenced PRs"},
    {"name": "Issue has no comments expressing interest", "grade": "pass", "evidence": "0 comments"},
    {"name": "Contribution policy does not explicitly forbid AI usage", "grade": "pass", "evidence": "CONTRIBUTING.md: 'Pull requests made with AI tools are welcome'"}
  ], "verdict": "accept"},
  {"item": "https://github.com/Nano-Collective/nanocoder/issues/1692", "checks": [
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "cross-referenced open PR #1694 (and a fork PR)"}
  ], "verdict": "reject"},
  {"item": "https://github.com/Nano-Collective/nanocoder/issues/1774", "checks": [
    {"name": "Issue has no comments expressing interest", "grade": "fail", "evidence": "2026-10-15 ducanhnguyen223: 'I would like to take this issue'"}
  ], "verdict": "reject"},
  {"item": "https://github.com/lfnovo/open-notebook/issues/1451", "checks": [
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "open PRs #1463 and #1464 cross-reference it"},
    {"name": "Issue has no comments expressing interest", "grade": "fail", "evidence": "VirenSumbly: 'I'd like to work on this issue'"}
  ], "verdict": "reject"},
  {"item": "https://github.com/lightly-ai/lightly-train/issues/982", "checks": [
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "open PR #983"},
    {"name": "Issue has no comments expressing interest", "grade": "fail", "evidence": "saitakarcesme: 'I am working on a focused fix'"}
  ], "verdict": "reject"},
  {"item": "https://github.com/run-llama/llama_index/issues/23339", "checks": [
    {"name": "Issue is one settled piece of work", "grade": "fail", "evidence": "collaborator: 'This requires an upstream fix imo'; the author's question about approach is unresolved"},
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "open PR #23365 cross-references it"}
  ], "verdict": "reject"},
  {"item": "https://github.com/vllm-project/llm-compressor/issues/3290", "checks": [
    {"name": "Issue has no comments expressing interest", "grade": "fail", "evidence": "evanliuuu: 'could I be assigned to this issue?'"}
  ], "verdict": "reject"},
  {"item": "https://github.com/NVIDIA/Megatron-LM/issues/5766", "checks": [
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "open PR #6926 named the canonical implementation"}
  ], "verdict": "reject"},
  {"item": "https://github.com/dimensionalOS/dimos/issues/3399", "checks": [
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "open PR #4540 cross-references it"},
    {"name": "Issue has no comments expressing interest", "grade": "fail", "evidence": "mc856: 'Claiming this one'; YHPeter: 'I'm willing to work on it'"}
  ], "verdict": "reject"},
  {"item": "https://github.com/ggml-org/llama.cpp/issues/17488", "checks": [
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "open PR #30530"},
    {"name": "Issue has no comments expressing interest", "grade": "fail", "evidence": "virg1n 2026-10-14: 'Taking this on'"}
  ], "verdict": "reject"},
  {"item": "https://github.com/lfnovo/open-notebook/issues/1452", "checks": [
    {"name": "No open PR on the issue", "grade": "fail", "evidence": "open PRs #1463 and #1464"},
    {"name": "Issue has no comments expressing interest", "grade": "fail", "evidence": "adityawaghamare posted a solution summary for the fix"}
  ], "verdict": "reject"}
]
```
