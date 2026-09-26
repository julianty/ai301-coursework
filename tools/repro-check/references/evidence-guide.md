# Evidence guide: where proof lives in a reproduction package

Every rubric check names a kind of proof. This guide maps the five proof
families to the places you look: in the eval bundle (the package
markdown or its `.json` twin) and in live mode (the GitHub issue thread,
the repo's docs, and the student's draft comments). Each family ends
with what good looks like, stated as conditions someone else could check.

A package has four parts, and every check reads one of them against
another:

| Part | In the eval bundle | In live mode |
|---|---|---|
| Issue context | "Issue" (title, body excerpt) and "Thread highlights" (each comment with its author association: MEMBER, CONTRIBUTOR, NONE) | the issue page on github.com: the body, the thread, and the badges next to commenters' names |
| Repo facts | "Repo facts" block: latest release, the bug-report template asks, the contribution policy line (including any AI policy) | the repo's Releases box, `.github/ISSUE_TEMPLATE/`, `CONTRIBUTING.md`, and any `AI_POLICY.md` / `AI_USAGE_POLICY.md` it links to |
| Claim comment | "Candidate claim comment" | the student's draft claim comment |
| Repro report | "Candidate repro report": its environment record, steps, artifacts, and expected / actual | the student's draft repro comment |

Read the issue context first. Nearly every check is a comparison, and
the issue is the side you compare against.

## Environment

**Where it lives.**

- Candidate side: the repro report's environment record, usually a line
  starting "Environment:" or a table under an Environment heading. Some
  reports fold it into prose ("reproduced on 4.53.3 on macOS"); that
  counts if the facts are there.
