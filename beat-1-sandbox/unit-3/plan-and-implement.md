# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**
julianty

[Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.]

**Plan comment**
https://github.com/codepath/pathreview-ai301-fa26-s1/issues/71#issuecomment-5966457585

# Plan

The following describes my proposed approach for this issue

## Diagnosis

### Symptom:

As suggested in the [issue comment](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/71#issue-5417583935), the test surfaced a problem with indented markdown in a multi-line comment. This caused the associated test to parse no headers.

### Cause:

The parser this test uses reads each line and matches headers beginning with `#`. This does not match if there is an indentation at the beginning of the line.
I looked into the parser and confirmed this behavior on my own machine. See my [repro comment](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/71#issuecomment-5841899968).

## Scope

The only file that needs to be changed is `tests/unit/test_readme_parser.py`, no other changes necessary in any other files.

## Approach

As suggested by the issue comment, the indentation of the multi-line comment will be removed, and the `xfail` marker removed from `test_readme_parser.py`.

## Test plan

Test the same command

```
$ .venv/Scripts/python -m pytest "tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy"
```

And verify that test passes

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]

---

## Your branch

**Branch**

fix/71-remove-heading-indent-in-test

**Evidence**

Before (on `main`, with the `xfail(strict=True)` marker still in place, the test is marked as
an expected failure):

```
$ .venv/Scripts/python -m pytest "tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy"
collected 1 item

tests\unit\test_readme_parser.py x                                       [100%]

============================= 1 xfailed in 0.22s ==============================
```

Before, with `--runxfail` so the underlying failure shows (the indented fixture yields no headings):

```
$ .venv/Scripts/python -m pytest "tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy" --runxfail
        headings = parser._extract_heading_hierarchy(markdown)

        assert isinstance(headings, list)
>       assert len(headings) > 0
E       assert 0 > 0
E        +  where 0 = len([])

tests\unit\test_readme_parser.py:156: AssertionError
=========================== short test summary info ===========================
FAILED tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy
============================== 1 failed in 0.20s ==============================
```

After (on `fix/71-remove-heading-indent-in-test`, fixture de-indented and `xfail` marker removed):

```
$ .venv/Scripts/python -m pytest "tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy"
collected 1 item

tests\unit\test_readme_parser.py .                                       [100%]

============================== 1 passed in 0.14s ==============================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

categories: clear-accept 6/7 scope-creep 4/4 thread-convention 2/2 unbuildable 3/3 wrong-cause 4/4
agreement: 19/20 scored items (bar: 18/20: PASS)

**Package analysis**

pkg-14: my rubric said **reject**, gold said **accept**. It failed `buildable-plan` because the
plan defers the exact functions ("to be pinned in the PR after tracing"), which the grader read
as "investigate". But the plan names the area and has already chosen the change (drain OSC
responses before pane input is wired), and its test is concrete, so it's a borderline case. A
re-run with `--only pkg-14` passed it.

**Check rationale**

> | buildable-plan | The plan's files, approach, and test plan, read against the repro steps | A stranger could start without asking anything, and the test says what they will observe when the fix works | required |

> - **Could a stranger start?** The plan names the file, function, or
>   area to open, and has already chosen what to change there. It fails
>   on "somewhere", "whichever is easier", "investigate", "maybe also",
>   or a list of things to look at instead of a change.

I allowed "file, function, or area" instead of requiring an exact function, because what makes
a plan buildable is that the change is already chosen. Precise naming isn't what matters.

**Trade-offs**

Allowing "area" leaves an edge case: pkg-14 can grade either way from run to run. I didn't loosen
the check further, because the unbuildable packages (pkg-10, 17, 18, all correctly rejected)
fail it for vague "somewhere / investigate" wording, and a looser check could let them through.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
