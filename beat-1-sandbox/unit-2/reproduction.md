# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Nandini-G1
---

## Posted upstream

**Claim comment**

Claim comment link: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-5875989924
Claim comment text: Hi, I'm going to start by running the reproduction from the issue body against the current main branch to check whether indented resume text gives back an empty detected_sections list from _detect_sections() in ingestion/parsers/resume_parser.py. I'll also run the three failing tests in tests/unit/test_resume_parser.py so I can see how they fail before I change anything. I'll post a repro report here with my environment, the exact steps, and what I observe, whether or not it reproduces.

**Reproduction comment**
Repro comment link: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-5901256377
Repro report for #54: reproduced.

**Environment**
- macOS 26.5.2 (build 25F84)
- Python 3.14.7
- Commit: f89c06fc3ff292df2a04a39ac51319d32a76b779 (my fork of main)

**Steps**
1. Cloned my fork and created a virtual environment:
   `python3 -m venv .venv`
2. Installed the project with dev dependencies:
   `.venv/bin/pip install -e ".[dev]"`
   (I skipped the Docker/database steps from SETUP.md, since the
   parser and its unit tests don't use them.)
3. Saved the reproduction from the issue body as `repro54.py` and ran
   `.venv/bin/python repro54.py`
4. Ran the parser's tests:
   `.venv/bin/python -m pytest tests/unit/test_resume_parser.py -rx -q`

**Observed**
The issue's example prints an empty list:
```
[]
```
Expected: sections including Education and Skills.

The test run gives `5 passed, 5 xfailed`. All five xfailed tests are
marked with the reason "issue #54: resume section detection fails on
leading whitespace":
- test_parse_single_column_resume_text
- test_parse_resume_no_work_experience
- test_parse_markdown_resume
- test_detect_sections
- test_strip_markdown_syntax

The issue body lists three related tests; the repo marks two more (test_parse_markdown_resume, test_strip_markdown_syntax) as xfail for this issue.

**Outcome**
Reproduced: indented resume text gives back an empty detected_sections list, matching the issue. Next I'll look at how_detect_sections() anchors its patterns

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**
1. --limit 1 smoke run (pkg-01): 1/1. Partial; confirmed the harness and my files loaded.
2. Full run: 17/20 (below bar; category floor unmet, disclosure 0/1). Disagreed on pkg-05, pkg-16, pkg-20.
3. --only pkg-16,pkg-20,pkg-01,pkg-03: 3/4. Partial. After tightening environment-recorded and repo-conventions, pkg-16 and pkg-20 agreed, but canary pkg-03 flipped to reject on repo-conventions.
4. --only pkg-03,pkg-20: 2/2. Partial. After scoping repo-conventions to repos that explicitly require disclosure.
5. Full run with --save-run eval-run.txt: 19/20 (bar: PASS, all categories matched). This is the committed eval-run.txt.

**Package analysis**

pkg-16 (pandas-dev/pandas#66656). In my first full run my rubric graded it accept; the gold label is reject (wrong-target).

The error in the report matched the issue exactly: "ValueError: Length of new names must be 1, got 3". So behavior-matches-issue passed, and environment-recorded passed because the environment line gave concrete values: "pandas 1.5.3 (pip), Python 3.10.12, Ubuntu 22.04 (x86_64)". My first version of that check only asked whether the versions were concrete, not whether they were the right ones.

But the repo facts say the latest release is v3.0.5, and the bug template "asks reporters to confirm the bug exists on the latest version and on the main branch." The report ran a version two majors old and still said "The crash the issue describes is confirmed". Reproducing on 1.5.3 does not confirm the bug as reported on main. I tightened environment-recorded so the tested version must be the one the issue targets, or the report must flag the gap, and the final run rejects pkg-16, agreeing with gold.

**Check rationale**

"| repo-conventions | The repo-facts block's contribution policy, including any AI-use policy, read against the claim comment and the repro comment | Every policy the repo states for contributor comments is met. Only when the policy explicitly requires disclosing AI use must each comment contain a disclosure statement (the tool and extent, or that no AI was used); on those repos a comment with no disclosure statement fails. When a policy restricts AI use without requiring disclosure (for example, "comments must be written by humans"), the comment passes unless its text shows the rule was broken; never presume AI use. If the repo states no AI policy, this passes | required |"

My first version just said every stated policy must be met, and it passed pkg-20 (Ghostty), whose policy says "All AI usage in any form must be disclosed". The comments said nothing about AI, and the grader read silence as "no AI used, nothing to disclose." So I added that a comment with no disclosure statement fails. That fixed pkg-20 but flipped pkg-03 (ripgrep) to reject, because ripgrep's policy restricts AI ("comments to maintainers must be written by humans") without requiring disclosure, and my wording made the grader presume AI use. So the check now separates the two kinds of policy: silence fails only where disclosure is explicitly required, and the grader must never presume AI use anywhere else.

**Trade-offs**

Tightening environment-recorded to catch pkg-16 cost me pkg-07: it agreed in my first run, but the confirming run rejected it on environment-recorded and tested-on-current, while the gold label is accept. I accepted that loss because a report that confirms a bug on the wrong version misleads maintainers, which is worse than holding back one good report.

For repo-conventions, I used pkg-03 as a canary with --only when I tightened it, which is how I caught the flip at $0.20 instead of on a full run. When I then loosened it, I re-ran pkg-20 alongside pkg-03 as the disclosure canary, and it stayed reject. Also, pkg-05 moved from reject to accept between full runs with no change to steps-followable, so that call is borderline for the grader and could go either way on a rerun.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
