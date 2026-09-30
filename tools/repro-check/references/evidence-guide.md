# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives- Eval bundle: the environment record inside the
repro report, read against the issue context (what version or
platform the issue targets) and the repo-facts block (supported
versions, setup docs, default branch). Live mode: the environment
section of the student's draft repro comment, read against the issue
on GitHub and the repo's README, CONTRIBUTING, or setup docs.

What good looks like- The record names the OS, the
language/runtime version, and the repo commit or release as concrete
values. Those values match what the issue targets and what the repo
supports, or the report calls out the difference. "Latest," "my
laptop," or a missing commit means a stranger cannot rebuild the run. A reproduction on an older version than the issue targets does not confirm the issue unless the report flags the gap and softens its claim.

## Steps

Where it lives- Eval bundle: the steps section of the repro
report. Live mode: the steps in the student's draft repro comment,
read against the repo's own setup docs.

What good looks like- Starting from a fresh clone, every command,
input, file, and config value needed to reach the behavior is
written down. A reader never has to guess or already know something
the steps leave out. Setup the repo docs already cover can be linked
rather than repeated, as long as the link points at the exact
instructions used.

## Behavior shown

Where it lives- Eval bundle: the artifacts in the repro report
(output excerpts, error text, logs, screenshots), read against the
behavior described in the issue context. Live mode: the artifacts in
the draft repro comment, read against the issue's description and any
error it quotes.

What good looks like- The artifact shows the same symptom the
issue describes, in the same feature: the same error message or
wrong output under the same trigger. An artifact that shows a
different error, a different feature, or a failure the steps caused
some other way is adjacent, not a match, even if it looks similar.


## Honesty

Where it lives- Eval bundle: the outcome the repro report states
(reproduced, cannot reproduce, partial), read against that report's
own artifacts. Live mode: the outcome sentence in the draft repro
comment, read against the artifacts in the same comment.

What good looks like- The stated outcome claims exactly what the
artifacts show and no more. A cannot-reproduce is honest when it
shows what was tried and what happened instead. A report is
dishonest when it says "reproduced" but the artifacts don't show the
issue's behavior, or states certainty the evidence doesn't support.

## Comms

Where it lives- Eval bundle: the claim comment and repro comment,
read against the issue context, the repo-facts block's stated
policies (comment templates, contribution rules, AI-use disclosure
requirements), and any earlier comments included in the issue
context. Live mode: the student's draft comments, read against the
issue thread on GitHub and the repo's CONTRIBUTING file or policy
docs.

What good looks like-
- Conventions: every policy the repo states for comments is followed.
  Tell the two kinds of AI policy apart. If the policy explicitly
  requires disclosure ("all AI usage must be disclosed"), the comment
  must carry a disclosure statement, and silence fails. If the policy
  only restricts AI use ("comments must be human-written"), the comment
  passes unless its text shows a violation; never presume AI was used.
  If the repo states no policy, there is nothing to violate.
