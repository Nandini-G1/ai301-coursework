# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Before you finish**, replace every `[bracketed prompt]` with your own words, then delete
the unused `[Tool name]` entry stub, its copy-me sentence, and the prompt sentences under
each header. A leftover bracketed prompt reads as unfilled.

**Student:** [Student name]

## Featured Tools

Three or four tools, presented in depth. Open with a few sentences
on why you chose these.

Full credit asks the featured set to show real change: **at least two** of your featured
entries should show a tool that visibly moved through use. An honest entry for a tool that
barely changed — saying so, dating what did happen, and giving the reason — earns the solid
middle tier and never fails you.

Each tool's honest limit is not written here. It goes in the tool-limits list at the
bottom of this page, one line per featured tool, so that the limits sit together and can be
read as a set.

[Why these tools, in your own words.]

Copy the entry shape below once per featured tool and fill it there.

**Issue-scout**

**What it is, and the judgment hole I wrote:** 

Issue-scout is a tool that searches GitHub for potential open-source issues that match my skills and experience. I wrote the selection rubric in tools/issue-select/rubric.md and later developed its search strategy using two gh search issues queries based on my fit profile (Python, good first issues, bugs, and tests), along with six ranking rules. My judgment was deciding what makes an issue genuinely worth pursuing rather than simply finding an issue labeled "good first issue." The rubric evaluates factors such as whether the repository is active, whether the issue is actually available, and whether its scope is realistic.

**How it evolved, dated:** 

September 22, 2026: After the Unit 1 evaluation scored 18/20, I found that issue-20 was incorrectly accepted even though it was opened by a bot and had no labels. I added work-is-wanted as a required check and changed not-a-graveyard from required to preferred. This improved the full evaluation score to 20/20.

October 28, 2026: During its first real scan of 198 issues, I noticed that all five accepted issues came from repositories that were only weeks old or unrelated to my interests. I added a rule rejecting repositories less than 90 days old and a one-result-per-repository ranking rule.

October 28, 2026: I discovered that the unassigned check only looked at open pull requests. This meant it could accept an issue that had already been fixed through a merged PR. I documented a patch but did not implement it, so I still manually inspect the Development sidebar.

By November 2, 2026: I replaced bounded-scope with scope-feasible and added a difficulty note to help distinguish manageable issues from issues that are technically possible but too large.

**Evidence:** 

Unit 1 evaluation: 18/20 → 20/20 after rubric changes.

The --only evaluation of nine items scored 9/9.

During the first real scan, the tool correctly rejected Red-DiscordBot#6794 because four pull requests were already open.

It also caught PathReview issue-62 because a maintainer's claim comment indicated that the issue was already being addressed. My original note was: "I would have taken issue-62 on the strength of its labels."

MFC#1506 was accepted, with three of four preferred checks passing. Its difficulty note initially described the issue as "straightforward but large."


**repro-check**

**What it is, and the judgment hole I wrote:** 

Repro-check evaluates whether a reported open-source issue is reproducible and whether the reproduction report follows the repository's conventions. I wrote the rubric, including checks such as environment-recorded and repo-conventions. My judgment was determining whether a reproduction actually demonstrated the reported problem, whether the tested environment was relevant, and whether the report followed the project's contribution policies.

**How it evolved, dated:** 

September 29, 2026: The Unit 2 evaluation initially scored 17/20, below the passing threshold. One major disagreement involved pkg-16, where the report used pandas 1.5.3 even though the issue targeted version 3.0.5. I changed environment-recorded so that the tested version must match the version targeted by the issue, or the report must explicitly identify the gap.

September 29, 2026: Another problem involved the interpretation of repository AI policies. My first revision to repo-conventions incorrectly affected the pkg-03 canary. I revised the wording to distinguish policies that explicitly require AI disclosure from policies that restrict AI use.

