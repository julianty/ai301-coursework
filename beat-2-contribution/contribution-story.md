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
**Pull Request:** https://github.com/AcademySoftwareFoundation/OpenImageIO/pull/5650

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

**Unit 7: Installed the ship-gate, wrote a two-row manifest, and patched the hook for PowerShell**

My manifest has two must-pass rows, a build plus the BMP ctest and a clang-format 22 dry-run on the BMP plugin files. It also lists three excluded checks with dated reasons: the full testsuite, the repo-wide format script and the `-Werror` build. The hook test `gh pr create --help` went through without stopping, because Claude Code on my machine runs PowerShell and both the ship-gate and voice guard hooks only matched the Bash tool. I changed the matchers to `Bash|PowerShell` and the tool-name checks in both scripts, and after that the test stopped as expected. The gate runs manifest rows through cmd.exe, so the rows use cmd syntax. On 10/31/26 it passed my real branch: both rows ok, and all seven required pr-precheck checks passed. It still flagged things I fixed in `pr_draft.md`: "One test failed" when it was one CI job, a CI claim it couldn't verify (I checked the run myself), and no sentence saying what Claude did beyond the `Assisted-by:` line.

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

Deviations (plan accepted by plan-check on 2026-10-31): step 3 made two test files instead of one, adding a no-alpha case to cover the alpha rule. The test files use their own pixel values, so step 5's `10 50 100 200` check was done on `distinct.bmp`.

**Toolkit**

- Tool: plan-check, run live on my `plan.md` and a draft plan comment for #1901. Claude drafted the first version of the comment from my plan, and I rewrote it
- What it produced: accept, with all five required checks passing (grounded-diagnosis, bounded-scope, buildable-plan, thread-aware-comment, ai-policy-compliance). It failed two preferred checks: honest-certainty, because my comment said opaque alpha matches "the default behavior for other programs" with no evidence, and template-asks, because my repro has no `oiiotool --buildinfo` output and no minimal image
- Difficulties: before plan-check, the plan had errors I fixed while reviewing it: a `compression == 3` condition alone would have broken `g32bf.bmp`, "V5 only" left out V4, and my reason for excluding V3 was wrong. My own procedure has no check that the comment matches the plan, so my comment leaving out the V3 scope did not affect the verdict. The skill's `voice-guide.md` is only a pointer to the real file in `~/.claude/voice-guard/`
- What changed: the plan now requires a V4/V5 header, gives the right V3 reason, sets an alpha rule, and lists what it won't change. I would add a cause sentence and the V3 scope to the comment and turn the alpha claim into a question before posting, and add a "comment matches the plan's scope" line to my thread-aware-comment check

---

## Testing Strategy

I test the fix by building twice from the same build directory: once on unmodified `main` (`fde6512a2`), once on my branch (`d3a477cd9`). Then I read the same files with each `oiiotool`. Every input has a different value in each channel, so a channel swap can't hide behind equal values. The full output is in `test_evidence.md` in my clone.

**The reproduction, before and after.** `distinct.bmp` is the issue's `input.bmp` with every pixel set to R=10 G=50 B=100 A=200. `oiiotool --printstats` gives `50 100 200 10` on `main` and `10 50 100 200` on my branch. A copy with the alpha mask set to 0 gives `50 100 200 10` on `main` and `10 50 100 255` on my branch, which checks the "no alpha mask means opaque" rule.

**The regression test.** The two new 2x2 files in `testsuite/bmp/src/` (`g32bf-rgba-v5.bmp` and `g32bf-noalpha-v5.bmp`) read with rotated channels on `main` and with the values I wrote on my branch (`oiiotool --dumpdata`). Pillow 13 agrees with my branch. They're now in `testsuite/bmp/run.py`, so the reference output records their pixel hashes, and the test fails if the decode ever changes.

**The control.** The main risk of the fix is changing how other BMPs decode, especially `g32bf.bmp`, a 32-bit bitfields file with a V3 header that has to keep the old path. The regenerated `ref/out.txt` adds 22 lines and removes none, so every existing file in the BMP test, including `g32bf.bmp` and `g32def.bmp`, gives the same output and SHA-1 as on `main`.

**The repo's checks.** `ctest --test-dir build -R bmp` passes, and clang-format 22.1.8 (CI's version) reports nothing on the BMP plugin files. I don't run the full testsuite (my local build has most optional formats off), the `-Werror` build (`main` fails it on MinGW for an unrelated file), or Linux/macOS locally. CI on my fork covered those (27 of 28 jobs passed, see the Toolkit below), and upstream CI will run them again on the PR. The ship manifest lists these exclusions with dates.

**What the tests don't cover.** 32-bit bitfields files with a V3 header and non-default masks are still misread. That's out of scope by the plan, and the evidence says so instead of hiding it.

**Toolkit**

