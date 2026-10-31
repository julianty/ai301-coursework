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

Files that are 32-bit color encoded with color masks that do not match the default (ARGB) have their channels read incorrectly.

**Expected Behavior**

I created a file `distinct.bmp` with the headers matching `input.bmp`. It is an image, 256x256, filled with this exact pixel value: `(R,G,B,A) = (10, 50, 100, 200)`.
`distinct.bmp` should be read as R=10, G=50, B=100, A=200, matching Pillow.

**Current Behavior**

`distinct.bmp` is being read as R=50, G=100, B=200, A=10. This swap is more than a simple A, B channel swap. The channels are being read as GBAR.

**Affected Components**

`src/bmp.imageio/bmpinput.cpp` (Ingests bmp) `src/bmp.imageio/bmp_pvt.cpp` (Reads headers)

**Toolkit**

- Tool: Claude Code, used only to explain code: how `read_header` reads the header field by field with `fread`, the difference between V3/V4/V5 headers, and what compression 3 (`BI_BITFIELDS`) means
- What it produced: explanations of `bmp_pvt.cpp` and `bmpinput.cpp`, and a header dump of the 32-bit test files showing `g32bf.bmp` is a V3, 32-bit, `BI_BITFIELDS` file and `g32def.bmp` is V3 with compression 0
- Difficulties: I misread things that took several rounds to clear up: I thought `WINDOWS_V3` meant 16 bpp and that compression 3 meant the masks were non-default (it means "use the masks"), and my first draft blamed `BmpInput::open`. Claude's header dump also printed an alpha mask of `0x0` for `g32bf.bmp`, which is not a real mask (V3 has only three), so I had to check its output against the code
- What changed: I followed the masks myself from `read_header` to `read_native_scanline`, which moved the cause to `read_native_scanline`, made me describe `input.bmp` as a valid file whose masks the reader ignores, and turned up the V3 32-bit case that set my scope

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

The masks are read by `DibInformationHeader::read_header` in `bmp_pvt.cpp`. They are applied in the 16-bit image case, but are unused in the 32-bit image case.
In the function `BmpInput::read_native_scanline` in `bmpinput.cpp`, the pixel values are read in. As a 32-bit image, the byte order
on disk expected by the function is BGRA (little-endian storage of ARGB). The function wants to reorder this into
RGBA, so the 0th and 2nd bytes of each pixel are swapped. This achieves RGBA for typical images.
In our case, `input.bmp`, `read_native_scanline` produces GBAR from ABGR (ABGR because of little-endian storage of RGBA).
After the swap, the function returns. It does not use the bit shifts that were computed in `BmpInput::open`.
`BmpInput::open` only computes the shifts for three channels, thus the arrays `m_right_shifts` and `m_bit_counts` have 3 entries for the RGB channels.

**Proposed Solution**

The `read_native_scanline` path for 32-bit images should pass through a mask read and shift if the `compression` header value is 3. This indicates that color masks describe which channel is encoded in the 32-bit number.
The `compression` value of the header is read in `DibInformationHeader::read_header`, so it's accessible in `bmpinput.cpp` already as `m_dib_header.compression`.
The solution would involve changing the mask computations in `BmpInput::open` to include the alpha channel.
An additional condition would live in `BmpInput::read_native_scanline` for the 32-bit case that checks the header compression.
If `compression == 3`, 32-bit, and the header is `WINDOWS_V5 || WINDOWS_V4`, apply the four masks.
The condition `WINDOWS_V5 || WINDOWS_V4` is necessary because for a 32-bit `WINDOWS_V3` file `read_header` reads no masks at all (see below), so they would be zero and `open()` would fill in the 16-bit defaults.
If `alpha_mask` is 0, the file has no alpha channel, so alpha is set to fully opaque (255).

**What I Won't Change**

I chose not to change `bmp_pvt.cpp`, where `DibInformationHeader::read_header` lives.
It controls the header variables that are made available in `bmpinput.cpp`.
In its current state, it provides enough information to complete this fix, but uncovers a possible other issue.
BMP files that use `WINDOWS_V3`, and have `compression == 3` may need their color masks.
The current state of `bmp_pvt.cpp`, a 32-bit image using `WINDOWS_V3` will not read any color masks even with the
`compression == 3` header.
V3 32-bit files keep the old byte swap, so one with non-default masks will still be misread.
I could open another issue to address this problem if desired.
Compression 0, 24-bit, 16-bit, palette/RLE files and the BMP writer are untouched.

**Implementation Plan**

1. Changes in `BmpInput::open()`
   Include the alpha channel when computing `m_right_shifts` and `m_bit_counts`

2. Changes in `BmpInput::read_native_scanline()`
   Add a condition check nested in the `m_dib_header.bpp == 32` path for `m_dib_header.compression == 3` and a `WINDOWS_V4` or `WINDOWS_V5` header
   Use the computed shifts in `open()` to shift the color data similar to how `.bpp == 16` implements it.

3. Create a test image with `WINDOWS_V5` headers, `compression = 3`, and color masks similar to `input.bmp`. Only a few pixels, saved in `testsuite/bmp/src/`

4. Add it to `testsuite/bmp/run.py` and generate new `ref/out.txt`

5. Confirm the build reads it as R=10, G=50, B=100, A=200

6. Run the full BMP test, and confirm the `g32bf` and `g32def` hashes are unchanged

7. Re-run the reproduction on `distinct.bmp` with the branch build before and after

8. clang-format, then commit with -s, a `fix(bmp):` subject, and Assisted-by: line.

Deviations: none yet (plan accepted by plan-check on 2026-10-31).

**Toolkit**

- Tool: plan-check, run live on my `plan.md` and a draft plan comment for #1901. Claude drafted the first version of the comment from my plan, and I rewrote it
- What it produced: accept, with all five required checks passing (grounded-diagnosis, bounded-scope, buildable-plan, thread-aware-comment, ai-policy-compliance). It failed two preferred checks: honest-certainty, because my comment said opaque alpha matches "the default behavior for other programs" with no evidence, and template-asks, because my repro has no `oiiotool --buildinfo` output and no minimal image
- Difficulties: before plan-check, the plan had errors I fixed while reviewing it: a `compression == 3` condition alone would have broken `g32bf.bmp`, "V5 only" left out V4, and my reason for excluding V3 was wrong. My own procedure has no check that the comment matches the plan, so my comment leaving out the V3 scope did not affect the verdict. The skill's `voice-guide.md` is only a pointer to the real file in `~/.claude/voice-guard/`
- What changed: the plan now requires a V4/V5 header, gives the right V3 reason, sets an alpha rule, and lists what it won't change. I would add a cause sentence and the V3 scope to the comment and turn the alpha claim into a question before posting, and add a "comment matches the plan's scope" line to my thread-aware-comment check

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
