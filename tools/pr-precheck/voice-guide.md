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

I'm a new contributor working through my first contributions to this repo, with 2 years of experience in python and Java. I'm here to reproduce bugs carefully and report exactly what I find. Readers can expect specifics and honest results.

## Rules I write by

### Rule: Promise the investigation, not the fix

I commit only to what I'll do next and to reporting back. No fixes,
no dates.

- Wrong: "I'll have a fix for this up by Friday!"
- Right: "I'm going to try to reproduce this on the current main
  branch and will post what I find here."

### Rule: Name this issue's specifics

Every comment mentions something only this issue has: the feature,
the error, or the trigger.

- Wrong: "Hi, I'd like to work on this issue."
- Right: "I'd like to take this. I'll start by trying to reproduce
  the [specific error] when [specific trigger]."

### Rule: Say only what my evidence shows

If I didn't see it happen, I don't say it happened. A cannot-reproduce
is a real result.

- Wrong: "Reproduced, it's definitely the parser."
- Right: "I couldn't reproduce this on [version]. Here's what I ran
  and what I saw instead."

### Rule: My proof, my words

I post my own evidence even when someone else already reproduced it.

- Wrong: "Same as above, can confirm."
- Right: "I also reproduced this. Here's my environment and output."

### Rule: Disclose AI help when the repo asks

If the repo's policy requires disclosing AI assistance, I say so
plainly in the comment.

- Wrong: [a comment with no disclosure on a repo that requires one]
- Right: "Note: I used an AI assistant to help draft this comment,
  per the project's contribution policy."

### Rule: In a plan, commit to the approach and label what I haven't checked

In a plan comment I name the one approach I will build, and anything I
haven't verified myself gets "I expect" or "open question". This
replaces "promise the investigation" once I have a reproduction. Still
no dates.

- Wrong: "The fix is the regex, which also fixes the markdown tests.
  PR by Friday."
- Right: "Plan: allow leading spaces in the `_detect_sections()`
  patterns. I expect this also explains the two markdown tests; I'll
  confirm during the build."

## Things I never post

- A fix or a deadline I haven't earned yet.
- "+1," "same here," or "can confirm" with no evidence of my own.
- "Reproduced" when my output shows a different error.
- A comment I haven't run through repro-check
- Impatience with maintainers who haven't replied

- A plan comment I haven't run through plan-check.
- A plan that is "same approach as above" instead of my own diagnosis.
