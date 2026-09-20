# Unit 1 — Issue Selection

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/59

**Verdict output**

````
Good, `gh` is authenticated. Let me gather repo-level facts and per-issue data in parallel.

All three issues confirmed with no comments, no PRs, no claims — just labeling and a rename event each. All evidence gathered. Here's the grading.

**Repo-level facts** (apply to all three): not archived, most recent default-branch commit 2026-09-16 (4 days ago) by a human collaborator (Aburke225) → maintainer-active passes. No AI-restriction policy anywhere in `docs/CONTRIBUTING.md` or the PR template → ai-policy-allowed passes (silence). All three issues: opened by a COLLABORATOR, zero comments, zero assignees, zero linked/mentioned PRs, no `good first issue`/`easy`/`help wanted` label.

## Summary

**Accepted, ranked by fit** (Python/TS-React background, wants RAG + agent reps, limited evenings, avoid heavy infra):

1. **#59 — Faithfulness checker scores claims unsupported when wording differs** (`rag`, `tier-1`) — direct RAG-scoring fix with a concrete failing test (`pytest tests/unit/test_faithfulness_checker.py`) to drive the work, pure Python logic, no infra label.
2. **#16 — Failed tool calls never reach the review output** (`agent`, `tier-2`) — direct agent-orchestrator fix, ~4-6h estimate, matches the "get better at agent code" goal, pure backend logic.
3. **#32 — `DELETE /profiles/{id}` leaves embeddings in the vector store** (`api`, `devops`, `tier-2`) — solid bounded bug but spans three layers (route, service, vector store) and carries a `devops` label, which brushes against the stated preference to avoid infra work.

None carry a `good first issue`/`easy`/`help wanted` label, so the preferred check fails across the board — doesn't change any verdict, just flattens the ranking to fit alone.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/59",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "archived: no; commit 2f4e82f by human Aburke225 on 2026-09-16, 4 days before today 2026-09-20"},
      {"name": "unclaimed", "grade": "pass", "evidence": "no assignees, zero comments, zero linked/cross-referenced PRs"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "single bug fix in `_is_supported()`, opener is COLLABORATOR, bug fix so ownership condition exempt anyway, includes concrete repro test, opened 10 days ago with no PR history"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "no AI/contribution restriction found in docs/CONTRIBUTING.md or PR template; silence passes"},
      {"name": "labeled-friendly", "grade": "fail", "evidence": "labels are [bug, rag, tier-1], no good first issue/easy/help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/16",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "archived: no; commit 2f4e82f by human Aburke225 on 2026-09-16, 4 days before today 2026-09-20"},
      {"name": "unclaimed", "grade": "pass", "evidence": "no assignees, zero comments, zero linked/cross-referenced PRs"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "single bug fix wiring failed tool_results into review output, opener is COLLABORATOR, bug fix so ownership condition exempt anyway, opened 10 days ago with no PR history"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "no AI/contribution restriction found in docs/CONTRIBUTING.md or PR template; silence passes"},
      {"name": "labeled-friendly", "grade": "fail", "evidence": "labels are [bug, agent, tier-2], no good first issue/easy/help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/32",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "archived: no; commit 2f4e82f by human Aburke225 on 2026-09-16, 4 days before today 2026-09-20"},
      {"name": "unclaimed", "grade": "pass", "evidence": "no assignees, zero comments, zero linked/cross-referenced PRs"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "single bug fix (clear vector-store chunks on profile delete), opener is COLLABORATOR, bug fix so ownership condition exempt anyway, opened 10 days ago with no PR history"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "no AI/contribution restriction found in docs/CONTRIBUTING.md or PR template; silence passes"},
      {"name": "labeled-friendly", "grade": "fail", "evidence": "labels are [bug, api, devops, tier-2], no good first issue/easy/help wanted"}
    ],
    "verdict": "accept"
  }
]
```
````

---

## Eval iterations

**Run history**

Run 1, full run on all 20 scored issues: 19/20, PASS. Categories were claimed 4/4,
clear-accept 7/8, dead-repo 3/3, policy 1/1, scope 4/4. I only did one run, and that's
the run in eval-run.txt.

**Issue analysis**

issue-01 (conda/conda#16475). My rubric rejected it, gold says accept. The check that
failed was scope-bounded, specifically clause (1). The issue asks for a new docs page and
then lists updates to manage-pkgs.rst, pip-interoperability.rst, new-features.md, plus a
maybe-entry in troubleshooting.rst. My wording says "one piece of work, not a list", so
all those file names read as an umbrella to it. Gold sees it differently: it's one docs
page, and the other files are just pointers to it. So my check is counting files touched
when it should be counting deliverables, and one deliverable can touch a few files.

**Check rationale**

Here's the scope-bounded pass condition from my rubric.md as it stands now:

"All four hold: (1) it asks for one piece of work, not an umbrella, tracking,
"megaissue", or "add X across the codebase" list; (2) it is not a usage or support
question; (3) if it asks for new product functionality (bug fixes and documentation
changes are exempt), a maintainer (OWNER/MEMBER/COLLABORATOR) opened it, labeled it good
first issue / help wanted, or said in the thread they would accept it; (4) it is not open
more than 2 years with 2 or more closed, unmerged PRs."

I split it into four clauses because the scope issues in the set all fail for different
reasons, and one word like "bounded" doesn't tell them apart. Clause (1) is for umbrellas
and codebase-wide work. Clause (3) is there because a feature nobody with commit rights
has agreed to is really a product decision, not a task. Clause (4) treats a pile of dead
PRs as a sign the work is harder than the label says.

**Trade-offs**

Clause (1) is what costs me issue-01. A big but single docs task looks like a list to it,
so it gets rejected. That's the one clear-accept I miss and I'm fine with it, because the
same clause is what catches issue-05 (type annotations across the whole codebase),
issue-10 (a literal megaissue), and with clause (3), issue-20 (a feature wish with no
spec). Nothing else changed, and I know that because there was only one run. It hit 19/20
with every category matched the first time, so I never had to revise another check.

---

## Selection rationale

**Selection rationale**

1. Fit and time. #59 is a bug in the word-overlap logic in faithfulness_checker.py. It's
   Python, it's RAG code, which is what I want more practice with, and it's tier-1 /
   Starter difficulty. It already has a failing pytest case, so I know exactly when I'm
   done. That matters since I only have a few evenings this week.

2. What the verdict caught vs. what I added. The skill handled the stuff I'd otherwise
   check manually: repo is active (human commit four days before I ran it), no assignee,
   no comments, no linked PR, and no AI policy blocking how I work. What it couldn't do
   was pick for me, since all three candidates passed every required check. I went with
   #59 over #16 and #32 based on difficulty tier and how much code the fix touches. #32
   spans routes, a service, and the vector store and has a devops label, which is the
   kind of thing I said I'd rather avoid right now.

3. Claiming it. It's a classroom repo, so other people may claim the same issue, and the
   house rule says that's fine. The real risk is duplicate work, not getting blocked. So
   the thing I need to get right in Unit 2 is a claim comment that says which part of the
   fix I'm taking.
