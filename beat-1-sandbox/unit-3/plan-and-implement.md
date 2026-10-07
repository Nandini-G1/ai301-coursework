# Plan and implement

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

## Posted upstream

### GitHub username

Nandini-G1

### Plan comment

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-6030293988

Plan for #54, following my repro report above (indented text returns `[]`; the test file gives `5 passed, 5 xfailed`).

**Cause:** in `ingestion/parsers/resume_parser.py`, all four patterns in `_detect_sections()` require the section name right after `^` or `\n`, so any leading spaces stop the match. The header regex in `_strip_markdown()` (`^#+\s+`) has the same problem, which I expect is why `test_parse_markdown_resume` and `test_strip_markdown_syntax` are also marked for this issue.

**Change:** allow optional leading spaces or tabs (`[ \t]*`) in those five patterns, and remove the `xfail(strict=True)` marker from the five #54 tests, per CONTRIBUTING. Nothing else in the parser changes. The other markdown regexes, `SECTION_HEADERS`, and PDF extraction stay as they are.

**Test:** re-run my repro script (expect Education and Skills instead of `[]`), run an unindented copy as a control (same sections before and after), and re-run the test file (expect `10 passed`, no xfail or XPASS), plus `make lint`, `make typecheck`, and `make test-unit`.

**Open question:** non-breaking spaces from PDF extraction would still block detection. I'm leaving that out unless someone thinks it belongs here. I also still need to check the callers of `_detect_sections()`, and indented lines like `Skills: Python` will now count as section headers, the same as unindented ones do today.

I'll work on branch `fix/54-resume-section-whitespace` in my fork. I'm using Claude to help with this work, and I review and understand every change before I keep it.

## Your branch

### Branch

fix/54-resume-section-whitespace

## Evidence

Run from my fork's clone. Before is on `main` (commit f89c06f); after is on `fix/54-resume-section-whitespace`. `control54.py` is the same example as `repro54.py` with the indentation removed.

**Before**

```
$ .venv/bin/python repro54.py
[]

$ .venv/bin/python ~/Desktop/ai301/control54.py
['Education', 'Skills']

$ .venv/bin/python -m pytest tests/unit/test_resume_parser.py -rx -q
xx.x..xx..                                                               [100%]
=========================== short test summary info ============================
XFAIL tests/unit/test_resume_parser.py::TestResumeParser::test_parse_single_column_resume_text - issue #54: resume section detection fails on leading whitespace
XFAIL tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience - issue #54: resume section detection fails on leading whitespace
XFAIL tests/unit/test_resume_parser.py::TestResumeParser::test_parse_markdown_resume - issue #54: resume section detection fails on leading whitespace
XFAIL tests/unit/test_resume_parser.py::TestResumeParser::test_detect_sections - issue #54: resume section detection fails on leading whitespace
XFAIL tests/unit/test_resume_parser.py::TestResumeParser::test_strip_markdown_syntax - issue #54: resume section detection fails on leading whitespace
5 passed, 5 xfailed in 0.22s
```

**After**

```
$ .venv/bin/python repro54.py
['Education', 'Skills']

$ .venv/bin/python ~/Desktop/ai301/control54.py
['Skills', 'Education']

$ .venv/bin/python -m pytest tests/unit/test_resume_parser.py -rx -q
..........                                                               [100%]
10 passed in 0.15s
```

The indented repro went from `[]` to finding Education and Skills, the unindented control found the same two sections both times (the order differs because the parser returns `list(set(...))`), and the five #54 tests now pass with their xfail markers removed.

## Eval iterations

### Run history

1. Smoke test, partial (`--limit 2`, not a full run): 2/2 scored items.
2. Full run 1: agreement 19/20 scored items (bar: 18/20: PASS). This is the run saved in `eval-run.txt`.

I did one full run. It cleared the bar with every category matched (clear-accept 6/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, wrong-cause 4/4), so I didn't revise and re-run.

### Package analysis

**pkg-14** (clear-accept). My rubric decided **reject**; the gold label is **accept**. The harness note was "failed: executable, honest-unknowns".

The deciding check was `executable`, which is required. It passes only if "at least one specific file, function, or code site is named AND one approach is chosen." pkg-14's plan chooses an approach (drain the pending OSC color responses in the reattach handshake before pane input is wired), but for location it only gives "the client attach/reattach path in `zellij-server` (session connection handling)" and says "exact functions to be pinned in the PR after tracing the query issuance with debug logs." My rubric reads that as a code area, not a specific site, so the grader failed it. (`honest-unknowns` also failed, but it's preferred and can't change the verdict.)

I think the gold label is reasonable. The plan is well grounded: its 0.44.1 control and cache control both fit the diagnosis, the Windows variant is deferred with a reason, and its test is decisive (five reattach cycles with no rgb strings). The gold note calls it "arguable on the deferral, ready as scoped." A maintainer could start from "the reattach handshake in zellij-server's connection handling," so my check is stricter than the staff's reading here.

### Check rationale

| executable | The plan's files/functions named and its chosen approach | Pass if a stranger could start the change without asking the author anything: at least one specific file, function, or code site is named AND one approach is chosen. Fail if the location is "somewhere" or unknown, the approach is left open ("X or Y, whichever is easier", "not sure which layer"), or the plan is investigation rather than a change. | required |

It requires both halves, a named site and one chosen approach, because the unbuildable packages fail in different ways. pkg-10 has neither (profile-and-optimize, no files). pkg-17 hasn't picked a layer ("gocui? tcell? not sure"). pkg-18 names something but leaves the decision open ("upstream or vendored, whichever is easier"). A check that only asked for named files would let pkg-18 through, and one that only asked for an approach would let pkg-17 through. The fail examples quote that kind of wording so the grader can match it.

I rejected two other versions. One was a structure check, like "the plan has a Files section," because the rubric template warns that checks on the write-up's shape make graders disagree; pkg-18 could have a Files heading and still say "somewhere." The other was a looser "names the area of the code that will change," because "the input stack" in pkg-17 would count as an area.

### Trade-offs

This check gives up pkg-14. Requiring a specific file, function, or code site rejects plans that name a code area and defer the exact function to tracing, even when the rest of the plan is strong, and the gold label accepts pkg-14. That's the one disagreement in my run.

I accepted that miss instead of loosening the check. Loosening "specific file, function, or code site" to accept an area would risk flipping the unbuildable packages, whose locations are also vague ("the input stack" in pkg-17, "somewhere" in pkg-18). If I had loosened it, I'd have re-run pkg-14 with pkg-17 and pkg-18 as canaries using `--only`, to check that the unbuildable category still matched. With 19/20 and every category already matched, I kept the stricter version.
