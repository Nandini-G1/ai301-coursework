# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54

**Verdict output**

All three are in scope (`codepath/pathreview-ai301-fa26-s1`), and all three **accept** — every required check passes on each. Shared repo facts: not archived, last default-branch commit Sep 16 2026 (6 days ago), no releases but all 5 recent commits within 90 days, and `docs/CONTRIBUTING.md` says nothing about AI either way (silence passes).

**Ranked by fit**

1. **#57 — tech detector counts vendored/build files** — tightest match for your profile. The body carries a copy-pasteable 8-line Python repro with observed-vs-expected output, needs no services running, and names the two tests (`test_node_modules_excluded`, `test_build_directory_excluded`) that give you the fails-before/passes-after loop for free. The fix is a directory-exclusion filter on a pure function. Despite the JavaScript-flavored subject matter, every line you'd write is Python.
2. **#54 — section detection fails on leading whitespace** — also pure Python string-in/list-out with a stated repro and three named failing tests. Ranks second only because the regex anchoring in `_detect_sections()` spreads across three tests, so the change is slightly wider than #57's.
3. **#62 — health check references a nonexistent `settings.redis_host`** — a genuinely clean one-attribute mismatch, but reproducing it means standing up Redis and the FastAPI stack, and no failing tests are named. That's infra setup rather than the read-the-Python-and-fix-it work you said you're strong at.

