# Unit 1 — Issue Selection

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/59

**Verdict output**

```
Repo facts (apply to all three): not archived; last commit 2026-09-16 by human Aburke225
(well within 90 days of today, 2026-09-20) -> maintainer-active passes for all. No stated
AI/contribution-AI policy in docs/CONTRIBUTING.md or PR template -> ai-policy-allowed
passes (silence passes) for all. None of the three issues have any assignee, comment, or
linked/mentioned PR -> unclaimed passes for all.

Issue: #59 - faithfulness checker word-overlap bug
maintainer-active: pass
unclaimed: pass
scope-bounded: pass (bounded bug fix, has repro test)
ai-policy-allowed: pass
labeled-friendly (pref): fail (labels: bug/rag/tier-1, "Starter difficulty" isn't
literally good-first-issue/easy/help-wanted)
Verdict: accept

Ranked by fit profile:
1. #59 - straight RAG-logic bug (faithfulness_checker.py), tier-1/"Starter difficulty,"
   has a failing pytest repro already written. Smallest, cleanest first bite.
2. #16 - agent-orchestration bug, tier-2/"Intermediate" with a 4-6h estimate, more
   plumbing/propagation than domain logic.
3. #32 - vector-store cleanup, carries a devops label alongside api, and the fix spans
   api/routes, profile_service, and vector_store.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/59",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "archived:false; latest commit 2026-09-16 by human Aburke225"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees:[], comments:[], no linked/mentioned PRs for #59"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "single bounded bug in _is_supported(); bug fix so maintainer-open exemption applies; repro via pytest given; opened 2026-09-10, no history of abandoned PRs"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "no AI/contribution-AI policy found in docs/CONTRIBUTING.md or PR template"},
      {"name": "labeled-friendly", "grade": "fail", "evidence": "labels are bug, rag, tier-1 (Starter difficulty) - no literal good first issue/easy/help wanted label"}
    ],
    "verdict": "accept"
  }
]
```

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
