---
name: next-session-prep
description: Use when a session is winding down or starting without a clear direction for what to tackle next — user says "what's next?", "not sure what to work on next time", "help me prep for the next session" — and the next session's goal needs to be chosen
---

# Next Session Prep

## Overview

Turns "no clear direction" into one concrete, session-sized goal. Reads the project TODO, weighs momentum from recent work, and commits to a recommendation — a decision, not a menu.

## Inputs to gather (in order)

1. **TODO list** — read the `TODO.md` of the project this session is running in (usually at the repo root; if not there, search the working directory for one). Note what's open, what's done, and any "needs on-device check" flags.
2. **Momentum** — what did the current session move forward? Check `git log --oneline -10` for what recent sessions shipped. If session-handoff was invoked earlier in this chat, its "Next step when resuming" line is the primary signal.
3. **Handoff memory** — check `~/.claude/projects/<project>/memory/MEMORY.md` for handoff files (`project_*_handoff.md`) and read the most recent one.

## Decision rules

- **Momentum wins by default.** If recent work builds toward an unfinished goal, the next session continues it — unless an open item clearly beats it on value-to-work.
- **Rank by value-to-work ratio.** Value = user-visible impact, unblocking other items, or closing a lingering loop. Work = fraction of a session. High value / low work ranks first.
- **Bundle small items into sprints.** Adjacent small items (same screen, same subsystem, same theme) become one sprint candidate and are ranked as a unit.
- **Slice large arcs.** If the best candidate spans multiple sessions, recommend only the first session-sized slice — completable and verifiable in one session — and name the broader arc it builds toward.
- **Chains: first domino wins.** When candidates build on each other, recommend the one that must land first and say what it unblocks.
- **Decisions are candidates too.** "Decide whether to keep X" items are near-zero work — resolve them in the prep conversation itself or attach them as warm-up.

## Output contract

The reply is a **Next Session Plan** with exactly these parts, in order:

1. **Momentum verdict** — 1–2 sentences: what recent work built toward, and whether clear momentum exists (yes → toward what; no → say so plainly).
2. **TODO snapshot** — 2–4 sentences on the list's state: what's closed, what clusters remain. Not a restatement of the list.
3. **Ranked candidates** — 3–5 max, each with a one-line value-to-work note. Bundled sprints appear as one candidate; multi-session arcs appear as their first slice.
4. **The recommendation** — ONE goal for the next session, with the concrete first action, what "done" looks like by end of session, and (if part of a larger arc) how it advances the arc.
5. **Prep steps** — only if any exist: things the user can do before the session (device checks, decisions to mull).

Close by offering to record the recommendation via the session-handoff skill so the next session starts cold-ready.

## Common mistakes

- Presenting a menu and asking the user to pick — weigh and recommend; the user can always override.
- Recommending a multi-session item whole ("redesign the Share screen") instead of its first slice ("write the Share screen design spec into `docs/superpowers/specs`").
- Skipping the momentum check and going straight to the TODO — work in flight is cheaper to continue than to restart cold later.
- Ranking every small item separately instead of bundling related ones into a sprint.
