# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The repro report's environment record, read against the version the issue targets and the repo-facts block's bug-report template asks | The record names the OS, runtime version, and repo version or commit as concrete values, AND the version tested is the one the issue targets (or the version the repo's template asks reporters to test, such as latest release or main). A run on an older version passes only if the report explicitly flags the mismatch and doesn't claim to have confirmed the issue as reported | required |
| steps-followable | The repro report's steps, read in order from a fresh clone to the observed behavior | A stranger starting from a fresh clone could reach the observed behavior without guessing any command, input, file, or config value; nothing the run depended on is left unstated | required |
| behavior-matches-issue | The artifacts (output excerpt, error text, screenshot) read against the behavior the issue describes | The artifacts show the same failure the issue describes, in the same feature, not a different error or a neighboring bug | required |
| outcome-honest | The report's stated outcome read against its own artifacts | The stated outcome (reproduced, cannot reproduce, or partial) is exactly what the artifacts support. An evidenced cannot-reproduce that shows what was tried and what happened instead passes; claiming a reproduction the artifacts don't show fails | required |
| repo-conventions | The repo-facts block's contribution policy, including any AI-use policy, read against the claim comment and the repro comment | Every policy the repo states for contributor comments is met. Only when the policy explicitly requires disclosing AI use must each comment contain a disclosure statement (the tool and extent, or that no AI was used); on those repos a comment with no disclosure statement fails. When a policy restricts AI use without requiring disclosure (for example, "comments must be written by humans"), the comment passes unless its text shows the rule was broken; never presume AI use. If the repo states no AI policy, this passes | required |
| own-proof | The repro comment, read against earlier comments on the issue | The comment presents the author's own evidence in their own words, not "same as above," "+1," or "can confirm" resting on someone else's report | required |
| claim-specific | The claim comment, read against the issue | The claim names something specific to this issue (the feature, error, or symptom) and the author's next step, promises the investigation and report rather than asserting a result not yet obtained, and promises no fix or date | required |
| tested-on-current | The environment record's commit, read against the repo's default branch in the repo-facts block | The run used the current default branch or says why it didn't | preferred |

## Verdict rule

Accept if every applicable required check passes; otherwise reject.
Preferred checks never change the verdict. An `unclear` grade on a
required check counts as fail, since posting on evidence the grader
can't confirm is what this rubric exists to stop.

On a claim-only draft (no repro report yet), environment-recorded,
steps-followable, behavior-matches-issue, outcome-honest, own-proof,
and tested-on-current report as not yet applicable and are left out
of the verdict. claim-specific and repo-conventions still apply.