- Tool: my local `oiiotool` builds of `main` and of my branch for before/after reads, Pillow and the unfixed PyPI wheel to check the test files independently, `ctest` for the BMP test, and CI on my fork (GitHub Actions) for the full testsuite. Claude ran the builds and captured the output into `test_evidence.md`.
- What it produced: before/after values for `distinct.bmp` (`50 100 200 10` -> `10 50 100 200`) and for both new test files, a `ref/out.txt` diff of +22/-0, and a fork CI run where 27 of 28 jobs passed (run 41219941633).
- Difficulties: the fork had Actions turned off, so the first push ran nothing. The one failing CI job (`MacOS-15-ARM` py3.13) failed on 14 Python tests with `No module named 'numpy'`, and I had to check that it wasn't my change. The system Python had no Pillow, so the cross-check ran from the clone's `.venv`.
- What changed: I enabled Actions on the fork and started the workflow by hand. I compared the failing job with upstream `main`'s runs, where the same job fails the same way at `0008a6f04`, and the BMP test passed in that job. So I ticked the CI box under the template's "unrelated failures" exception and explained it in the PR description.

---

## Implementation Notes

**2026-10-30**

Set up a local build so I could test a fix, not just the released wheel. I installed OIIO's dependencies through MSYS2 (OpenEXR, Imath, libtiff, libjpeg-turbo, libpng, zlib, fmt, robin-map, OpenColorIO) and built with Ninja and g++, with Python bindings and most optional formats turned off. Three things fought me: `main` doesn't compile under MinGW with warnings as errors (unused `decode_utf8`/`encode_utf8` in `src/libutil/strutil.cpp`, unrelated to BMP), so I built with `-DSTOP_ON_WARNING=OFF`; the testsuite needs a Windows CPython, because MSYS2's Python writes `../..` paths that `cmd.exe` can't run; and `runtest.py` calls `tr` and `diff`, so `C:\msys64\usr\bin` has to be on PATH. After that, `ctest --test-dir build -R bmp` passes on `main` (fde6512). My build of `main` also reads `distinct.bmp` as `50 100 200 10` (`oiiotool --printstats`), so the bug is confirmed on current `main`, not just on 3.2.1.3.

**2026-10-31**

Plan accepted by plan-check. Chose option (b): use the masks only for 32-bit `BI_BITFIELDS` files with V4/V5 headers and leave `read_header` alone, because a 32-bit V3 file's masks are never read and `g32bf.bmp` (V3, 32-bit, bitfields) has to keep passing. Decided not to touch the default-mask block in `open()` for alpha: a zero alpha mask means "no alpha", and adding it to that condition would overwrite the real masks of 16-bit bitfields files like `g16bf565.bmp`.

Step 1 (commit `44c4987ef` on `fix/1901-bmp-bitfields`): widened `m_right_shifts` and `m_bit_counts` from 3 to 4 entries and added a `calc_shifts` call for `alpha_mask` in `BmpInput::open`. The BMP test still passes and clang-format 22 is clean, as expected, since nothing reads the alpha slot yet.

Step 2 (commit `b80389108`): added a branch at the top of the 32-bit path in `read_native_scanline`, taken only when `bpp == 32`, `compression == 3` and the header is V4 or V5. It reads each pixel as a `uint32_t`, masks and shifts out each channel with the shifts from step 1, and scales it to 8 bits with `bit_range_convert`, the same helper the 16-bit path uses. Two wrong turns: my first version had no `return true` at the end of the new branch, so it fell through into the old byte-swap code and the output was still wrong; and I first ran alpha through `bit_range_convert` like the other channels, which gives 0 (fully transparent) when the alpha mask is 0 because the bit count is 0. I added an explicit `alpha_mask == 0` case that writes 255. After that, my build reads `distinct.bmp` as `10 50 100 200` (it was `50 100 200 10`), a copy with the alpha mask zeroed reads alpha 255, the BMP test still passes, and clang-format 22 is clean.

Steps 3 to 6 (commit `d3a477cd9`): wrote a throwaway Python script with `struct.pack` that builds two 2x2 V5 bitfields files from scratch, `g32bf-rgba-v5.bmp` (masks R `ff000000`, G `ff0000`, B `ff00`, A `ff`) and `g32bf-noalpha-v5.bmp` (alpha mask 0, junk in the low byte). Every pixel and channel has a different value, so a channel swap or a flipped row would show. Getting the headers right took a few drafts: wrong value counts for the `struct` formats, a file size that left out the 14-byte file header, and a pixel offset that pointed at the header length instead of 138. Pillow, my build and the unfixed 3.2 wheel then agree on the file contents and disagree on the decode: Pillow and my build read `(0,0)` as `11 61 121 201`, and the wheel reads `61 121 201 11`. Pillow opens the no-alpha file as RGB (3 channels), while OIIO reports 4 channels with alpha 255, which is the rule I chose in the plan. I added both files to `testsuite/bmp/run.py` with `rw_command("src", ...)`; I first put them in the `files` list, which reads from the downloaded bmpsuite folder, not `src/`. The new reference output only adds 22 lines and removes none, so `g32bf.bmp`, `g32def.bmp` and every other existing file read exactly as before. One Windows trap: the first run kept saying my new files didn't exist, even after reconfiguring. `runtest.py` copies `src/` and `ref/` into `build/testsuite/bmp/` only if they aren't there yet (other platforms use symlinks), so I had to delete the stale copies after adding files or changing the reference.

