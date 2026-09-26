# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I'm a student without much experience with open source contributions. I am courteous and give space and grace to others. I don't submit code that I don't check myself, especially AI generated code.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

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

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- A deadline or a guarantee ("PR by Friday", "this will definitely fix it")
- Output I didn't run myself, or edited output that isn't marked as edited
- An AI-drafted comment that I haven't rewritten in my own words
- "Same as above" / "+1" in place of my own work
