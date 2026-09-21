# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | Repo facts: "last 5 default-branch commits" (dates) and "maintainer first-response sample" (days to first owner/member/collaborator reply) | Pass if at least one of the last 5 default-branch commits is dated within 90 days of the capture date, OR at least one entry in the maintainer first-response sample shows an owner/member/collaborator reply within 60 days. A commit merging a human's PR counts even if a bot authored the merge commit. | required |
| repo-in-use | Repo facts: "archived:" flag and "last push to any branch" | Fail immediately if archived is "yes". Otherwise pass if the last push to any branch is within 180 days of the capture date. A missing or old "latest release" does not fail this check by itself if commits are recent (active repos without frequent releases still count as in use). | required |
| bounded-scope | Issue title, body, and comment thread | Fail if the issue is a self-described umbrella/tracking/mega-issue (explicitly framed as a list of separate items meant to be split into their own issues/PRs), if the thread runs for years with repeated attempts and no maintainer ever settling on a final decision, if a maintainer states the fix touches core internals, if the issue is a pure usage/support question, or if the request has no settled concrete spec and leaves a product/design decision for the implementer to make. A numbered list is NOT itself a scope failure when it is one person's breakdown of causes, sub-steps, or optional follow-on suggestions for a single fix (e.g. a maintainer diagnosing "cause 1, cause 2" behind one bug) — that is normal bug triage, not an umbrella. A terse body, a bug report without repro steps, or a plain checklist is also not a scope failure as long as the piece of work is singular and bounded. Pass otherwise. | required |
| unclaimed | Repo facts: "this issue: assignees:" and "linked PRs:", plus the Comments section | Fail if an assignee is set, or if any linked PR (formally linked or just mentioned in the thread) addressing this specific issue is currently open, or if a "working on this / I'll take this" claim comment is unanswered and recent (within ~60 days) with no sign of abandonment. Pass if there is no assignee and any linked PRs for this issue are closed/merged-and-superseded or stale (no follow-up for months, or a maintainer's reply reads as inviting other takers rather than reserving the issue for the claimant). For a tracking/umbrella issue, PRs linked to individual sub-items do not by themselves count as a claim on the whole issue (bounded-scope already handles umbrellas). | required |
| ai-contribution-policy | Repo facts: "contribution policy" line (from CONTRIBUTING.md / AI policy files) | Fail only on an outright ban on AI-assisted or AI-generated contributions. Conditions (disclosure, requiring the contributor to understand and test the change, human review) are terms to follow, not a fail. No stated policy passes. | required |
| newcomer-friendly-signal | Issue labels, opener's author_association, and body (repro steps / acceptance criteria) | Pass if the issue carries a "good first issue"-style label, was filed or clearly scoped by a maintainer, or includes clear repro steps or acceptance criteria. This never changes accept/reject; it only ranks accepted issues. | preferred |

## Verdict rule

Accept only if every `required` check grades `pass`. If any required check grades `fail` or `unclear`, the verdict is `reject` — `unclear` is treated as `fail` because a first issue whose liveness, scope, claim status, or policy cannot be verified from the evidence is not a safe first issue to take. `preferred` checks never affect the verdict; report their grades and use them only to rank issues that are already accepted.
