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

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5989161222

Hi, I'd like to take this as my first contribution. As I read it, verify_password in core/security.py lets UnknownHashError escape for an unrecognized hash instead of returning False. Next I'll set up the repo locally, reproduce it on current main, and post my environment, commands, and output here before I touch any code. If it reproduces, I'll then look at un-skipping the H-05 test in tests/unit/test_security.py.

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

## Eval iterations

**Run history**

17/20, then a 5-package `--only` re-run (pkg-03, pkg-05, pkg-07, pkg-19, pkg-20) that agreed 5/5, then the confirming full run: 19/20. The last score, 19/20 (bar PASS, every category matched), is the agreement line in `eval-run.txt`.

**Package analysis**

pkg-07 (p5.js#7168). My first rubric rejected it on `policy-respected` ("Repro report comment contains no AI disclosure; claim's disclosure ... does not substitute for the repro comment's own required disclosure line"); gold said accept. p5.js's policy requires disclosure of AI assistance, and the claim comment already says "Per the AI usage policy: I used an AI assistant to help me organize this report". My check had demanded a disclosure in each comment separately, when the policy is satisfied by one disclosure anywhere in the package. After the revision it accepts, matching gold.

**Check rationale**

> | policy-respected | The repo-facts block's contribution/AI policy line, read against the claim comment and the repro report together | Fail only if the policy explicitly requires AI use to be disclosed and neither the claim comment nor the repro report discloses it (treat course packages as AI-assisted work); one disclosure line anywhere in the package satisfies it. A policy that only welcomes AI, asks for human understanding or responsibility, or asks that comments be in the author's own words does not require disclosure: pass if the comments read as specific first-person writing. Bug-report template items the report omits do not fail this check. | required |

It reads this way because the first version failed three accepts (pkg-03, pkg-05, pkg-07): it treated "comments must be human-written" (pkg-03) and a missing `conda info` template item (pkg-05) as policy failures, and required disclosure per comment (pkg-07). I narrowed it to the one thing that must be disclosed, an explicit disclosure requirement, which is what pkg-20 (ghostty) turns on.

**Trade-offs**

This loosening could flip pkg-20, the single disclosure package, so I re-ran it as a canary with `--only` alongside the three fixed packages; it stayed reject. What it now gives up: a package that omits a template-requested item (such as `conda info` output) is no longer held by this check, and `steps-followable` lets a precisely described minimal input stand in for the literal file. The final run still misses pkg-12, which `steps-followable` rejects while gold accepts; I accept that miss rather than loosen the check further and risk the unfollowable-comms packages.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
