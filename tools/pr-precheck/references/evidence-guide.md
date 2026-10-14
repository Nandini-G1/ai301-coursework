# Evidence guide: where evidence lives in a PR package

Each family below matches one failure category. A package that fails none of them is a clear accept. For each family: where the evidence lives in an eval bundle, where it lives in a live run on Path Review, and what good looks like.

## Plan fidelity (harness category: silent-drift)

Where it lives, eval bundle: the "Plan context" block holds the accepted plan. Its scope pair is the "Scope, one bounded change" sentence and the "Not in scope" sentence; its named files follow "Files:"; deviation and deferral notes appear as "Known limit", "Deliberately deferred", or "Deviation note". The diff is the "Diff" section of the "Candidate PR"; changed files are the `+++ b/` lines. The description's fidelity claims are in the "Description" section.

Where it lives, live: `plan.md` (its scope, files, and test plan, and everything under `## Deviations`) against `git diff main...HEAD` and its `--stat` file list; the description is `pr_draft.md` below its first line.

What good looks like: every changed file falls inside the plan's named files or a deviation note, every hunk serves a plan step, nothing the plan scopes out appears, and every plan step is in the diff or disclosed as deferred. Silent drift runs in both directions: more than the plan (a new option, flag, setting, renaming pass, or rewritten helper nobody planned) or less than the plan with no note (a promised docs update missing). A description that says "exactly as planned", "no other changes", or "in full" over a diff that departs from the plan is silent drift too, not a comms issue. An honest deviation note, in the plan or restated in the description, re-ties the mismatch and makes it pass.

## Test evidence (harness category: not-tested)

Where it lives, eval bundle: the "Test evidence" section of the candidate PR, sometimes with before/after output in the "Description". Read it against the plan's "Test plan" sentence (each scenario and its expected-after) and the "Repro evidence" line that the plan built on. The repo's own checks are named in the repo-facts block ("pass cargo test", "yarn test", "pre-commit").

Where it lives, live: `test_evidence.md` and the Testing section of `pr_draft.md`, read against the test plan in `plan.md` and your unit 2 repro steps. Path Review's checks are the four in its PR template: `make test-unit`, `make test-integration` (which currently reports "no tests ran", the expected honest result), `make lint`, `make typecheck`. The CI box stays unticked before the PR is opened.

What good looks like: the plan's failing scenario itself, with the same input, re-run on the branch, with the command and its actual after output shown next to the before (for example, `before: ESC[?997;2n` / `after: ESC[?997;1n`); every scenario the test plan names is covered; each repo check is named with its outcome. Not decisive: "tested locally, works now", "verified on my machine for a day", "all tests pass" with nothing named, evidence that runs only a single-file control or a GET when the bug was a POST, and a ticked box with no output behind it. A failing check reported with its reason is still evidence.

## Diff quality (harness category: unreviewable)

Where it lives, eval bundle: every hunk of the "Diff" section and the "Commits" list.

Where it lives, live: `git diff main...HEAD` hunk by hunk, and `git log --oneline main..HEAD`.

What good looks like: every added and removed line serves the fix, its tests, or a required entry (changelog, i18n). Debris tells: an added `print`, `eprintln!`, `console.log`, or `DEBUG` line; commented-out code or an earlier attempt left commented; a function or variable nothing calls (often behind `allow(dead_code)` or a leading underscore); a new TODO or FIXME; re-indented or reformatted lines whose logic did not change; import reordering the new code does not need; lines that were deleted and re-added identically; an edit to a file or function unrelated to the issue. Commit messages like "wip", "fix", "fmt + cleanup", or "misc cleanups while debugging" usually point at debris in the hunks. One debris hunk is enough to make the diff unreviewable.

## Standards and comms (harness category: standards-wall)

Where it lives, eval bundle: the repo-facts block's "pull requests" line (template sections, required checklist, issue-link form, required entries such as CHANGELOG.md or whatsnew) and its "contribution policy" line (including any AI-use policy, and whether it requires disclosure). The PR meets them in the "Title", "Description", and "Diff". Maintainer direction lives in "Thread highlights".

Where it lives, live: `.github/PULL_REQUEST_TEMPLATE.md` (sections Summary, Issue with "Closes #", Changes, Testing checklist, Screenshots / Demo, Notes for Reviewers), `docs/CONTRIBUTING.md` (branch naming `<type>/<issue-number>-<short-description>`, Conventional Commits, xfail marker removal for seeded bugs, no bulk lint fixes), `scope.md`'s house rules, and the issue thread. The course requires an AI-use disclosure in Notes for Reviewers, in the author's own words. The branch name comes from `git branch --show-current`.

What good looks like: every required template section is present and carries real content written for this change, not placeholder text; each required checklist item is addressed truthfully; the issue is linked in the form the template asks for; every required entry file is in the diff; and when the stated policy requires AI disclosure, the description says that AI was used and how much. Visibly ignored asks look like a template checklist that never appears, a missing "closes #" the template requires, a required whatsnew or changelog entry absent from the diff, or no disclosure under a policy that demands one. When the repo states no template and no AI policy, there is nothing to ignore, and the family passes. Whether the description's claims are true is plan fidelity, above, not this family.
