# Evidence guide: where evidence lives in a plan package

This guide is a map. For each kind of evidence the rubric asks about, it
says where to find it and what good looks like. It covers both the eval
bundle and live mode (the real GitHub issue and the student's drafts).

## The five parts of a package

Every check compares one part against another.

| Part | In the eval bundle | In live mode |
|---|---|---|
| Issue context | "Issue" and "Thread highlights" (each comment shows its author's role: OWNER, MEMBER, COLLABORATOR, CONTRIBUTOR, NONE) | The issue page: body, thread, and commenter badges |
| Repo facts | "Repo facts": latest release, bug template asks, contribution policy (including AI rules) | Releases, `.github/ISSUE_TEMPLATE/`, `CONTRIBUTING.md`, any linked AI policy |
| Repro evidence | "Repro evidence": environment, steps, control runs, expected / actual | The student's posted repro comment (house issue: the repro pack as quoted in the drafts) |
| Candidate plan | "Candidate plan" | The student's `plan.md` |
| Plan comment | "Candidate plan comment" | The student's draft comment |

Plans don't share headings. One says "Cause:", another "### Diagnosis".
Find each piece by what it says, not by its label.

## Diagnosis and grounding

**Answers the question:** Does the plan's cause fit what the repro
evidence actually shows?

**Where to look.** The plan's cause (and the comment's, if it restates
it differently). Then the repro evidence, especially its **control
runs**: the same steps with the trigger removed, or on another platform.
Also any cause proposed in the thread.

**What good looks like.** The cause explains why the failing run fails
*and* why the control doesn't. Nothing the controls showed working is
blamed. The fix lands where the problem starts, not where it shows up.

**Watch for.** A plan blaming a component its own control shows working.
A confident thread diagnosis adopted without checking it against the
data. A long, polished plan with the wrong cause.

## Scope

**Answers the question:** What will change, what won't, and is every
change needed for this bug?

**Where to look.** The list of proposed changes, the in-scope and
not-in-scope lines, and the files named.

**What good looks like.** Each change is needed for this bug. Anything
deliberately left out is named, with a reason.

**Watch for.** A right fix bundled with a migration, a redesign, a new
setting, or "while I'm in the area" work.

The same fix applied at a sibling site the issue or repro names is one
change, not creep. A docs-only or workaround plan can be bounded. Whether the thread
wanted a code fix instead belongs to Comms, not Scope.

## Executability

**Answers the question:** Could a stranger start the work without
asking the author anything?

**Where to look.** The files, functions, or areas named; the approach;
anywhere a decision is left for later.

**What good looks like.** You could open the named file and start. The
approach is chosen, not "to be investigated". Terse is fine.

**Watch for.** "Somewhere", "whichever is easier", "maybe also",
"not sure which layer". No files at all.

## Test plan

**Answers the question:** How will we know the fix works?

**Where to look.** The plan's test section, side by side with the
repro steps.

**What good looks like.** Re-run the step that failed and say what you
should now see. Name a control if the fix could break it.

**Watch for.** "Run the full test suite", "should feel fast", "nothing
else should break". A test that never touches the failing step.

Executability and Test plan together feed the rubric's `buildable-plan`
check: can a stranger start, and will they know when they're done?

## Honesty

**Answers the question:** Is every claim backed by the evidence, and
are the unknowns named?

**Where to look.** Every strong claim in the plan and comment
("confirmed", "verified", "fixes", "contained to"), plus any risks or
open questions the plan lists. In live mode, mid-build changes belong
in an updated `plan.md`.

**What good looks like.** Each claim points to something in the repro
evidence. Unknowns are named as unknowns, with what happens if they go
badly.

**Watch for.** Claims about versions, platforms, or cases the repro
didn't cover. Risky changes with no risk named.

## Comms

**Answers the question:** Does the comment respond to the maintainers
and follow the repo's rules?

**Where to look.** The plan comment, read against two things:

1. **The thread**: comments from the project's side: OWNER, MEMBER,
   or COLLABORATOR authors, plus any CONTRIBUTOR who proposes, chooses,
   or rejects an approach. Note what they found, asked for, chose, or
   ruled out, and any open PRs.
2. **The repo's policy line**: the AI rules, plus the bug template
   asks.

**What good looks like.** The comment answers the maintainers by name:
it follows their direction or explains why not. It acknowledges prior
work like open PRs. It's specific to this issue and promises nothing
it can't back up. It meets the repo's AI rule (see the table in
`rubric.md`).

**Watch for.** A maintainer who already isolated the bug and posted a
test build, and a comment that never mentions it. A repo requiring AI
disclosure, and a comment with none.

## The bundle is frozen

Grade what the bundle contains, not what the live issue says today. If
the bundle lacks what a check needs, the grade is `unclear`, which the
rubric treats as a fail.
