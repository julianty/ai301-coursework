<!-- Replace this file with your unit-3 plan: the same `plan.md` your
plan-check run graded.

Keep the deviations heading below, and fill it before you submit. It is
graded on being answered, not on there being deviations to report. -->

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

## Deviations

[What changed between the plan you posted and the change you built, and
why. If nothing changed, say so in your own words - "nothing changed;
the plan held" earns these points in full. Leaving this blank does not.]
