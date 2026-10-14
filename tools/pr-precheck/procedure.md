# Procedure: how this tool grades a PR package

## Read order

Read the parts in this order, and take the notes listed under each before opening the next part. The plan comes before the diff and the diff comes before the description, so that you judge the diff against what was promised and judge the description against what the diff actually does, instead of letting the description tell you what the diff contains.

1. Live mode only: `scope.md` (apply the scope seam in SKILL.md before going on), then the branch name.
2. Repo standards (eval: the repo-facts block; live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`). Note: the template's required sections and checklist items, the issue-link form it asks for, any file a change must carry (changelog, whatsnew, i18n, docs), the suite or checks it names, and the AI-use policy, written as "requires disclosure" or "no disclosure requirement".
3. The issue and its thread. Note: the reported failing behavior, and any maintainer question or direction.
4. The plan (eval: the plan-context block; live: `plan.md` including `## Deviations`). Note four lists: the in-scope steps, the files it names, what it marks not in scope, and every deviation or deferral note. From its test plan, note each failing scenario to re-run with its expected-after, and any suite it names.
5. The diff (eval: the Diff section; live: `git diff main...HEAD`, with `--stat` for the file list). Note: every changed file, and for each hunk one line saying what it does.
6. The commit list (eval: the Commits section; live: `git log --oneline main..HEAD`).
7. The test evidence (eval: the Test evidence section; live: `test_evidence.md`). Note: each command shown, which scenario it exercises, and its output.
8. The title and description (eval: the Title and Description sections; live: `pr_draft.md`). Note: every factual claim about the change, every disclosure, the issue link, and which template sections are present and filled.

## Evidence gathering

Make these pairings, writing each result down before grading anything. Each pairing feeds the named check.

- Diff against plan (plan-fidelity). For each hunk from read step 5, find the plan step or deviation note it serves; mark any hunk with no match as "extra". For each plan step from read step 4, find the hunk that delivers it; mark any step with no hunk as "missing" unless a deviation, deferral, or the description discloses it. Check every extra hunk against the not-in-scope list.
- Description against diff (description-matches-diff). For each claim from read step 8, find the hunk that makes it true; mark claims with no hunk as "unbacked". Mark any "exactly as planned", "no other changes", or "in full" claim as false if the diff-against-plan pairing found an undisclosed extra or missing step.
- Evidence against test plan (repro-before-after). For each failing scenario from read step 4, find the command in read step 7 that re-runs that scenario (same inputs, same path), and record whether its after output and its before output are shown. Mark evidence that only runs a control, a different input, or an unchanged path as "wrong scenario".
- Evidence against stated checks (repo-checks-run). For each suite or check from read steps 2 and 4, find the line in the evidence that names it and its outcome. In live mode for Path Review, the four are `make test-unit`, `make test-integration` (where "no tests ran" is the expected, honest result), `make lint`, and `make typecheck`.
- Hunks against the debris list (diff-clean). Scan each hunk from read step 5 for added debug output, commented-out code, unused or dead code, TODO or FIXME, whitespace or formatting changes on untouched logic, import changes the new code does not need, and edits unrelated to the issue. Record the file and line of each.
- Asks against the PR (template-and-asks). For each ask from read step 2, record where the PR meets it (section, line, or diff file) or that it is absent. In live mode, also compare each ticked Testing box to the evidence, and run `grep -rn "issue #<N>:" tests` and check `pyproject.toml` for a suppression naming the issue.
- Policy against description (ai-disclosure). Record the policy note from read step 2 and quote the disclosure sentence, or record that none exists.
- Commit messages (commit-messages) and thread direction against description (thread-engaged): record the messages and any engagement sentence.

## Check execution

Grade the checks in rubric order: plan-fidelity, description-matches-diff, repro-before-after, repo-checks-run, diff-clean, template-and-asks, ai-disclosure, commit-messages, thread-engaged. Grade every check, even after one has failed.

For each check, apply its pass condition from `rubric.md` literally to the pairing recorded for it, and grade from those notes without re-reading the whole package; reopen only the one part the note points to if a note is ambiguous. Write the evidence line as the single fact that decided the grade: the extra hunk's file, the false claim quoted, the missing scenario, the debris line, the missing ask.

Grade `unclear` only when the evidence the check needs does not exist in the package (for example, no test-evidence section at all, or in live mode a missing `test_evidence.md`), and name what is missing. Do not grade `unclear` because a judgment is hard; make the call from the pass condition. Before failing plan-fidelity or description-matches-diff, check the deviation notes and the description once more for a disclosure of that exact item; a disclosed item does not fail.

## Verdict assembly

Apply the rubric's verdict rule: if every required check is `pass`, the verdict is accept; if any required check is `fail` or `unclear`, the verdict is reject. Ignore the preferred checks' grades for the verdict.

The deciding check is the first required check in rubric order whose grade is `fail` or `unclear`; for an accept, there is no deciding failure, so say "all required checks pass". Name the deciding check and quote its evidence line in the summary's verdict line. Then emit the JSON block from SKILL.md with every check in rubric order, the item set to the bundle id (eval) or the issue or PR URL (live), and the verdict. Nothing follows the block.