Two notes on the preferred checks: `maintainer-responsive` **fails** identically on all three — I sampled five issues (#54, #57, #62, #72, #43) and every one has zero comments, so no maintainer first-response exists to measure. That's normal for a freshly seeded classroom repo and, being preferred, changes no verdict. The other three preferred checks pass on all three issues, which is why fit rather than check count decides the ranking.

Per the Path Review house rule, go ahead and claim #57 even if classmates have claimed it — credit attaches to the PR you open.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "archived: no; latest main commit 'chore: track five more manifest entries' Sep 16 2026, 6 days before today"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "No releases listed; all 5 recent main commits (Sep 16 x3, Aug 24 x2) fall within 90 days of Sep 22 2026"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no mention of AI-assisted or AI-generated contributions; silence passes"},
      {"name": "unassigned", "grade": "pass", "evidence": "Assignees: None; Development box shows no linked PRs"},
      {"name": "unclaimed", "grade": "pass", "evidence": "Issue thread has zero comments, so no claim comment exists"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One change: exclude node_modules/ and build/ in tech_detector.py; not a tracking issue, no design debate, no core-internals statement"},
      {"name": "is-a-contribution", "grade": "pass", "evidence": "Bug report requesting a fix: primary_language returns 'JavaScript' where 'Python' is expected"},
      {"name": "work-is-wanted", "grade": "pass", "evidence": "Issue reports a bug, which passes automatically; also carries maintainer labels 'bug', 'good first issue', 'agent', 'tier-1'"},
      {"name": "not-a-graveyard", "grade": "pass", "evidence": "Opened Sep 10 2026 (12 days), far under 36 months, and no closed unmerged linked PRs"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled issues #54, #57, #62, #72, #43 all have zero comments: 0 of 5 got a maintainer first response"},
      {"name": "newcomer-labelled", "grade": "pass", "evidence": "Labels include 'good first issue (Good for newcomers)'"},
      {"name": "thread-is-warm", "grade": "pass", "evidence": "No comments, so opened date Sep 10 2026 is the latest human activity, within 12 months"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "archived: no; latest main commit Sep 16 2026, 6 days before today"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "No releases listed; all 5 recent main commits (Sep 16 x3, Aug 24 x2) fall within 90 days of Sep 22 2026"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no mention of AI-assisted or AI-generated contributions; silence passes"},
      {"name": "unassigned", "grade": "pass", "evidence": "Assignees: None; Development box shows no linked PRs"},
      {"name": "unclaimed", "grade": "pass", "evidence": "Issue thread has zero comments, so no claim comment exists"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One change: fix line-start regex anchoring in _detect_sections() in resume_parser.py; not a tracking issue, no design debate"},
      {"name": "is-a-contribution", "grade": "pass", "evidence": "Bug report requesting a fix: indented resume text yields an empty detected_sections list"},
      {"name": "work-is-wanted", "grade": "pass", "evidence": "Issue reports a bug, which passes automatically; also carries maintainer labels 'bug', 'good first issue', 'ingestion', 'tier-1'"},
      {"name": "not-a-graveyard", "grade": "pass", "evidence": "Opened Sep 10 2026 (12 days), far under 36 months, and no closed unmerged linked PRs"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled issues #54, #57, #62, #72, #43 all have zero comments: 0 of 5 got a maintainer first response"},
      {"name": "newcomer-labelled", "grade": "pass", "evidence": "Labels include 'good first issue (Good for newcomers)'"},
      {"name": "thread-is-warm", "grade": "pass", "evidence": "No comments, so opened date Sep 10 2026 is the latest human activity, within 12 months"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "archived: no; latest main commit Sep 16 2026, 6 days before today"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "No releases listed; all 5 recent main commits (Sep 16 x3, Aug 24 x2) fall within 90 days of Sep 22 2026"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no mention of AI-assisted or AI-generated contributions; silence passes"},
      {"name": "unassigned", "grade": "pass", "evidence": "Assignees: None; Development box shows no linked PRs"},
      {"name": "unclaimed", "grade": "pass", "evidence": "Issue thread has zero comments, so no claim comment exists"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One change: reconcile the Redis probe in api/routes/health.py with the redis_url field on Settings; no design debate in thread"},
      {"name": "is-a-contribution", "grade": "pass", "evidence": "Bug report requesting a fix: GET /health returns 503 reporting redis unhealthy due to an AttributeError"},
      {"name": "work-is-wanted", "grade": "pass", "evidence": "Issue reports a bug, which passes automatically; opener Aburke225 also carries a Contributor badge and the issue has labels 'api', 'bug', 'good first issue', 'tier-1'"},
      {"name": "not-a-graveyard", "grade": "pass", "evidence": "Opened Sep 10 2026 (12 days), far under 36 months, and no closed unmerged linked PRs"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled issues #54, #57, #62, #72, #43 all have zero comments: 0 of 5 got a maintainer first response"},
      {"name": "newcomer-labelled", "grade": "pass", "evidence": "Labels include 'good first issue (Good for newcomers)'"},
      {"name": "thread-is-warm", "grade": "pass", "evidence": "No comments, so opened date Sep 10 2026 is the latest human activity, within 12 months"}
    ],
    "verdict": "accept"
  }
]
```

**Note on this run's evidence for issue-62.** This run reports issue-62's comment thread as empty and grades `unclaimed` a pass. Two earlier live runs of the same rubric on the same day found two comments there by `ZJShown`, dated 2026-09-21: "I'm a TF from CodePath's AI 301 course. I'd like to take on this issue as part of the TF weekly prep task", followed two minutes later by a full local reproduction ending "will follow up with a PR proposal." Those comments live only in the page's embedded JSON payload and do not appear when the page is fetched as rendered markdown, which is the path this run fell back to after exhausting its unauthenticated GitHub API budget. This run also reports `#72` and `#43` as having zero comments, which is likewise wrong. The rubric was not at fault either time — the verdict flipped because the evidence handed to the check was incomplete. Issue-54, the issue selected here, has a genuinely empty thread and graded `accept` in all three runs.

---

## Eval iterations

**Run history**

Five runs, in order. Three were partial (`--limit` / `--only`) and are marked as
such; the two full runs are the ones the bar reads.

1. `--limit 3` smoke run — **2/3**. Partial. Ran only to confirm the harness and
   the CLI worked before spending a full run.
2. `--only issue-01,issue-02,issue-03` — **3/3**. Partial. Re-graded the same three
   after rewriting `bounded-scope`.
3. Full run — **18/20** (bar: PASS; categories `claimed 4/4  clear-accept 7/8
   dead-repo 3/3  policy 1/1  scope 3/4`). Disagreed on `issue-09` and `issue-20`.
4. `--only issue-09,issue-20,issue-01,issue-04,issue-06,issue-11,issue-14,issue-16,issue-19`
   — **9/9**. Partial. The two disagreements plus all eight accept-labelled issues,
   run together so that a fix for the two could not quietly break the eight.
5. Full run with `--save-run eval-run.txt` — **20/20** (bar: PASS; categories
   `claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4`).

The last score, 20/20, is the agreement line in the committed `eval-run.txt`.

**Issue analysis**

`issue-20` (excalidraw/excalidraw#11811, "Add company logo shape to the toolbar").
In run 3 **my rubric graded it `accept`; the gold label is `reject`.** It was the
one `scope` miss that run (`scope 3/4`).

My rubric accepted it because every required check I had written passed on the
evidence, and each pass was correct on its own terms. The repo is plainly alive —
`archived: no`, five default-branch commits dated `2026-08-04`, one day before the
capture date, and release `v0.18.1 (2026-04-21)` well inside my 24-month window.
The contribution policy line reads "no statement on AI or contribution tooling",
which my `policy-allows-ai` check treats as silence and passes deliberately. The
issue line reads `assignees: none; linked PRs: none` and the thread has zero
comments, so `unassigned` and `unclaimed` passed with nothing to weigh. And the
body is genuinely well written: it names a single surface ("logo tool in the shapes
toolbar → place/resize/move like other elements → correct export"), points at
`packages/excalidraw`, and even fences off future work ("Out of scope for v1:
custom logo upload / branding settings"). My `bounded-scope` check asks whether one
contributor could finish the work in one pull request, and by that reading it
passes.

What every one of those checks was blind to is the line `opened by cursor[bot]
(NONE) on 2026-08-02` together with `labels: none` and an empty comment thread. The
request is for *new functionality* in a 128,988-star project, filed by a bot with
no association to the repo, and in the three days to capture no maintainer had
labelled it, triaged it, or replied. Nobody had agreed the project wants a
hardcoded company-logo tool at all — and "Logo asset TBD" means the feature is not
even fully specified. A newcomer could build exactly what the issue describes and
have it closed as out-of-scope without a line being read. My rubric was asking
"is this work well-scoped and free?" and had no check asking "does anyone want this
work?", which is why a clean-looking issue sailed through. Adding `work-is-wanted`
closed that gap and the final run agrees with the gold label.

**Check rationale**

The check, quoted as it currently stands in the `rubric.md` uploaded to
`tools/issue-select/`:

> | `work-is-wanted` | The `opened by <user> (ASSOCIATION)` line, the issue's `labels:` line, the body (is it a bug report, a docs change, or a request for new functionality?), and the Comments section for any comment by an `OWNER`, `MEMBER`, or `COLLABORATOR`. | Passes automatically when the issue reports a bug or asks for a documentation change. For an issue requesting NEW functionality, pass only when at least one of these shows the project wants it: the opener is an `OWNER`, `MEMBER`, or `COLLABORATOR`; the issue carries a maintainer-applied label such as `good first issue`, `help wanted`, `accepted`, or an area or type label; or a maintainer has commented in the thread without rejecting it. Fail an unlabelled new-functionality request opened by a `NONE`/`CONTRIBUTOR` account or a bot with no maintainer response: nobody has agreed the project wants this yet, so the work may be refused on sight however well it is written. | required |

The form follows from what went wrong on `issue-20`. The naive version of this
check — "a maintainer must have endorsed the issue" — would have been far too
broad: it would have failed `issue-01`, a conda documentation issue opened by a
`CONTRIBUTOR` with no maintainer comment in the thread at all, which the gold label
accepts. So the check is deliberately narrowed twice over. First by *kind of work*:
bug reports and documentation changes pass automatically, because a bug is a defect
the project has already implicitly agreed it does not want, and a docs fix does not
change behaviour, so neither needs anyone's prior blessing. Only requests for new
functionality — where a maintainer can reasonably say "we don't want this" — are
gated. Second by *how weak the required signal is*: three independent ways to pass,
any one of which suffices, and the weakest of them is merely "an area or type
label", i.e. evidence that a human maintainer touched the issue at all. It fails
only on the full conjunction: new functionality, AND an opener with no standing in
the repo, AND no labels, AND no maintainer in the thread. That is precisely the
`issue-20` shape and very little else.

It is weighted `required` rather than `preferred` because the cost it prevents is
not a ranking cost. An issue that fails it can be completed perfectly and still be
closed unmerged, which is the specific outcome Unit 1 exists to avoid.

**Trade-offs**

What `work-is-wanted` gives up is the untriaged-but-legitimate feature request: a
small project, an outside contributor files a genuinely good enhancement, and the
lone maintainer simply has not got to it yet. There are no labels and no reply
because the repo is quiet, not because the idea is unwanted. My rubric rejects that
issue, and in a small repo that is a real loss — the four independent escape
hatches (owner/member/collaborator opener, any maintainer label, any maintainer
comment, or being a bug or docs issue) narrow the blast radius but do not eliminate
it. I accepted that loss knowingly: the failure it prevents is wasted work on a
feature that gets refused, which costs a newcomer far more than skipping one
viable issue costs them, and there are always other candidates.

The second cost is the coupling I had to watch for. `work-is-wanted` reads the same
three fields — opener association, labels, thread — that `newcomer-labelled` and
`bounded-scope` read, so tightening it risked knocking out accepts that were
already passing. That is what run 4 was for: rather than re-grading only the two
issues I disagreed on, I ran `--only` over those two **plus all eight
accept-labelled issues**, so a fix aimed at `issue-20` could not silently cost me a
clear-accept. It came back 9/9, and the confirming full run moved `clear-accept`
from 7/8 to 8/8 and `scope` from 3/4 to 4/4 with nothing else changing — so I know
the check cost me nothing elsewhere in this set, and the one category that moved is
the one it was written for.

The same run confirmed the other half of that edit. Demoting `not-a-graveyard` from
`required` to `preferred` was what flipped `issue-09` (conda/conda#7617 — open
since 2018, with linked PR `conda/conda#11627 (closed)`) from `reject` to the gold
`accept`. Age plus one abandoned attempt turns out to be a reason to *rank* an
issue lower, not a reason to refuse it: the issue is still `good first issue`,
opened by a `MEMBER`, on a repo committing daily. It still grades `fail` on that
issue in the final run — it just no longer sinks it.

---

**Selection rationale**

**1. Fit to my interests and the time available.** I took issue-54 because the work
is plain Python on a pure function: `_detect_sections()` in
`ingestion/parsers/resume_parser.py` anchors its patterns at the start of a line, so
text extracted from a PDF with leading indentation matches nothing and
`detected_sections` comes back empty. The issue body hands me a seven-line
reproduction I can paste into a REPL, and it names three already-failing tests in
`tests/unit/test_resume_parser.py`. That means the fails-before/passes-after loop is
set up for me rather than something I have to build, which is the part of the
contribution workflow I most want practice at. Nothing in it touches JavaScript,
CSS, or build configuration, which is what I wanted to avoid for a first
contribution. It is also small enough to finish in the time I have.

**2. What the verdict identified correctly, and what I weighed that the rubric could
not.** The rubric was right about everything it can see: no assignee, no linked PR,
an empty comment thread, a `good first issue` and `tier-1` label from a maintainer,
and a repo that is plainly alive with commits six days before I ran it. It was also
right in a way I did not expect on a different issue — on issue-62 it found a claim
comment from a course TF posted the day before and rejected it, correctly
distinguishing course staff from a classmate, since the Path Review house rule only
exempts classmates. I would have taken issue-62 on the strength of its labels.

What the rubric could not weigh is which accepted issue teaches me more. My skill
ranked issue-57 first and issue-54 second, and I picked issue-54 anyway, which the
homework allows — the instruction is to choose the best fit among the issues it
accepts, not to take the top-ranked one. My reason is that issue-57's fix is
essentially "add two directory names to an exclusion list," where the title states
the answer, while issue-54 is a regex that looks correct and silently matches
nothing. Chasing a wrong answer that does not raise an exception is harder and more
useful to learn than chasing an obvious omission, and understanding why `^` fails
against indented text is a bug class I will meet again. Fit, in my rubric, only
orders accepted issues — so this was a judgment the tool handed back to me by
design.

**3. Anticipated difficulty in claiming it.** Low on paper: zero comments, no
assignee, no linked PR at the time I ran the skill, so nobody is on it yet. The real
difficulty is that no one will confirm the claim. My `maintainer-responsive` check
failed repo-wide — across every issue sampled, no Owner, Member, or Collaborator has
replied anywhere in that repository. So I should expect to post the claim comment
and start work without acknowledgement, rather than waiting for a green light that
is not coming. The second risk is speed: a TF claimed issue-62 the day before I
looked, so these issues do move. And because the house rule says a shared issue
blocks nobody, a classmate may well claim issue-54 after me — which costs me
nothing, since credit attaches to the pull request I open.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
