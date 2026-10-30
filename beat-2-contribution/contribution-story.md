# Contribution: Misinterpretation of some BMP files (A and B channels swapped?)

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Alexander Julian Ty
**GitHub Username:** julianty
**Issue:** https://github.com/AcademySoftwareFoundation/OpenImageIO/issues/1901
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built the issue-scout with a three-field search strategy and tuned it over three scans**

I wrote a search strategy of 15 `gh search issues` queries in three fields (computer vision, local models, and 9 pinned repos with 500+ stars), ranked the results by freshness, label and fewest comments, and had the scout grade the top candidates. The first scan failed on permissions, so 5 of 6 candidates were rejected for missing data, not on merit; I added `gh` allow rules and told the strategy to run each query as a single command. Even then the winners came from repos with 0 to 2 stars, because fewest-comments-first rewards places nobody visits, and the bigger-repo picks mostly failed on claim comments or open PRs, so I measured comments by repo size and added the pinned bigger-repos field, a 12-month age drop, backfill on reject, and `-linked:pr` on every query. Scan 3 accepted 5 issues, including stan-dev/math#3349 (842 stars), but the rubric still has no duplicate check and `-linked:pr` misses PRs that only mention an issue in text.

**Unit 6: Installed the voice guard and wrote a repo memory file for OpenImageIO**

My voice guide has an Upstream section that checks my Github CLI commands and is wired as a hook
on Bash commands. Claude ran a wiring test and stopped `gh issue comment --help` (on purpose) and passed
my claim comment on OpenImageIO#1901 today (10/23/26). The guard only sees Claude Code runs, so it doesn't
check anything I write on the browser. I rewrote the claim draft myself after running /repro-check
since it flagged my claim comment as including the repro. I cloned the repo and Claude has a memory file
with the repo's `AGENTS.md`, AI policy for context. It's excluded via `.git/info/exclude`.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I got this issue from the Issue Selection site and graded it with my issue-scout in direct mode, not from a scan. The scout accepted OpenImageIO#1901 and frontend-app-authoring#2768 and rejected maplibre-native#2888 because a contributor had asked a scoping question in August that nobody answered. I re-graded all three on 2026-10-22 after replacing my scope check with the staff `scope-feasible` check. #1901 was accepted again with a difficulty note of moderate: the bug is one reproducible problem with a test file attached, but I have to find the BMP reader myself.

It fits me because it is C++ image I/O with a file I can test against, and the fix can be proved with a regression test, which is the skill I wanted to practice. The report is from 2018, so the first thing I did was check it still happens: on OIIO 3.2.1.3 it does, and it is wider than the title says (see Reproduction Process). I hope to learn how a file-format reader is tested in a large project and how a maintainer wants a bug like this fixed.

The scout flagged something its rubric cannot grade: OIIO's AI policy "discourages use of AI tools to fix GitHub issues labeled as 'good first issue'", and #1901 has that label. I chose it anyway and said so in my claim: Claude Code only helps me read the code and learn, and I write the fix and the test myself, with an `Assisted-by:` line on anything it helped with. The scout's other limit was that its checks ran on release data and the thread at grading time; it could not tell me that the title's "A and B swapped" was incomplete, which I found by running the file.

Claim comment: https://github.com/AcademySoftwareFoundation/OpenImageIO/issues/1901#issuecomment-6375543695 (posted 2026-10-23)

**Toolkit**

- Tool: issue-scout, run in direct mode on three Issue Selection picks, with my rubric patched on 2026-10-22 (my unit-1 scope check replaced by the staff `scope-feasible` row, plus a difficulty note)
- What it produced: accept for #1901 (difficulty: moderate) and #2768, reject for maplibre-native#2888 on an interest comment; a policy note on OIIO's AI conditions
- Difficulties: the scout cannot judge fit or skill, treats "no release on GitHub" as a failure for projects that publish elsewhere (openedx), and its checks did not surface the AI policy's good-first-issue discouragement as a check; it appeared only as an aside
- What changed: the scope check now accepts issues with open design edges and raises a difficulty note instead; I read the thread and `CONTRIBUTING.md` myself before choosing. Not changed: the policy gap (I would add a "policy discourages AI on this label" line to the rubric if I scan again)

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

