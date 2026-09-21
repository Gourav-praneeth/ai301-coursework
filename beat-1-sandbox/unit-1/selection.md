# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

**Verdict output**

```
Scope check: codepath/pathreview-ai301-fa26-s1 matches the scoped source in
scope.md. Candidate is in scope. Path Review house rule applies: other
students' claim signals in this repo don't block the issue.

Checks:

maintainer-alive: pass — most recent default-branch commit is 2026-09-16,
4 days before the capture date (2026-09-20), inside the 90-day window.

repo-in-use: pass — archived: false; last push 2026-09-16, 4 days ago,
inside the 180-day window.

bounded-scope: pass — single named defect (verify_password lets
UnknownHashError escape instead of returning False), two named files
(core/security.py, tests/unit/test_security.py), one test to un-skip
(xfail marker referencing manifest id H-05), estimated effort 1-2 hours.
No umbrella framing, no unsettled design debate.

unclaimed: pass — assignees: []; 0 open PRs against the upstream repo
(checked repo-wide: 0 open PRs total); 0 comments on the issue. Two
"cross-referenced" timeline entries are other students' own forks
(newairforces/ai301-coursework, foojanbabaeeian/ai301-coursework-Fozhan)
coincidentally mentioning the number 72 in their own unrelated commit
history, not PRs against this issue — and even if they were claim
signals, the Path Review house rule says classmates' claims don't block.

ai-contribution-policy: pass — no CONTRIBUTING.md, .github/CONTRIBUTING.md,
AI_POLICY.md, AI_USAGE_POLICY.md, or AGENTS.md found in the repo; no
stated policy, and silence passes.

newcomer-friendly-signal (preferred): pass — labeled "good first issue";
opened by Aburke225 (COLLABORATOR), i.e. maintainer-filed with a precise
fix location and effort estimate.

All required checks pass.
```

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
  "checks": [
    {"name": "maintainer-alive", "grade": "pass", "evidence": "last default-branch commit 2026-09-16, 4 days before capture (2026-09-20), inside the 90-day window"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16, inside the 180-day window"},
    {"name": "bounded-scope", "grade": "pass", "evidence": "single defect in core/security.py with named test to un-skip (xfail marker, manifest id H-05), 1-2 hour estimate, no umbrella framing"},
    {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; 0 open PRs repo-wide; 0 comments on the issue"},
    {"name": "ai-contribution-policy", "grade": "pass", "evidence": "no CONTRIBUTING.md or AI-policy file found in the repo; silence passes"},
    {"name": "newcomer-friendly-signal", "grade": "pass", "evidence": "labeled good first issue; opened by Aburke225 (COLLABORATOR)"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Smoke run, `--limit 6`: agreement 6/6 scored items.
2. First full run, 20 issues: agreement 18/20 scored items (bar: 18/20: PASS); categories: claimed 4/4, clear-accept 7/8, dead-repo 3/3, policy 1/1, scope 3/4. Missed issue-19 (clear-accept, graded reject — failed bounded-scope) and issue-15 (scope, graded accept).
3. Targeted re-run after revising the `bounded-scope` check, `--only issue-01,issue-04,issue-05,issue-06,issue-09,issue-10,issue-11,issue-14,issue-15,issue-16,issue-19,issue-20`: agreement 11/12 scored items. issue-19 flipped to a correct accept; no other verdict in that set changed; issue-15 still graded accept against a gold reject.
4. Final confirming full run, 20 issues, saved with `--save-run eval-run.txt`: agreement 19/20 scored items (bar: 18/20: PASS); categories: claimed 4/4, clear-accept 8/8, dead-repo 3/3, policy 1/1, scope 3/4. This is the run committed in `eval-run.txt`.

**Issue analysis**

issue-15 (`zulip/zulip#19589`, category `scope`). Gold label: `reject`, noted as "years of design debate and two abandoned PRs behind a friendly label." My rubric's verdict: `accept`.

The bundle is a request to separate the `command` and `text` fields for a Slack-compatible outgoing webhook. It has 97 comments (the bundle shows the first 40), spans 2021 to 2025, and carries two closed, unmerged linked PRs (`zulip/zulip#20840`, `zulip/zulip#23123`) — a sign of repeated abandoned attempts. My rubric's `bounded-scope` check reads it as a bug with a clear, singular technical description (route the bot-mention prefix into a separate field) and no maintainer statement that the fix touches core internals, so it graded the check `pass`. What it missed: the check's pass condition for scope debate depends on the grading model noticing that no maintainer ever settled on a final approach within the visible thread, and a technically well-specified request can still be a swamp when the actual implementation was attempted and abandoned more than once — clarity of the ask and settledness of the ask are different things, and my check conflates them. That is the gap the gold label is catching and mine is not.

**Check rationale**

From `rubric.md`, the `bounded-scope` check, quoted as currently written:

> Fail if the issue is a self-described umbrella/tracking/mega-issue (explicitly framed as a list of separate items meant to be split into their own issues/PRs), if the thread runs for years with repeated attempts and no maintainer ever settling on a final decision, if a maintainer states the fix touches core internals, if the issue is a pure usage/support question, or if the request has no settled concrete spec and leaves a product/design decision for the implementer to make. A numbered list is NOT itself a scope failure when it is one person's breakdown of causes, sub-steps, or optional follow-on suggestions for a single fix (e.g. a maintainer diagnosing "cause 1, cause 2" behind one bug) — that is normal bug triage, not an umbrella. A terse body, a bug report without repro steps, or a plain checklist is also not a scope failure as long as the piece of work is singular and bounded. Pass otherwise.

The numbered-list carve-out (the second sentence) is there because my first full run failed issue-19 (`zxcalc/zxlive#517`, category `clear-accept`, gold `accept`): a maintainer-diagnosed performance bug listing two causes plus three optional follow-on suggestions. The original wording treated any numbered breakdown as umbrella-shaped, which rejected a bounded bug just because the maintainer triaged it in list form.

**Trade-offs**

The carve-out fixed issue-19 without changing any other verdict — I confirmed this with a `--only` re-run across all 12 issues in the `clear-accept` and `scope` categories (run 3 above), and only issue-19 moved. What it gives up: it makes the check more permissive toward numbered lists in general, which is exactly the shape that could let a genuine umbrella slip through if a single person's numbered breakdown ever smuggled in several independent deliverables rather than causes/sub-steps of one fix — the check now has to trust that distinction instead of failing every numbered list on sight. I accept that as a case it could still miss.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Fit: my fit profile in `scope.md` says I'm most comfortable in Python and want a first issue with a clear bug and a test to point to, in a backend/service file, not infra or unfamiliar frontend code. Issue #72 is exactly that: one function (`verify_password`) in `core/security.py`, one test file, an estimated 1-2 hours — realistic for the time I have this unit.

2. What the verdict got right vs. what I weighed myself: the rubric's mechanical checks correctly read the repo as alive (commits 4 days old), the issue as unclaimed (no assignee, 0 comments), and the scope as bounded (one named defect, one test, an effort estimate). What I had to weigh outside the rubric: the issue's timeline showed two "cross-referenced" events, and the `unclaimed` check's evidence source doesn't distinguish a real linked PR from a coincidental mention. I checked manually — 0 open PRs exist against the upstream repo at all — before trusting the check's pass grade, and separately confirmed the Path Review house rule would have covered it anyway even if those had been genuine classmate claims.

3. Anticipated difficulty: low-to-moderate. The fix itself (catch `passlib`'s `UnknownHashError` in `verify_password` and return `False`, then remove the `xfail` marker on the covering test) is small and scoped to one function, but I haven't used `passlib` before, so I'll need to read how it identifies hash formats to be sure I'm failing closed in the right place rather than papering over a different bug.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
