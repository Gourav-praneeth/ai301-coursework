# Evidence guide: where proof lives in a reproduction package

In an eval bundle everything is in one markdown file: `## Repo facts`, `## Issue`, `## Thread highlights`, `## Candidate claim comment`, `## Candidate repro report`. Use only that text. In live mode the issue side is on GitHub (issue body, comments, labels, CONTRIBUTING.md, bug-report template, any AI policy file) and the candidate side is the student's draft files; the drafts are the whole package, not other files in the working directory.

## Environment

- Where it lives: bundle: the first lines of the repro report ("Environment: ..."), or inline in the steps. Issue target: the issue body and thread (versions, OS, driver, build profile, shell the reporter names; maintainer notes about what matters). Live: the draft's environment section; issue side from the issue thread.
- What good looks like: OS, tool version, and runtime are named, plus any variable the issue says changes the behavior. If the version differs from the one the issue was reported or confirmed on, the report says so. A missing record, or a record that leaves out the variable the issue singles out, is not good.

## Steps

- Where it lives: the commands or numbered steps in the repro report, including any control run.
- What good looks like: someone starting from a clean machine could type the commands and reach the trigger. Inputs are shown or shared, the issue's own trigger syntax is used, and nothing depends on a private repo or unshared config. For a cannot-reproduce, the exact attempt is still listed.

## Behavior shown

- Where it lives: output excerpts, logs, error text, exit codes, screenshots in the repro report; compared with the symptom quoted in the issue body ("Current result", error message, crash, exit code) and in thread highlights.
- What good looks like: the artifact reproduces the issue's specific symptom, not just that the tool runs. Check the details: same error type or message, same failure mode (crash vs. graceful error, exit code), same input or syntax as the issue, same version or an acknowledged difference. A control run showing the contrast is a strong sign. An adjacent symptom (a different error, a modified input, garbled output with the process still alive) is a different behavior.

## Honesty

- Where it lives: the report's "Expected / Actual" and conclusion lines, the claim comment's assertions, set against the artifacts.
- What good looks like: each claim is something the artifact shows. Causes are marked as hypotheses unless shown. The claim does not extend to versions, platforms, or builds that were not tried. An honest "could not reproduce" with the attempt, the differences, and a guess at what is needed is as good as a successful repro. Words like "verified", "guaranteed", or "confirmed" with no artifact behind them are the warning sign.

## Comms

- Where it lives: the claim comment against the issue body; both comments against the `Repo facts` lines on bug-report template and contribution/AI policy.
- What good looks like: the claim names this issue's real problem and one concrete next step, with modest promises. If the repo facts state an AI policy that requires disclosure, both comments disclose; a policy that is silent or permissive needs no disclosure. Interchangeable boilerplate ("please assign me, I will fix it in 2 days") or a bare +1 is not good.