November 2, 2026: During real use on MFC#1506, repro-check evaluated my claim and reproduction report as acceptable. It caught that grep -c counts lines rather than individual uses, which led me to reword my counts as "lines containing."


**Evidence:** 

The revised policy wording stated:

Only when the policy explicitly requires disclosing AI use must each comment contain a disclosure statement … never presume AI use.

The evaluation improved from 17/20 to 19/20 PASS, with all categories matching the expected results.

During the MFC contribution, the tool also caught an inaccurate description of my grep results. However, it incorrectly described my claim as "after the fact" and suggested that the reproduction report was ready to post as a comment, even though the course instructions said not to post it.

**plan-check**

**What it is, and the judgment hole I wrote:**

Plan-check evaluates an implementation plan before I begin changing code. I wrote its rubric, including the executable check, which requires identifying a specific code site and choosing an implementation approach. My judgment was deciding whether a plan was sufficiently specific to be followed, whether the proposed changes were realistic, and whether its testing instructions actually verified the intended changes.

**How it evolved, dated:**

October 6, 2026: I uploaded the plan-check skill after developing its rubric.

October 6–7, 2026: The Unit 3 evaluation scored 19/20 on its first full run. The only disagreement involved pkg-14, which named a general code area instead of a specific implementation site. I decided to keep the requirement strict rather than weaken the rubric.

November 2, 2026: During my MFC#1506 contribution, plan-check evaluated my implementation plan and caught several problems. I had used a branch name that did not follow MFC's naming convention, referenced my private manifest instead of the actual ./mfc.sh lint command, and included an unsupported claim about "same 5 of 7." It also identified ambiguity in the phrase "one combined issue."

**Evidence:**

The tool caught the following issues during the MFC contribution:

Changed the branch name to feature/1506-snake-case.

Replaced the private manifest reference with ./mfc.sh lint.

Identified an unsupported testing claim.

Clarified the difference between one combined issue and one pull request.

The original evaluation scored 19/20, and I did not revise the rubric because I believed the single disagreement was justified.

## Inventory

One line each for the rest of the toolkit: what it is and where it
stands (one bullet per tool; a compact sentence or two is fine).

Voice guide + voice guard: Combined three separate voice guides into one consistent guide, added upstream rules for claims, questions, and pings, and created a guard to prevent low-quality or repetitive communication. The guard blocked a question that simply repeated the issue, and the question was submitted after I added what I had actually checked.

CLAUDE.local.md: A repository-specific instruction file for MFC that records the 11 in-scope names and the ./mfc.sh test --list command. It was updated after a pre-commit hook blocked my first commit on November 2, 2026.

PR-monitor playbook: A workflow created on November 3, 2026, that uses a 14-day first-response threshold, a one-nudge rule, and the principle that bot reviews do not count as maintainer feedback. It drafted a follow-up but held the nudge until November 17.

## The Arc

The story of the toolkit in order: friction, change, result, dated.
Your weekly Toolkit entries are the source; read your own record and
tell it oldest first.

Write one block per beat, in the shape below, oldest first. Keep all four labels on every
beat, each on its own line. The `Result:` line is what the beat was for: it says what
happened *after* the change, which is not the same sentence as the change itself. If a beat
never reached a result, write `Result: none` — an honest beat that did not land still counts
fully as a beat.

Full credit asks for **at least two** beats whose `Result:` line names something that
actually happened afterwards. A beat about something that did not work counts fully as a
beat, and when the work happened never moves this score.

**Beat 1**
Date:  September 16, 2026
Friction: I needed a structured environment for my AI301 coursework and a way to organize my tools and evaluations instead of relying on disconnected prompts.
Change: Created the Nandini-G1/ai301-coursework repository from the course template.
Result: Established the repository that I used to develop, evaluate, and track my toolkit throughout the semester.

