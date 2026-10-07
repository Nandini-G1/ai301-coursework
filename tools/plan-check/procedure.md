# Procedure: how this skill grades a plan package

## Read order

1. Read the repo-facts block first. Write down the contribution policy's AI rule in one line: does it require disclosure in issues or comments (yes / pull requests only / no policy)?
2. Read the issue and the thread highlights. List every comment from an OWNER, MEMBER, or COLLABORATOR account that gives direction: a diagnosis, a preferred fix, a patch, or a request. If there are none, write "no maintainer direction".
3. Read the repro evidence before the plan. Write down: what each step shows, every control run and what it rules in or out, and the Actual result. Reading this first means the plan's cause gets judged against the evidence, not the other way round.
4. Read the candidate plan. Note its stated cause, its change list, its in/out-of-scope lines, the files and functions it names, its approach, its test plan, and its unknowns.
5. Read the candidate plan comment last, since it is graded against the thread and policy you already noted.

## Evidence gathering

1. grounded-cause: copy the plan's cause in one line. Next to it, copy each repro step or control run that bears on that cause (the step number and what it showed).
2. bounded-scope: list every change the plan commits to doing (not things it defers). Mark each "needed for the repro's expected behavior", "regression test", or "extra".
3. executable: copy the named files/functions/sites and the chosen approach. If the plan offers alternatives without choosing, copy that wording.
4. decisive-test: copy the test plan's action and its expected result, and the repro's Actual result it should differ from.
5. thread-and-policy: use the notes from read-order steps 1 and 2. Copy any comment sentence that engages each maintainer direction, and any sentence that discloses AI use.
6. honest-unknowns: copy the plan's stated unknowns and any claim written as certain that the repro does not show.

## Check execution

1. Run the checks in the rubric's table order: grounded-cause, bounded-scope, executable, decisive-test, thread-and-policy, honest-unknowns.
2. Grade each check only from the evidence recorded for it, applying the rubric's pass condition word for word. Do not grade on length, tone, or formatting.
3. Run every check even after one fails, so the output shows every problem.
4. If the package does not contain the evidence a check needs (for example, the plan names no test at all), grade it fail, not unclear. Use unclear only when the evidence is present but could honestly be read either way, and say what makes it ambiguous.
5. Write one line of evidence for each grade: the quote or fact that decided it.

## Verdict assembly

1. Collect the grades of the required checks.
2. If every required check is pass, the verdict is accept.
3. If any required check is fail or unclear, the verdict is reject.
4. Ignore the grade of honest-unknowns for the verdict; report it in the summary only.
5. In the summary, name the required check that decided a reject and quote its evidence line. Then emit the JSON block last, as SKILL.md specifies.
