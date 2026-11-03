# Contribution: snake_case sweep: rename camelCase/Hungarian leftovers in test toolchain
Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Vishwanandini Reddy Gajjala
**GitHub Username:** Nandini-G1
**Issue:** https://github.com/MFlowCode/MFC/issues/1506
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built my issue scout and fixed two rubric gaps that real scans exposed**

I turned my unit-1 issue-select skill into a scout with two gh search issues queries from my fit profile (Python issues labeled good first issue plus bug or tests) and six ranking rules. Running my bug query by hand first showed a few repos had bulk-filed many issues at once, which would have filled the whole top 5, so I added a one-result-per-repo rule before my first scan. The scan accepted all 5 picks, but repo-in-use passed brand-new single-person repos (one was created a week before), so I added a rule that fails repos less than 90 days old. Grading my site picks showed a second gap: unassigned only checks open PRs, so it accepted MFC#1509 even though merged PRs had already fixed both parts; I logged a patch for that check, and I now open an issue’s Development sidebar before claiming anything.

**Unit 6: Installed the voice guard on one merged voice guide and wrote a scoped memory file for MFC**

I merged my three voice-guide copies into one (the repro-check copy was missing my unit-3 plan rule), added Upstream rules for claims, questions, and pings, and installed the voice guard; the wiring test was blocked, as it should be. Before installing, I noticed my guide contradicted itself: an old rule said "no dates," but my new claim rule asks for a report-back window, so I reworded the old rule to forbid only fix dates. My claim draft passed repro-check, but the voice check said my question only repeated the issue instead of saying what I had checked, so I confirmed the names were still on master and added that before the guard let the post through. For my CLAUDE.local.md, the scoped orientation turned up more camelCase names than the issue lists, so I read the full issue and wrote down exactly which names are in scope, and I recorded `./mfc.sh test --list` as a way to prove no test case changes without building any Fortran.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched two ways. My scout ran two gh search issues queries from my fit profile (Python issues labeled good first issue plus bug or tests). Its first scan found 198 issues and accepted all five it graded, but four came from repos only weeks old and one was entirely React. My real candidates came from the AI301 Issue Selection site, filtered to Python. I graded four: MFC#1509 was accepted but had already been fixed by merged PRs, Red-DiscordBot#6794 was rejected because four PRs were already open, and proCAT#862 was accepted as moderate and was my first choice, but another contributor asked to work on it a few hours after it was opened, just before I claimed it. MFC#1506 was accepted both times I graded it, and after this week’s scope patch its difficulty note said straightforward: the issue names the exact files and identifiers, but it’s about 80 renames, each of which has to be checked inside its own function. It fits most of my profile: it’s all Python, in an active project with regular releases, and has no front-end or build work. It doesn’t cover two of my learning goals, since there’s no bug to reproduce and no failing test to write. It does cover the third, scoping a change small enough for a maintainer to review quickly, which is why my claim asks whether they want one PR or three. I want to learn how a large project reviews a careful mechanical change, especially one whose PR template warns against low-effort submissions. My claim: https://github.com/MFlowCode/MFC/issues/1506#issuecomment-6593204160

Honestly, my scout helped and fell short in about equal measure. It correctly rejected Red-DiscordBot#6794, and its re-check of the current code is how I know #1506’s renames are still undone. But on a real search, repo-in-use passed brand-new, single-person repos, so I added a rule that fails repos less than 90 days old. And unassigned only looks at open PRs, so it accepted MFC#1509 even though merged PRs had already done the work. I logged a patch for that and now check an issue’s Development sidebar myself before claiming. Its maintainer-responsive check also failed for MFC, so I’m going in knowing replies may be slow.

