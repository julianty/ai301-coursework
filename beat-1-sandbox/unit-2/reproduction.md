# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

julianty

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/71#issuecomment-5841396080

Hi! I'd like to work on this one, too.
I see @miaaoyama has already posted a reproduction. I'll run my own from my environment and share it here.

My plan:

1. Reproduce it locally first: run the test with the `xfail` marker removed and confirm it
   fails because no headings are extracted.
2. Remove the indentation from the fixture, then remove the `@pytest.mark.xfail` marker.
3. Confirm the test passes, and check that nothing else in `tests/unit/test_readme_parser.py`
   depends on the indented fixture.

I'll post my reproduction here before opening a PR. Happy to adjust if you'd like it
handled differently!

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/71#issuecomment-5841899968

### Environment

- OS: Windows 11, running commands in Git Bash
- Python: 3.11.8 (python.org installer)
- pytest: 9.1.1
- Code: upstream `main` at commit `f89c06f` (2026-09-16), no local changes

### Setup

From a fresh clone of the repo:

```bash
PATH="/path/to/python311:$PATH" make setup
```

Note: in my Git Bash, `python` pointed to an MSYS2 Python, which creates
`.venv/bin/` instead of `.venv/Scripts/`, so `make setup` failed. Putting the
python.org Python first on PATH fixed it.

### Steps and observed output

Run the test with `--runxfail`, so pytest ignores the `xfail` marker and reports the real failure:

```text
$ .venv/Scripts/python -m pytest "tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy" -v --runxfail
```

Local paths replaced with <repo>, and plugin header lines trimmed to [...]; otherwise unedited.

```text
============================= test session starts =============================
platform win32 -- Python 3.11.8, pytest-9.1.1, pluggy-1.6.0 -- <repo>\.venv\Scripts\python.exe
rootdir: <repo>
configfile: pyproject.toml
[...]
collecting ... collected 1 item

tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy FAILED [100%]

================================== FAILURES ===================================
_______________ TestReadmeParser.test_extract_heading_hierarchy _______________

self = <tests.unit.test_readme_parser.TestReadmeParser object at 0x00000249F6EDEE90>
parser = <ingestion.parsers.readme_parser.ReadmeParser object at 0x00000249F6EFDA10>

    @pytest.mark.xfail(
        strict=True,
        reason="issue #71 (manifest H-04): heading hierarchy fixture is indented, so it has no headings",
    )
    def test_extract_heading_hierarchy(self, parser):
        """Test heading hierarchy extraction."""
        markdown = """
        # Main Title
        Some content

        ## Subsection
        More content

        ### Sub-subsection
        Even more content

        ## Another Section
        Final content
        """
        headings = parser._extract_heading_hierarchy(markdown)

        assert isinstance(headings, list)
>       assert len(headings) > 0
E       assert 0 > 0
E        +  where 0 = len([])

tests\unit\test_readme_parser.py:156: AssertionError
=========================== short test summary info ===========================
FAILED tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy
============================== 1 failed in 0.19s ==============================
```

### Result

Reproduced on current `main`. With `--runxfail`, the test fails at line 156
with `assert 0 > 0`: `_extract_heading_hierarchy` returns `[]` for the test's fixture.

This matches the issue's description. Every line of the fixture starts with
8 spaces, and reading the source, the parser only treats a line as a heading
if `#` is its first character
([`readme_parser.py` line 55](https://github.com/codepath/pathreview-ai301-fa26-s1/blob/f89c06fc3ff292df2a04a39ac51319d32a76b779/ingestion/parsers/readme_parser.py#L55)):

```python
match = re.match(r"^(#{1,6})\s+(.+)$", line)
```

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

categories: clear-accept 8/8 disclosure 1/1 no-evidence 4/4 unfollowable-comms 3/3 wrong-target 4/4
agreement: 20/20 scored items (bar: 18/20: PASS)
run written to eval-run.txt

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Package analysis**

pkg-01
My rubric decided to accept this; and the gold label agreed to accept with the note: "faithful offline repro of the missing Content-Type with a control run; env recorded; claim specific and modest"
It decided to accept because every required check passed.

```JSON
{
  "item": "pkg-01",
  "checks": [
    {"name": "env-recorded", "grade": "pass", "evidence": "'Environment: HTTPie 3.2.4 (pip), Python 3.12.4, multidict 6.6.0, macOS 14.5 (arm64)': version, platform, and the thread's deciding factor (multidict) all recorded"},
    {"name": "env-matches-target", "grade": "pass", "evidence": "Tested 3.2.4 = 'latest release: 3.2.4'; multidict 6.6.0 is newer than the regressed 6.5.0 named in the thread"},
    {"name": "steps-followable", "grade": "pass", "evidence": "Single self-contained command '$ http --offline post pie.dev/post 'header1: xyz' x=1' with no private inputs"},
    {"name": "steps-hit-trigger", "grade": "pass", "evidence": "Keeps the trigger (exactly one custom header 'header1: xyz' plus JSON body x=1); swap from -v to --offline is named: 'offline, prints the request without sending'"},
    {"name": "behavior-shown", "grade": "pass", "evidence": "Artifact request shows 'header1: xyz' and body '{\"x\": \"1\"}' with no Content-Type line, matching the issue's step-1 output"},
    {"name": "claims-backed", "grade": "pass", "evidence": "'I can reproduce the missing Content-Type ... on 3.2.4' is backed by the artifact; no root cause asserted, only a plan to check apply_missing_repeated_headers()"},
    {"name": "claim-specific-and-honest", "grade": "pass", "evidence": "Names 'missing Content-Type: application/json on 3.2.4 with exactly one custom header'; next step 'check ... and report back what I find'; no deadline or reservation"},
    {"name": "ai-policy-respected", "grade": "pass", "evidence": "'standard contribution guide; no stated AI policy'"},
    {"name": "control-run", "grade": "pass", "evidence": "Control '$ http --offline post pie.dev/post x=1' shows 'Content-Type: application/json' present when the single custom header is removed"},
    {"name": "template-asks-covered", "grade": "fail", "evidence": "Template asks to confirm a search for similar issues; report states latest version and minimal steps but never mentions searching"}
  ],
  "verdict": "accept"
}
```

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

**Check rationale**

Check: steps-followable

Evidence: The repro report's steps and every input they use (files, configs, layouts, scripts), inline or linked (evidence guide: Steps)

Pass condition: A stranger with only the posted comment could re-run the steps from a named starting state to the trigger: every command is given, and every input the steps depend on is shown inline, publicly linked, or is the issue's own published reproduction. Fails if any step depends on something private or unshared (a private repo, an internal config, "our pre-commit hook"), or if the report has no steps at all.

It reads this way because I asked Claude to generate a tighter pass condition. The steps-followable criteria is a vague one, but an important one, so I wanted to have a very tight description.

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

After writing the rubric loosely in class and in the time after, I had Claude Opus draft the rubric based on my work.
My only eval run scored 20/20, with every category at full marks. No package disagreed with the gold label, so there was nothing a change could fix, and any change could only risk breaking a package that already agreed.

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