**2026-11-03**

Opened the PR. One wrong turn while rewriting the PR description: I ran `ctest --test-dir build -R bmp` from PowerShell and it failed, with the whole output shown as added lines. My fix was fine; the PowerShell session didn't have `C:\msys64\usr\bin` on PATH, so `runtest.py` couldn't run `diff` and `tr` to compare against the reference. The same trap from 10/30, in a new shell. With `C:\msys64\ucrt64\bin;C:\msys64\usr\bin` added to PATH, it passed (1/1).

Disclosure: another session told me I could leave `Assisted-by:` off the fix commits because I wrote the code. After reading `AI_Policy.md` again I added it to all three commits (before pushing), because the policy requires it when an AI "helped design the approach" or "suggested the specific fix", and my claim on #1901 promised the line on any commit Claude helped with.

**Toolkit**

- Tool: Claude Code as a navigator. It explained `bmpinput.cpp`, the BMP header layouts and `struct.pack` syntax, and reviewed each of my drafts. I wrote the C++ change, the test script and `run.py` by hand, as my claim on #1901 promised. Claude ran the builds, the BMP test and clang-format, regenerated `ref/out.txt` (a generated file), and did the `Assisted-by:` rebase.
- What it produced: three commits on `fix/1901-bmp-bitfields` (`44c4987ef`, `b80389108`, `d3a477cd9`), each with `Signed-off-by` and `Assisted-by: Claude Code / Claude Opus 5.5`.
- Difficulties: two times I asked Claude to write text that goes upstream (a commit body and my issue comment). It declined and gave line-by-line notes instead, because of the boundary I'd set. Two sessions also disagreed about whether `Assisted-by:` was needed on code I typed myself.
- What changed: I wrote both texts myself from the notes. I settled the `Assisted-by:` question by reading `AI_Policy.md` directly instead of trusting either session, and added the line to all three commits before pushing.

---

## Pull Request

**PR Link:** https://github.com/AcademySoftwareFoundation/OpenImageIO/pull/5650 (opened 2026-11-03)

**PR Description:** Title `fix(bmp): decode 32-bit BI_BITFIELDS pixels with the channel masks`, three commits (`44c4987ef`, `b80389108`, `d3a477cd9`). The description opens with "Fixes #1901" and says what changed: `open()` now computes the shift and bit count for the alpha mask, and `read_native_scanline` decodes 32-bit `BI_BITFIELDS` pixels with the four masks when the header is V4 or V5; a zero alpha mask gives alpha 255. It states the scope limit (V3 32-bit files keep the old byte swap, since fixing them means changing `bmp_pvt.cpp`), lists the two new test files and what each checks, and says `ref/out.txt` only gains lines. It has the `Assisted-by: Claude Code / Claude Opus 5.5` line plus a sentence on what Claude did (reviewed my changes, checked my test-file headers) and what I did (wrote the fix and the generator script, ran the bmp test). The CI checklist note links my fork run, names the one failing job, and explains why it is unrelated (missing numpy, same failure on upstream `main` at `0008a6f04`, bmp test passed in that job).

**Maintainer Feedback:**

- 2026-11-03: none yet from maintainers. The EasyCLA bot commented within a minute that my commits weren't covered by a signed CLA, and its check failed. I signed the Individual CLA, and after a recheck the bot showed "EasyCLA check passed". DCO passed from the start because every commit has `Signed-off-by`.
- 2026-11-03: the CI workflows haven't started on the PR yet; as a first-time contributor, a maintainer may need to approve the run.

**Status:** Awaiting review

**Toolkit**

- Tool: ship-gate (my two-row manifest plus pr-precheck in live mode) and the voice guard, both firing as hooks when Claude ran `gh pr create` with `--body-file pr_draft.md`.
- What it produced: on the first try the voice guard stopped the post on "Claude then reviewed the behavior and tested it" and "BMP test passes locally" with no command named. On the second try the ship-gate ran both manifest rows (ok) and then rejected the branch: pr-precheck said the test evidence listed the full suite and Linux/macOS as "left to upstream CI" and the description didn't disclose that. On the third try the gate passed and the voice guard stopped a new line that reported test results Claude got, not me. The fourth try opened PR #5650.
- Difficulties: the voice guard is graded by a model, and it passed my draft in manual mode (`check_voice.py --draft`) and then stopped a nearly identical draft as a hook minutes later. The gate's reject came from `test_evidence.md`, which was written before my fork CI run and was out of date, not from anything wrong in the PR. The gate had accepted the same branch with an earlier version of the draft in a manual run that morning, so its verdict changed with no change to the code.
- What changed: Claude updated `test_evidence.md` with the fork CI run. I rewrote the disclosure line so it says what I ran myself, after running the bmp test with the MSYS2 PATH fix. I would make the gate's evidence file part of the branch-ready checklist (refresh it after CI), and treat a single voice-guard pass as a signal, not a guarantee.

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
