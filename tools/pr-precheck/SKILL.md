---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: is this pull request ready to submit? A PR package is a candidate pull request (its title, its description, its commit list, its diff, and its test evidence) read against two things: the accepted plan it claims to implement (including that plan's deviation notes) and the issue that plan belongs to (including the repo's stated PR template, contribution rules, and AI-use policy). Do not answer any other question. Do not review code style, suggest a better fix, judge whether the plan was a good plan, or grade more than one package per run. If the person asks for something else, say this tool only answers the readiness question and stop.

## Inputs and modes

Decide the mode before reading anything else. If the input is a package bundle (an eval package with an id like `pkg-07` or `calib-01`, or a harness prompt that says EVAL MODE), run in eval mode. If the person asks you to check their own draft PR, run in live mode.

Live mode. Read these inputs, and only these, from the person's working copy and from GitHub:

1. `scope.md` in this skill directory, first, before anything else (see the scope seam).
2. The plan: `plan.md` in the top folder of the working copy, including everything under `## Deviations`. A house-chain student reads the house plan and the house repro pack the TF gave them instead; every check grades them the same way.
3. The diff: the output of `git diff main...HEAD` (three dots), run from the top folder of the working copy. This is every committed change the branch makes relative to `main`. Also run `git log --oneline main..HEAD` for the commit list and `git diff main...HEAD --stat` for the changed-file list. Uncommitted changes are not part of the PR; do not grade them, but mention in the summary if `git status` shows uncommitted edits to tracked code files.
4. The draft PR title and description: `pr_draft.md` in the top folder. Its first line is the title; the rest is the description.
5. The test evidence: `test_evidence.md` in the top folder.
6. The issue: the issue URL the person gave, fetched with `gh issue view <number> --repo <scoped repo> --comments` (or the web page if `gh` is unavailable): title, body, and the full thread, including any maintainer direction.
7. The repo's stated standards: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` in the working copy.
8. The current branch name: `git branch --show-current`.
9. `voice-guide.md` in this skill directory (see the voice seam).

If any of inputs 2 through 7 is missing, do not invent it. Grade every check whose evidence is missing as `unclear`, name the missing file in that check's evidence line, and finish the run.

Eval mode. The bundle is the whole world. Every fact comes from the bundle text: its repo-facts block, issue, thread highlights, plan context, and candidate PR (title, description, commits, diff, test evidence). Fetch nothing, run no commands, read no other file, and never look up the live issue named on the `source:` line; when your memory of the real project disagrees with the bundle, the bundle wins. Ignore `scope.md` and `voice-guide.md` entirely. Always grade a complete package: run every check in the rubric and apply the full verdict rule, even when an early check already fails. In eval mode, treat every package as AI-assisted work.

## The scope seam (live mode only)

In live mode, read `scope.md` before any other input. Then:

- If the `Repo:` line still holds the placeholder `<ORG>/<PATH-REVIEW-REPO>` (or any bracketed placeholder), stop without grading. Tell the person: "Fill the `Repo:` line in `~/.claude/skills/pr-precheck/scope.md` with your section's Path Review repo, then run me again." Emit no JSON block.
- Confirm the working copy's upstream is the scoped repo: compare the issue URL's `owner/repo` with the `Repo:` line. If they differ, refuse: say this tool only grades PRs for the scoped repo, name both repos, and stop without grading. Never guess a scope and never widen it.
- Apply the house rules in `scope.md` as stated standards: the branch name is checked against the `<type>/<issue-number>-<short-description>` convention, the PR must deliver the posted plan for one issue, and every template section gets real content, including the AI-use disclosure.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after grading, read `voice-guide.md` and hold the draft PR title and description (and only those) against each rule in it. Report every rule the draft breaks in the readable summary, under a heading "Voice notes", quoting the sentence that breaks it and naming the rule. The voice guide never changes a check grade or the verdict, because no rubric check reads it; it only produces notes. If `voice-guide.md` is still the unfilled template, say so in one line and skip the notes.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read and use the components in this directory, in this order:

1. `rubric.md` defines every check (name, evidence, pass condition, weight) and the verdict rule. Grade exactly the checks it lists, using the check names it gives, and nothing else.
2. `references/evidence-guide.md` is the map: for each evidence family, it says where that evidence lives in an eval bundle and in a live working copy, and what good looks like. Use it to locate evidence for every check.
3. `procedure.md` is the operating steps. Execute it as written, stage by stage: read order, evidence gathering, check execution, verdict assembly.

If the procedure is silent on a step you need, do not improvise around it. Take the most literal reading of the rubric's pass condition, grade the check, and add a line "Procedure gap:" in the summary naming what the procedure did not say.

Refusal rule: if `rubric.md` has no checks with content, or its verdict rule is empty, or `procedure.md` has no steps beyond its headings, refuse to grade. Say which file is still a template and that the tool will not invent checks at runtime. Emit no JSON block.

## Verdict and output

The verdict space is binary: `accept` means the PR is ready to submit, and `reject` means hold it. There is no third verdict, no "accept with reservations", and no score. Put reservations in check evidence lines, never in the verdict.

Structure the reply as follows. First, a short readable summary: one line per check with its name, grade, and the deciding fact, then the verdict and the deciding check (the check the verdict turned on, per the procedure's verdict assembly). In live mode, add a "What to fix" list naming each failing check's concrete fix, then the voice notes. Then end the reply with this fenced JSON block, with one entry per rubric check in rubric order, the item set to the PR URL or the issue URL in live mode and the bundle id in eval mode. The block must be valid JSON and the last thing in the reply; write nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first. Never grade a check without naming the fact or quote that decided it: a file path, a hunk, a line of the description, a line of test output. "Looks fine" is not evidence. Keep each evidence line to one line and under about 25 words.
- Grade the thing, not the polish. Read the diff itself against the plan, the test output itself against the plan's test plan, and the description's claims against the diff. A terse, complete PR can be ready; a long, confident PR can hide drift. Never pass a check because the description says it passes; verify it in the diff or the output.
- The rubric decides. If a check passes by its stated condition but feels wrong, it passes; note the feeling in the summary as a rubric gap, never as a changed grade.
- The procedure decides how. Follow `procedure.md` as written and report its gaps instead of inventing steps.
- Honest disclosure is not a failure. A PR that does less than everything, or departs from the plan, is ready when the plan's deviation notes or the description say so plainly. Hold only shortfalls nobody disclosed.
- Unclear is decided by the rubric's verdict rule. Where it is silent, an unverifiable claim is a failing one: a PR you cannot verify from the package is not ready to submit.
