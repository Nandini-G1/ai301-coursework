# Rubric: is this a good first issue?

Every threshold below is measured against the bundle's stated capture date
in eval mode, and against today's date in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `repo-alive` | Repo facts: the `archived:` flag on the repo line, `last push to any branch`, and the dates in `last 5 default-branch commits`. | `archived: no`, AND the most recent default-branch commit date is within 180 days of the capture date. | required |
| `repo-in-use` | Repo facts: `latest release` (name and date), plus the dates in `last 5 default-branch commits`. | The latest release is dated within 24 months of the capture date. If the repo lists no release at all, pass instead when at least 3 of the last 5 default-branch commits fall within 90 days of the capture date. | required |
| `policy-allows-ai` | Repo facts: the `contribution policy` line (and any AI policy it quotes or summarizes). | No outright ban on AI-assisted or AI-generated contributions. A line stating conditions (disclose AI use, review and understand the output, test it, human review) passes. A line reading "no statement on AI" or equivalent silence passes. Fail only on a stated refusal to accept AI-generated code. | required |
| `unassigned` | Repo facts: `this issue: assignees:` and `linked PRs:` with each PR's state; plus the Comments section for any PR a commenter says they have opened. | `assignees: none`, AND no linked or thread-mentioned PR is in the `open` state. A `closed` unmerged PR does not fail this check. | required |
| `unclaimed` | The Comments section: comments offering to take the work ("I'll take this", "can I work on this", "working on this"), each with its author and date; and any maintainer reply to them. | No such claim comment dated within 180 days of the capture date. A claim older than 180 days with no follow-up work does not fail this check; neither does a claim whose author later withdrew it in the thread. | required |
| `bounded-scope` | The issue body, and the Comments section. | The body asks for one bounded change that one contributor could finish in one pull request. Fail on exactly three things: (a) the body calls itself a tracking, umbrella, epic, or meta issue, or its sub-items are links to other issues meant to be worked separately; (b) the thread shows the design still being argued with no maintainer having settled it; (c) a maintainer states the fix reaches core internals. Nothing else fails this check. In particular, a long body, a detailed implementation plan, a list of several files or sections to edit, a terse body, a missing reproduction, or a bare acceptance-criteria checklist all PASS: grade the size of the work asked for, not the length or polish of the writeup. | required |
| `is-a-contribution` | The issue title and body. | The issue asks for a change to the project (bug fix, feature, docs, test, refactor). Fail when it is a pure usage or support question asking how to make the software work for the author, with no change to the project requested. | required |
| `work-is-wanted` | The `opened by <user> (ASSOCIATION)` line, the issue's `labels:` line, the body (is it a bug report, a docs change, or a request for new functionality?), and the Comments section for any comment by an `OWNER`, `MEMBER`, or `COLLABORATOR`. | Passes automatically when the issue reports a bug or asks for a documentation change. For an issue requesting NEW functionality, pass only when at least one of these shows the project wants it: the opener is an `OWNER`, `MEMBER`, or `COLLABORATOR`; the issue carries a maintainer-applied label such as `good first issue`, `help wanted`, `accepted`, or an area or type label; or a maintainer has commented in the thread without rejecting it. Fail an unlabelled new-functionality request opened by a `NONE`/`CONTRIBUTOR` account or a bot with no maintainer response: nobody has agreed the project wants this yet, so the work may be refused on sight however well it is written. | required |
| `not-a-graveyard` | The issue's opened date against the capture date; its labels; and `linked PRs:` for closed, unmerged PRs. | Fails when BOTH the issue has been open more than 36 months AND at least one previously linked PR is closed unmerged. Either signal alone passes. | preferred |
| `maintainer-responsive` | Repo facts: `maintainer first-response sample`, the per-issue days-to-first-maintainer-comment list. | At least 2 of the 5 sampled issues received a maintainer first response within 30 days. | preferred |
| `newcomer-labelled` | The issue's `labels:` line, and the `opened by ... (ASSOCIATION)` line. | The issue carries a `good first issue`, `good-first-issue`, `beginner`, `help wanted`, or documentation label, OR it was opened by an `OWNER`, `MEMBER`, or `COLLABORATOR`. | preferred |
| `thread-is-warm` | The Comments section: the date of the most recent non-bot comment, or the issue's opened date when there are no comments. | The most recent human activity in the thread is within 12 months of the capture date. | preferred |

## Verdict rule

`accept` when every `required` check grades `pass`. Any single `required`
check grading `fail` or `unclear` produces `reject`; `unclear` on a
required check counts as `fail`, because a first issue whose safety I
cannot verify from the evidence in front of me is not a first issue I
should take.

`preferred` checks never change the verdict. They are reported with their
grades and used only to rank the issues this rubric accepts: among
accepted candidates, more passing preferred checks ranks higher.
