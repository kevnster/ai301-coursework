# Rubric: is this a good first issue?

All "within N days" thresholds are measured against the bundle's capture
date in eval mode, and against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-active | Repo facts: the `archived:` flag, the last 5 default-branch commits (date and author), and the maintainer first-response sample | `archived: no` AND at least one default-branch commit within 90 days that is authored by a human or is a bot merging a human's pull request. Commits authored by a `[bot]` account, or a bot merging a bot's PR (e.g. dependabot), do not count. | required |
| unclaimed | Repo facts "this issue:" line (assignees, linked PRs with state), plus every PR number or claim comment in the Comments section | No assignee, AND no linked or thread-mentioned PR that is open or of unknown state, AND no claim comment ("I'll take this", "working on this", `/assign`, `@zulipbot claim`) within 60 days. Closed or merged PRs do not block. A claim older than 60 days with no PR does not block. | required |
| scope-bounded | Issue title, body, labels, opener's author_association, and the Comments section | All four hold: (1) it asks for one piece of work, not an umbrella, tracking, "megaissue", or "add X across the codebase" list; (2) it is not a usage or support question; (3) if it asks for new product functionality (bug fixes and documentation changes are exempt), a maintainer (OWNER/MEMBER/COLLABORATOR) opened it, labeled it good first issue / help wanted, or said in the thread they would accept it; (4) it is not open more than 2 years with 2 or more closed, unmerged PRs. | required |
| ai-policy-allowed | Repo facts "contribution policy" line | The policy does not ban AI-generated or AI-assisted contributions outright. Conditions (disclose AI use, understand and test every change, human review) pass. No stated policy passes. | required |
| labeled-friendly | Issue labels | Has a `good first issue`, `easy`, or `help wanted` label. | preferred |

## Verdict rule

Accept only if every required check passes. Any required check graded
fail or unclear rejects the issue. The preferred check never changes the
verdict; it only ranks accepted issues.
