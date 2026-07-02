---
name: session-handoff
description: Use when wrapping up a session to update memory files, project plans, and handoff docs so the next session resumes with clear orientation
---

# Session Handoff

## Overview

A closing ritual that captures what shipped, what's blocked, and what's next — written into the project memory so future sessions resume cold with full context.

## Steps

### 1. Check git state
```bash
git log --oneline -10
git log origin/main..HEAD  # confirm commits are pushed
```
If anything is unpushed, surface the git commands for the user to run manually.

### 2. Update or create the project handoff memory file

File: `~/.claude/projects/<project>/memory/project_<feature>_handoff.md`

Use this frontmatter and structure:
```markdown
---
name: project-<feature>-handoff
description: "<feature> — current status as of YYYY-MM-DD"
metadata:
  node_type: memory
  type: project
---

**What shipped:**
- `path/to/file.ts` — one-line description of what changed

**Phase N — In progress**
- ✅ #N Task name — brief note (merged YYYY-MM-DD)
- 🔲 #N Task name — plan at `docs/.../plan.md`; N-task fix

**Next step when resuming:** [Specific, cold-start-ready instruction. Name the skill to invoke, the files to touch, and the order.]

**Why:** [The motivation — deadline, dependency, constraint]
```

### 3. Update MEMORY.md index

If a new handoff file was created, add a one-line entry to `MEMORY.md`:
```
- [Feature Handoff](project_<feature>_handoff.md) — status summary as of YYYY-MM-DD
```

If an existing entry was updated, revise its description to reflect the new status.

### 4. Update the phased project plan (if one exists)

In `docs/first-app-build-project-plan.md` or equivalent:
- Mark completed tasks with ✅ and the merge date
- Add newly discovered tasks
- Note blockers inline with reason

### 5. Confirm to the user

Output a brief summary:
- What was updated
- The exact "Next step when resuming" line written to the handoff doc
- Any unresolved git state (unpushed commits, uncommitted changes)

## Common Mistakes

- Vague "next steps" — write them cold-start-ready: name the skill, file, and action
- Forgetting to verify push succeeded — always run `git log origin/main..HEAD`
- Updating MEMORY.md body instead of the linked file — MEMORY.md is an index only
