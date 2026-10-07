# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- Where it lives: eval mode, the "Cause:" or "Diagnosis:" line of the Candidate plan, read against the Repro evidence block's numbered steps, control runs, and any --debug, timing, or intermediate output. Live mode, the cause section of plan.md, read against the student's posted repro comment (or the house repro pack as quoted in the drafts).
- What good looks like: the cause explains every repro observation, and no control run shows the bug happening where the cause is absent or the blamed part working fine. A confident cause adopted from the thread still fails if the repro's own control rules it out.

## Scope

- Where it lives: the Candidate plan's "Change:" paragraph and its "In:" / "Not in scope:" lines; in live mode, plan.md's scope and files sections.
- What good looks like: one change at the site the repro points to, plus regression tests, with related work explicitly deferred. A bounded fix bundled with migrations, rewrites, new options, or "while I'm here" work is not bounded, even if the core fix is right.

## Executability

- Where it lives: the file paths, function names, and "Approach:" text in the Candidate plan; in live mode, plan.md's files and approach sections.
- What good looks like: a named file or function and one chosen approach, so someone else could open the file and start. "Somewhere in the input stack", "upstream or vendored, whichever is easier", or "profile and see" means a stranger could not start.

## Test plan

- Where it lives: the Candidate plan's "Test:" or "Test plan:" section, read against the Repro evidence's steps and its "Actual:" line; in live mode, plan.md's test plan read against the posted repro steps.
- What good looks like: a named step, command, or test case plus the expected observable result that differs from the repro's Actual (an output line, exit code, color, visible state). "Run the full suite" or "should feel fast" names nothing observable.

## Honesty

- Where it lives: any unknowns, risks, or "open question" lines in the Candidate plan and comment; in live mode, plan.md's risks and unknowns section and its Deviations section after the build.
- What good looks like: unverified points are labeled as unknowns with how they'll be checked ("may be one layer up; will confirm while implementing"). Deviations from the posted plan are recorded in plan.md with what changed and why.

## Comms

- Where it lives: the Candidate plan comment, read against the Thread highlights (comments from OWNER, MEMBER, or COLLABORATOR accounts) and the Repo facts block's "contribution policy" line. In live mode, the draft comment.md read against the live issue thread and the repo's CONTRIBUTING and AI policy files.
- What good looks like: the comment names any maintainer direction (a diagnosis, preferred option, patch, or test request) and either follows it or explains the departure, and it mentions open PRs instead of racing them. If the policy requires AI use to be disclosed in issues or comments, the comment states the tool and extent; a PR-only disclosure rule does not apply to the comment. Every package is treated as AI-assisted.
