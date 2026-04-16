---
name: sync-agent-files
description: >
  Synchronize agent-specific copies after any change to agent-related files. Triggered when ANY file is edited in: agent/, .claude/skills/, or agent-specific
  configs (CLAUDE.md, .cursorrules, .windsurfrules, .clinerules, .roomodes, copilot-instructions.md). Must run after every such edit, not only on explicit
  request.
user-invocable: true
disable-model-invocation: false
---

# Sync agent files

Universal sources live in `agent/` (committed). Each agent keeps its own copies (gitignored). After any change to either side, bring them back in sync.

## What to sync

| Source (committed)  | Agent copy (gitignored)           |
| ------------------- | --------------------------------- |
| `agent/AGENTS.md`   | `CLAUDE.md`, `.cursorrules`, etc. |
| `agent/skills/*.md` | `.claude/skills/`, etc.           |

## Procedure

1. **Determine what changed.** Compare the source file with the agent copy — diff content, check timestamps, or just re-read both.
2. **Direction of sync:**
   - Source changed → update the agent copy.
   - Agent copy changed (e.g. user edited `CLAUDE.md` directly) → propagate back to source, then update all agent copies.
   - Both changed → merge carefully, source wins on conflict.
3. **Apply changes.** Overwrite or merge the target. For skills, copy the entire directory — don't cherry-pick individual files.
4. **Verify.** Confirm the agent copy matches the source. No silent drift.