Windows 11 Home 10.0.26200, Python 3.11.8 in a venv, OpenImageIO 3.2.1.3 from the PyPI wheel (`pip install OpenImageIO pillow numpy`; Pillow 13.0.0, numpy 2.4.6). I forked and cloned the repo (clone at `main`, fde6512, 2026-10-22) but did not build it for the reproduction: the full build needs dependencies I had not set up on Windows, so every run in this section uses the released wheel. Challenges: none with the install. I compared `src/bmp.imageio/` between my `main` and `upstream/main` (43b3d649d) to see whether the reader changed: it did not, and it is unchanged since tag v3.2.1.2.

**Steps to Reproduce**

1. Create a venv and run `pip install OpenImageIO pillow numpy`.
2. Download the issue's file: `curl.exe -L -o input.bmp https://raw.githubusercontent.com/NatronGitHub/Natron-Tests/master/TestImageBMP/input.bmp` (262282 bytes, SHA-256 `49CBF792C41099DD61E38DDAE0A45504A4B5178531402965E0A8A8885254C91B`).
3. Read the header: it is a 124-byte BITMAPV5HEADER, 32 bits per pixel, compression 3 (BI_BITFIELDS), with masks red `0xff000000`, green `0x00ff0000`, blue `0x0000ff00`, alpha `0x000000ff` (bytes stored A, B, G, R).
4. Read the file with OIIO (`oiio.ImageBuf("input.bmp").get_pixels(oiio.UINT8)`) and with Pillow (`.convert("RGBA")`) and compare channels with `np.array_equal`.
5. Observed result: OIIO's blue is only 255 and its alpha varies; Pillow's alpha is only 255. OIIO's blue equals Pillow's alpha and OIIO's alpha equals Pillow's blue exactly, and OIIO's red and green do not match Pillow's either.
6. After lgritz asked for a test where R, G, B and A all differ in every pixel, I kept the header of `input.bmp` and filled every pixel with R=10, G=50, B=100, A=200 (`distinct.bmp`). Observed result: OIIO reads R=50, G=100, B=200, A=10 (the file read as G,B,A,R); Pillow reads 10, 50, 100, 200.

**Reproduction Evidence**

- **Commit showing reproduction:** none; the reproduction runs against the released wheel, and the scripts are in my comments on the issue.
- **Screenshots/logs:** first run, posted with my claim: https://github.com/AcademySoftwareFoundation/OpenImageIO/issues/1901#issuecomment-6375543695. Distinct-pixel test, posted 2026-10-24: https://github.com/AcademySoftwareFoundation/OpenImageIO/issues/1901#issuecomment-6380706774. Key lines: `OIIO unique per channel: [[0..5], [0..5], [255], [0..5]]` against `Pillow unique per channel: [[0..5], [0..5], [0..5], [255]]`; `OIIO output == raw bytes with bytes 0 and 2 swapped: True`; `Pillow == decode using the header masks: True`; for `distinct.bmp`, `OIIO unique per channel: [[50], [100], [200], [10]]` against `Pillow unique per channel: [[10], [50], [100], [200]]`. A control file with the default 32-bit layout reads all four channels correctly.
- **My findings:** reproduced on 3.2.1.3 (not on `main`, which I did not build). The issue title says A and B are swapped; the full comparison shows all four channels are wrong, because `bmpinput.cpp` handles every 24- and 32-bit file by swapping bytes 0 and 2 (assuming B,G,R,A order) and ignores the channel masks, while this file's masks say the bytes are A,B,G,R. Swapping bytes 0 and 2 of A,B,G,R gives G,B,A,R, which is exactly what the distinct-pixel test shows. lgritz suspected "a deeper problem is lurking", and the distinct-pixel test confirmed it.

**Toolkit**

- Tool: repro-check, graded on the claim and the report together
- What it produced: accept on all ten checks, with three fixes: open the report by correcting the claim, paste the missing scripts, and say I used Python and `oiiotool` instead of `iconvert`
- Difficulties: it could not read my voice guide in a non-interactive run (blocked by file permissions), so it did not check the drafts against it; it is also a grader of my report's form and cannot tell me the reproduction is complete
- What changed: I added the three scripts and an `oiiotool` step to the report (the wheel ships `oiiotool` and `maketx` but not `iconvert`, which I checked in the venv instead of assuming)

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
