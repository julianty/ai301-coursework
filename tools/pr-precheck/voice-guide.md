# Voice guide: how I talk upstream

## Who I am in threads

I'm a student without much experience with open source contributions. I am courteous and give space and grace to others. I don't submit code that I don't check myself, especially AI generated code.

## Rules I write by

### Rule: Be courteous when correcting others

I have to conduct myself in a manner that shows respect to others. When I disagree with someone's comment or code, say what I checked and ask a question before stating a conclusion.

- Wrong: "This fix is wrong, the fixture is the problem."
- Right: "I think the fixture might be the cause: when I dedented it, the headings came back. Did you see something different?"

### Rule: Check my own code

Because I use AI tools, I have to self-govern and ensure that I both disclose AI tool usage, and be accountable for its usability.

- Wrong: "I had Claude write this, it said it worked so I committed and opened a PR"
- Right: "I had Claude help generate this code, but I reviewed it myself and wrote some tests to ensure it works."

### Rule: Be honest about claims

I want to make sure that I don't make claims without sufficient evidence. This is the basis of trust.

- Wrong: "The parser's heading pattern requires # at the start of a line."
- Right: "Reading the source, the parser only treats a line as a heading if # is its first character [followed by a direct link to source code]"

### Rule: A PR title says what the change does

A title is read in a list of many PRs, so it names the change in the fewest words, in the imperative, and names the issue it fixes. It does not promise a result.

- Wrong: "Fixes everything in the parser"
- Right: "Fix heading detection when # is not the first character (#123)"

### Rule: A PR description claims only what the diff contains

Every behavior the description says the change adds or fixes must appear in the diff, and every test it names must have been run. If the description says "tested", it names the test and its output.

- Wrong: "Handles all edge cases for headings and passes the suite."
- Right: "Handles headings with leading spaces. I ran `pytest tests/test_headings.py`: 4 passed. I did not run the full suite."

### Rule: Disclose shortfalls plainly, without apology

A known gap goes in the disclosure section in one plain sentence: what is missing and why. Don't apologize for it, and don't hide it in a vague phrase.

- Wrong: "Sorry, I ran out of time, so some of this might be rough and I hope it's okay."
- Right: "Not done: the nested-list case. I did not have time to write a test for it, so it is untested."

## Things I never post

- A deadline or a guarantee ("PR by Friday", "this will definitely fix it")
- Output I didn't run myself, or edited output that isn't marked as edited
- An AI-drafted comment that I haven't rewritten in my own words
- "Same as above" / "+1" in place of my own work
- A PR description that claims coverage, a passing run, or a fix the diff and test evidence do not show
- A title or description that says "all", "fully", or "complete" without a test or a diff behind the word