**Beat 2**
Date: September 22, 2026
Friction: My initial issue-selection rubric accepted an issue opened by a bot even though it was not genuinely available to work on. The Unit 1 evaluation scored 18/20.
Change: Added work-is-wanted as a required check and changed not-a-graveyard from required to preferred.
Result: The full evaluation improved to 20/20, and the nine-item targeted evaluation scored 9/9.

**Beat 3**

Date: September 29, 2026
Friction: Repro-check scored 17/20 because it accepted a reproduction using a version unrelated to the issue's target and incorrectly interpreted repository AI policies.
Change: Required environment versions to match the issue's target or disclose the difference. Reworded the repository policy check to distinguish disclosure requirements from restrictions on AI use.
Result: The evaluation improved to 19/20 PASS, with all categories matching the expected results.

**Beat 4**

Date: October 28 – November 2, 2026
Friction: My first real issue-scout scan of 198 GitHub issues revealed that the tool was accepting issues from very new repositories and issues unrelated to my interests. I also found that its unassigned check could miss issues that had already been resolved through merged pull requests.
Change: Added a 90-day repository-age requirement and a one-result-per-repository ranking rule. I also documented a patch for the incomplete unassigned check and replaced bounded-scope with scope-feasible. During this period, I combined my three voice guides, installed a voice guard, and created repository-specific instructions in CLAUDE.local.md.
Result: Issue-scout correctly rejected Red-DiscordBot#6794 because four pull requests were already open. The voice guard also blocked a repetitive question until I added what I had actually checked.

**Beat 5**

Date: November 2–17, 2026
Friction: While contributing to MFC#1506, I found problems with my implementation plan and reproduction report. Additionally, MFC's checks failed on unchanged master on my Mac, making it difficult to distinguish existing environment failures from problems caused by my changes. I also needed a consistent way to monitor my pull request.
Change: Used repro-check and plan-check to catch inaccurate grep counts, incorrect branch naming, and unsupported testing claims. Updated the ship manifest to document and exclude environment-dependent failures. I also created a PR-monitor playbook with a 14-day response threshold and a one-nudge rule.
Result: The ship-gate passed on its first run, and I opened PR #2131 on November 3, 2026. The PR-monitor drafted a follow-up and held the nudge until November 17. A maintainer eventually told me to stop marking the PR ready to merge, revealing another limitation that I need to address in the playbook.

## Limitations and What's Next

My toolkit has become much more structured, but it still relies on incomplete information in several areas. Most importantly, the real MFC test suite was never run because it requires CMake and a Fortran build environment that I did not have configured. My next step is to set up Linux with CMake so that I can run the actual test suite rather than relying primarily on the available prechecks.

I also need to improve how my tools interpret GitHub activity. Issue-scout still does not check merged pull requests when determining whether an issue is unassigned, which means it can recommend issues that have already been fixed. I plan to implement this check and rerun the scan to verify that it rejects MFC#1509.

Another limitation is that the PR-monitor playbook does not account for draft versus ready states. After receiving maintainer feedback about marking my PR ready to merge, I realized that the workflow needs a rule to never change a PR's draft or ready state automatically and to read the repository's contributing guide first.

Finally, Ruff's naming rules are not configured correctly, so new camelCase names can still be introduced even when the repository expects a different naming convention. I plan to correct that configuration.

**Tool limits.** One line per featured tool, in the same order as the entries above, naming
where that tool still stops or what it still gets wrong. A small honest limit is full credit;
"none really" is not a limit. If a tool genuinely has none you can name, write `none` after
its label rather than deleting the line.

issue-scout: Its unassigned check is still incomplete because it only checks open PRs and does not account for merged PRs that may have already resolved an issue. The tests query also never reached the top five results, and its maintainer-responsive check failed for MFC#1506.
repro-check: It can incorrectly interpret contribution instructions and make recommendations that conflict with course requirements. During MFC#1506, it suggested that a reproduction report was ready to post even though the course instructed me not to post it.
plan-check: Its procedure assumes evaluation-mode inputs and does not include a specific workflow for refactoring code when there is no existing bug to fix.