**Toolkit**
- Tool: issue-scout (my search strategy and rubric). I ran one scan, graded my Issue Selection picks, then regraded them after the unit 6 patch.
- What it produced: a scan of 198 issues with the top 5 graded (all accepted), then grades for 4 site picks. For MFC#1506: accept both times, 3 of 4 preferred checks (maintainer-responsive failed), difficulty note "straightforward but large."
- Difficulties: repo-in-use passed weeks-old single-person repos; unassigned missed work already done by merged PRs (MFC#1509); my tests query never reached the top 5.
- What changed: added a 90-day repo-age rule to repo-in-use and a one-result-per-repo ranking filter; in unit 6 replaced my bounded-scope check with scope-feasible plus a difficulty note; I now check the Development sidebar before claiming.

---

## Understanding the Issue

**Problem Description**

MFC's Python toolchain uses snake_case, but its test runner in `toolchain/mfc/test/` still has camelCase and Hungarian-notation local variables and parameters, like `newTrace`, `bFoundFrom`, `nAttempts` and `dimInfo`. Nothing breaks at runtime; it's a consistency and readability problem that the linter never flags.

**Expected Behavior**

The 11 names the issue lists use snake_case (`new_trace`, `found_from`, `n_attempts`, `dim_info` and so on), and nothing else changes: the same test cases with the same UUIDs and parameters, and the same tests passing.

**Current Behavior**

All 11 names are still on master (a03848a): for example, `def define_case_d(stack, newTrace, newMods, ...)` in case.py and `nAttempts = 0` in test.py. `dimInfo` alone is on 113 lines of cases.py.

**Affected Components**

`toolchain/mfc/test/case.py` (`define_case_d`), `toolchain/mfc/test/test.py` (`__filter`, `handle_case`) and `toolchain/mfc/test/cases.py` (`get_bc_mods`, `get_dimensions`, `foreach_dimension`, the `alter_*` helpers, the example skip list and the case-size check). Also three places that mention `casesToSkip` by name: `docs/documentation/testing.md`, `docs/documentation/contributing.md` and a message in `toolchain/mfc/lint_test_suite.py`.

**Toolkit**

- Tool: my CLAUDE.local.md memory file, built from one scoped orientation run over `toolchain/mfc/test/`, plus a whole-repo search for each name.
- What it produced: the three files, how they connect (cases.py builds every case through case.py's `define_case_d`; test.py filters and runs them), and which tests cover them (none cover case.py or cases.py directly).
- Difficulties: the orientation listed more camelCase names than the issue does, and the issue's line numbers were from an older commit. The orientation also missed that `casesToSkip` is named in two docs pages and a lint message; I only found that by searching the whole repo for each name.
- What changed: I wrote the issue's exact list of names into my memory file as the scope, and added the three `casesToSkip` mentions to my plan.

---

## Reproduction Process

**Environment Setup**

macOS 26.5.2 on Apple Silicon, Python 3.14.7. I forked MFlowCode/MFC with `gh repo fork --clone`, synced my fork's master to upstream (a03848a, 2026-10-31), and ran `./mfc.sh lint`, which set up MFC's own Python environment (build/venv; MFC supports Python 3.9–3.14). No Fortran build is needed, because the issue only touches the Python toolchain.

Challenges: `./mfc.sh test --list` stopped because it needs CMake, which isn't installed (MFC can't fetch it for macOS arm64). Instead of installing it, I listed every test case by calling MFC's own `list_cases()` with a four-line script, which also prints each case's parameters. Unchanged master also doesn't pass every check on my laptop: `./mfc.sh lint` has 4 failing tests (test_archive.py::test_format_tar_zst and three in test_bench_preflight.py), and `./mfc.sh precheck` fails 2 of 7 steps (toolchain lint, because of those same tests, and example case validation). None of these touch the files in the issue, so I'm treating them as my environment's baseline: after the renames, the same failures should appear and nothing new.

**Steps to Reproduce**

1. Clone MFC and check out a03848a (current master).
2. For each name the issue lists, count the lines containing it: `grep -c -w <name> toolchain/mfc/test/case.py toolchain/mfc/test/test.py toolchain/mfc/test/cases.py`
3. Run `./mfc.sh lint` and `./mfc.sh precheck` for a baseline.
4. List every test case with its UUID, trace and parameters: `build/venv/bin/python dump_cases.py > cases-before.txt`, where dump_cases.py imports `list_cases` from `toolchain/mfc/test/cases.py` and prints `get_uuid()`, `trace` and the sorted `mods` for each case.
5. Observed result: all 11 listed names are still on master; lint is 777 passed, 21 skipped, 4 failed; precheck is 5/7; 776 test cases are listed.

**Reproduction Evidence**

- **Commit showing reproduction:** none (no code changed yet)
- **Screenshots/logs:** lines containing each name on a03848a: newTrace 4, newMods 2 (case.py); bFoundFrom 3, bFoundTo 3, nAttempts 8 (test.py); dimInfo 113, dimCmp 4, dimParams 13, patchID 20, casesToSkip 2, caseSize 3 (cases.py). Example: case.py:453 `def define_case_d(stack: CaseGeneratorStack, newTrace: str, newMods: dict, ...)`; test.py:239 `bFoundFrom, bFoundTo = (False, False)`; test.py:915 `nAttempts = 0`.
- **My findings:** The issue is real today: every name it lists is still on master. Its line numbers come from an older commit (40dde5e), so I go by names, not line numbers (define_case_d is now at line 453, not 442). My scoped orientation also found camelCase names the issue doesn't list (the n* module globals in test.py; couplingMethod, dragModel and fdOrder in cases.py); I'm leaving those out to keep the PR to what the maintainer asked for. No unit test covers case.py or cases.py directly, which is why I saved the full case list as a before/after check.

**Toolkit**

- Tool: repro-check with the wild scope, grading my claim and repro report together.
- What it produced: accept, with all 7 required checks and the preferred tested-on-current check passing.
- Difficulties: it called my claim's grade "after the fact," though I had checked the first version before posting and the final edit went through the voice guard; it also said the report was "ready to go" as a comment, but the course says not to post it. Its useful catch: `grep -c` counts lines, not uses, so "dimInfo 113" could be read as a total.
- What changed: I reworded the counts as "lines containing," ran `./mfc.sh precheck` as well as lint so my report matches what my claim promised, and kept the report off the issue thread.

---

## Solution Approach

**Analysis**

The names the issue lists predate the toolchain's snake_case convention, and they survived because MFC's `.ruff.toml` selects only the E, F, W, I and PL rule sets. It doesn't enable N (pep8-naming), so nothing flags camelCase or Hungarian local names. All 11 names are local variables or function parameters: `newTrace` and `newMods` are parameters of `define_case_d` in `toolchain/mfc/test/case.py`, and all 170 calls in `cases.py` pass them by position; `bFoundFrom`/`bFoundTo` are locals in `__filter()` and `nAttempts` is a local in `handle_case()` in `test.py`; `dimInfo`, `dimCmp`, `dimParams` and `patchID` are parameters and locals in `get_bc_mods`, `get_dimensions`, `foreach_dimension` and the `alter_*` helpers in `cases.py`, and `casesToSkip` and `caseSize` are locals there too. None is used as a keyword argument or a global, and none appears elsewhere in the toolchain code. Two risks: several `alter_*` helpers are nested closures that read the enclosing function's `dimInfo`, so each rename has to cover the enclosing function and every closure inside it together; and `casesToSkip` is named outside the code, in `docs/documentation/testing.md`, `docs/documentation/contributing.md` and a message in `toolchain/mfc/lint_test_suite.py`.

**Proposed Solution**

Rename exactly the 11 names the issue lists to snake_case, function by function, and update the three mentions of `casesToSkip` so the docs and the lint message still point to a real name. Nothing should change in behavior: the same 776 test cases, with the same UUIDs and parameters, and the same tests passing. I'm deliberately not changing: camelCase names the issue doesn't list (the n* module globals in test.py; couplingMethod, dragModel and fdOrder in cases.py), MFC's ruff configuration (enabling N rules would be a separate decision for the maintainers), or formatting on lines I don't touch. I'll open one combined PR, since the issue says "File as one combined issue", unless a maintainer answers my question on the thread differently.

**Implementation Plan**

1. Create a branch, `feature/1506-snake-case`, on my fork (Nandini-G1/MFC) from master a03848a, following contributing.md's `feature/<short-name>` convention; the PR goes from my fork to `MFlowCode/MFC:master`.
2. case.py: rename `newTrace` → `new_trace` and `newMods` → `new_mods` in `define_case_d`. Commit.
3. test.py: rename `bFoundFrom`/`bFoundTo` → `found_from`/`found_to` in `__filter()`, and `nAttempts` → `n_attempts` in `handle_case()`. Commit.
4. cases.py: rename `dimInfo` → `dim_info`, `dimCmp` → `dim_cmp`, `dimParams` → `dim_params` and `patchID` → `patch_id` one function at a time, renaming each enclosing function together with its closures; then `casesToSkip` → `cases_to_skip` and `caseSize` → `case_size`. Commit.
5. Update the three mentions of `casesToSkip` (testing.md, contributing.md, lint_test_suite.py) to `cases_to_skip`. Commit.
6. Verify: `grep -c -w` finds 0 lines for every old name; the test-case list from `list_cases()` is identical before and after (776 cases); `./mfc.sh lint`, which the issue asks for, gives the same result as on master (777 passed, the same 4 environment failures), and the spell check passes; `./mfc.sh precheck` gives the same 5 of 7 passing steps I recorded on master during reproduction.

**Proposed Solution**

Deviations: none yet.

**Toolkit**

- Tool: plan-check, grading plan.md and a draft plan comment (not posted) against the issue thread.
- What it produced: accept, with all five required checks and the preferred honest-unknowns check passing; it re-checked my facts against the code (ruff's rule sets, the 170 calls, the three casesToSkip mentions).
- Difficulties: my branch name didn't follow MFC's `feature/<short-name>` convention; my test step named my private manifest instead of `./mfc.sh lint`, which the maintainer asked for; "same 5 of 7" wasn't backed by anything plan-check could see; and my comment read "one combined issue" as "one PR". Its own procedure assumes eval-mode inputs and has no step for a refactor with no bug to reproduce.
- What changed: I renamed the branch to `feature/1506-snake-case`, named `./mfc.sh lint` and said where the precheck baseline comes from, and softened the one-PR line to say I'll split it if a maintainer asks.

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