- Target side: whatever the issue says is affected. Look in the issue
  body (versions, "built from main", "release build"), the template
  checkboxes the bundle summarizes ("confirmed on latest and main"),
  and maintainer comments in the thread ("cannot reproduce on the Store
  release", "works in Debug, crashes in Release").
- Deciding factors: things the issue or thread says change the
  behavior. Examples from this set: the minikube driver on a
  Windows-specific tunnel bug, debug vs release build profile on an
  overflow bug, browser language order on a translation bug, shell and
  `PWD` handling on a symlink bug, the `multidict` version on a header
  bug, `ARG_MAX` on an argument-size bug.

**What good looks like.**

- The record names the version of the software under test and the
  platform (OS and architecture, or the playground / browser when the
  repro runs there), plus every deciding factor the issue names.
- The tested version is the issue's target or newer. Anything older, or
  a different build or channel (Store release vs git main, release vs
  debug), is named in the report as a difference and treated as a
  limitation, not as a bonus confirmation.
- A report with no environment record at all fails, however good its
  output looks: a stranger cannot place the attempt, so they cannot
  tell whether it tested the reported bug.

**Common failures.** No record at all. An old version tested silently
against an issue confirmed on latest or main. A different build tested,
then presented as proof the bug is broader than reported.

## Steps

**Where it lives.** The repro report's Steps section and the command
lines inside its code blocks (lines starting `$`, `>>>`, or described
UI actions like "press `s`, type a name, Enter"). Inputs the steps use
may be inline (a heredoc, a `printf` into a file, a pasted config), a
public link (a playground URL), or "the issue's script verbatim".

**What good looks like (followable).** A stranger holding only the
posted comment could run it: a starting state is named (a fresh
directory, a fresh `git init`, a clean install of version X), every
command is given, and every file or config the commands read is shown
or publicly reachable. Terse is fine: four lines of shell that do all
of this pass.

**What good looks like (trigger fidelity).** Put the report's commands
beside the issue's reproduction and compare token by token where it
matters:

- The same command shape and flags, including any flag the thread says
  is required to trigger it (e.g. `--replace`, `--exec-batch`, a
  specific `--driver`).
- The same input features: the same operator or separator (`=` vs `:`),
  the same range syntax (offset-from-end vs prefix), the same bound
  variables, the same selector-list shape.
- A report that swaps in "an equivalent" input must say so, and the
  swap must keep the trigger. An unexplained edit that removes the
  trigger fails even if everything else is excellent.

**Common failures.** The reproduction lives in a private repo or uses
an unshared config. A required flag or driver is dropped. The input was
modified so a different code path runs.

## Behavior shown

**Where it lives.** The artifacts in the repro report: output
excerpts, logs, tracebacks, exit codes, rendered or produced output
(CSS, prompts, JSON), terminal escape-sequence replies, `git status`
style state checks. Prose describing a screenshot is not an artifact;
the bundle only contains text, so read what the text actually shows.

**What good looks like.** Identify the issue's specific behavior
first, then find it in the artifact:

- **Failure kind.** A panic / crash / abort (Rust exit 101, a stack
  trace, the process dying) is not the same behavior as a graceful
  validation or syntax error (exit 1, "error: invalid range", "syntax
  error"). A compile-time error ("$b is not defined") is not the
  runtime error the issue reports ("Invalid path expression").
- **Message and output.** The same error message class, the same wrong
  output (wrong line numbers, a missing header, an unscoped selector,
  a stray token), or the same missing element.
- **Survival.** If the issue says the program crashes, an artifact where
  the program is still running afterward ("the prompt returned") does
  not show it.
- **Setup is not behavior.** A version banner, a session list, or "the
  tabs are visible" shows the program runs, not that the bug happened.
- **Cannot-reproduce.** When the report says it could not reproduce,
  the artifact must show the outcome of running the issue's trigger
  (the log order, the rendered prompt), so a reader can see the attempt
  really exercised it.

A control run (same steps, trigger removed) whose output differs the
way the issue predicts is the strongest artifact, and it is what most
clear accepts in this set have. It is preferred, not required.

## Honesty

**Where it lives.** Every sentence in the claim comment and the repro
report that asserts something: "I reproduced", "confirmed", "verified",
"guaranteed reproducible", "the cause is", "this matches exactly", and
the report's Expected / Actual lines. Read each one against the
artifacts; the question is whether the package contains the thing the
sentence claims.

**What good looks like.**

- Every reproduction claim points at an artifact that shows it. Every
  cause asserted is either shown (a trace, a log line, a bisect result)
  or clearly labelled as a hypothesis ("suggests", "looks like").
- The Actual line describes what the artifact shows, not what the
  issue says. If the artifact shows garbled output and a live prompt,
  "the terminal crashed" is a misdescription.
- An honest cannot-reproduce passes: it says so up front, shows the
  attempt with artifacts, states which scenario was and was not tested,
  and names what differed from the report (OS, shell, limits, input
  distribution) and what a triggering setup likely needs.
- Certainty scales with evidence. "Two machines, 100% confirmed" over a
  wrong-target artifact, or "I verified this race condition" with no
  transcript, fails.

**Common failures.** A confident root-cause diagnosis with no evidence.
Enthusiastic confirmation with zero artifacts. Narration that
describes an adjacent artifact as the reported bug. An "Expected" line
stated backwards from the issue.

## Comms

**Where it lives.**

- The claim comment, read against the issue title and body.
- The claim comment and repro report, read against the contribution
  policy line in the repo-facts block (live: `CONTRIBUTING.md` and any
  AI policy file it links).
- The bug-report template line in the repo-facts block (live: the
  repo's issue templates), read against the repro report.

**What good looks like (claim comment).**

- It names something specific to this issue (the behavior, the version
  it was reproduced on, the code path or thread pointer it will start
  from). Swap test: if the comment would read the same pasted onto a
  different issue, it fails.
- It states a modest, concrete next step. "I'll check X and report
  back" is fine. A deadline or a guarantee ("fixed within 2 days
  guaranteed"), a request to reserve the issue, or a bare "+1 / same
  here" with no intent fails.

**What good looks like (AI policy).** In this course every package is
AI-assisted work, so the policy always applies. Read the policy line
and classify it:

| Policy says | Grade |
|---|---|
| Nothing about AI ("no stated AI policy") | pass |
| AI welcome, contributor responsible / must understand the work (no disclosure ask) | pass |
| Disclosure required, but only in pull requests; no ask for issue comments | pass |
| Comments to maintainers must be in the contributor's own words | pass if the comments are first-person and specific to this issue; fail if boilerplate |
| All AI usage in any form must be disclosed (covers issues and comments) | pass only if the claim comment or repro report contains a disclosure of AI assistance |
| Outright ban on AI-assisted contributions of this kind | fail |

Conditions are not bans. A disclosure like "I used an AI assistant to
help organize this report; I ran and verified every step myself" is
what the conditional-policy pass looks like. An excellent reproduction
still fails this check on a repo that requires disclosure and gets
none.

**What good looks like (template asks).** Each item the repo's
bug-report template asks for (version, OS, install method, logs,
`conda info`, a playground link) appears in the report or its absence
is explained. This is a preferred check: a report can miss a template
field and still be ready.

## Reading the bundle honestly

The bundle is frozen on its capture date. Grade what it contains, not
what the live issue shows today. In eval mode the bundle is the whole
world: if the evidence a check needs is not in it, the grade is
`unclear`, and the verdict rule treats that as a fail.
