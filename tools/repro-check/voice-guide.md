# Voice guide: how I talk upstream

## Who I am in threads

I'm a student contributor working through a course, making my first real contribution to this repo. I'm comfortable in Python and still learning this codebase, so I say plainly what I have and haven't checked. Readers can expect me to post what I actually ran, and to follow up when I say I will.

## Rules I write by

### Rule: Say what I ran, not what I believe

Every claim in a comment is tied to a command I ran or output I saw. Anything else is labelled as a guess.

- Wrong: "The bug is caused by the verify_password function not catching exceptions."
- Right: "I ran `verify_password(pw, 'not-a-hash')` and got an unhandled UnknownHashError. My guess is that the call isn't wrapped in a try/except, but I haven't confirmed that yet."

### Rule: Name my next step, never a deadline

A claim says what I'll do next on this specific issue. I don't promise a date or a guaranteed fix.

- Wrong: "I'll have a fix up by tomorrow, this is easy."
- Right: "I'll reproduce this on current main and post my findings here; if it holds up I'll open a PR that un-skips the xfail test."

### Rule: Record my environment every time

Any report I post includes OS, versions, and the commit I tested, and says so if that differs from what the issue reports.

- Wrong: "Reproduced on my machine."
- Right: "Reproduced on macOS 15, Python 3.12.4, at commit 45375a6 (current main)."

### Rule: Disclose AI help when the repo asks

If the repo's policy asks for AI disclosure, or I'm unsure, I say which parts Claude helped with.

- Wrong: (posting a Claude-drafted comment with no mention)
- Right: "Disclosure: I used Claude Code to help draft this comment; I ran every command shown myself."

## Things I never post

- "+1" or "same here" with no output of my own
- Guaranteed fixes, deadlines, or "this is trivial"
- A cause stated as fact when I only have a hypothesis
- Output I didn't run myself
- "Should be a quick fix" or any guess at how easy it is before I've read the code
- A claim comment I haven't followed up on: if I can't continue, I say so on the issue
