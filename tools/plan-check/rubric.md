# Rubric: is this plan ready to post and build from?

Seven checks, in four groups. Each check reads the plan against
something outside it (the repro evidence, the thread, the repo's
policy) and judges the thing itself, not how the write-up looks.
Where to find each piece of evidence is in
`references/evidence-guide.md`.

| Group | Checks |
|---|---|
| Plan against the evidence | grounded-diagnosis |
| Plan on its own terms | bounded-scope, buildable-plan |
| Comment against the outside world | thread-aware-comment, ai-policy-compliance |
| Calibration of claims | honest-certainty, template-asks |

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| grounded-diagnosis | The plan's stated cause, read against the repro evidence's steps and control runs | The cause fits every control and step, and explains why the failing case fails and the control does not | required |
| bounded-scope | The plan's change list and in/out-of-scope lines, read against the one behavior the issue reports | Every proposed change is needed to fix the reported behavior | required |
| buildable-plan | The plan's files, approach, and test plan, read against the repro steps | A stranger could start without asking anything, and the test says what they will observe when the fix works | required |
| thread-aware-comment | The plan comment, read against maintainer comments in the thread highlights | Any maintainer direction is followed, or the departure is explained | required |
| ai-policy-compliance | The plan comment and plan, read against the repo's contribution policy line | The comment meets whatever the policy requires of AI-assisted comments | required |
| honest-certainty | Claims in the plan and comment, read against the repro evidence | Every claim of confirmation or coverage is backed by the package; real unknowns are named | preferred |
| template-asks | The repo's bug-report template asks, read against the repro evidence | Each template item appears, or its absence is explained | preferred |

## What each check means in practice

### grounded-diagnosis

Before reading the plan's cause, list what the repro evidence rules out:
anything a control run showed working, and any stage whose output was
already wrong before the suspected code ran. Then read the cause.

- **Pass:** the cause survives that list and explains the difference
  between the failing run and the control.
- **Fail:** a control shows the blamed component working; the plan
  states no cause; or the plan patches a symptom the evidence traces to
  an earlier cause.
- A cause borrowed from the thread passes only if the repro evidence
  supports it. Confidence in the thread is not evidence.

### bounded-scope

Number the plan's proposed changes. For each, ask: is this needed to
make the repro's expected outcome happen?

- **Pass:** every item is needed. Work the plan leaves out on purpose,
  with a reason, is fine. That is honest scoping, not creep.
- **Fail:** anything extra rides along: a migration, a redesign, a
  refactor, a new setting, "while I'm in the area" fixes. This holds
  even when the core fix inside the plan is right.
- **The same fix at a sibling site counts as one change.** If the issue
  or the repro evidence names a second place with the same bug, fixing
  it there too is not creep. Creep is a different kind of work, not
  the same fix applied twice.
- **Docs-only or workaround plans** are judged by the same question:
  is every item needed for what the plan sets out to do? A small,
  focused docs plan is bounded. Whether the thread wanted a code fix
  instead is not a scope question; thread-aware-comment grades that.

### buildable-plan

Two halves. Both must pass.

- **Could a stranger start?** The plan names the file, function, or
  area to open, and has already chosen what to change there. It fails
  on "somewhere", "whichever is easier", "investigate", "maybe also",
  or a list of things to look at instead of a change.
- **Would they know when they're done?** The test re-runs a repro step
  (or the issue's commands) and says what must now be seen. It fails
  on "run the full test suite", "should feel fast", "nothing else
  should break", or any test that never touches the failing step.

When this check fails, say which half failed.

### thread-aware-comment

Look for direction from the project's side: a named culprit, a
requested test, a chosen or rejected approach, an open PR. The
project's side means OWNER, MEMBER, and COLLABORATOR authors, plus any
CONTRIBUTOR who proposes, chooses, or rejects an approach (project
leads sometimes show up as CONTRIBUTOR). Comments from NONE authors
are background, not direction.

- **Pass:** the comment engages each piece of direction by name, either
  following it or saying why it departs.
- **Pass:** the thread has no maintainer direction, and the comment
  still says something specific to this issue (it would not read the
  same pasted onto another issue).
- **Fail:** direction exists and the comment ignores it, or the comment
  is generic, or it promises a deadline or a guarantee.

### ai-policy-compliance

Treat every package as AI-assisted. Find the policy line and match it:

| The policy says | Result |
|---|---|
| Nothing about AI | pass |
| AI welcome, no disclosure asked for comments | pass |
| Disclosure required in pull requests only | pass |
| Comments must be in the contributor's own words | pass if the comment is first-person and specific; fail if boilerplate |
| All AI use must be disclosed, in any form | pass only if the comment or plan discloses AI help (tool and extent) |
| AI contributions banned | fail |

A strong plan still fails here if a disclosure is required and missing.

### honest-certainty (preferred)

Read each "confirmed", "verified", "the cause is", "fixes", "contained
to" against the package. Fail if the plan claims more than the repro
shows, or makes a risky change without naming the risk. Never changes
the verdict.

### template-asks (preferred)

Check the repro evidence covers what the repo's bug template asks for
(version, OS, install method, logs). Never changes the verdict.

## Verdict rule

- **Accept** if every required check passes.
- **Reject** if any required check fails.
- **Unclear counts as fail.** If the package doesn't contain what a
  check needs, the plan can't be verified, so it isn't ready.
- **Preferred checks** are reported but never change the verdict.
