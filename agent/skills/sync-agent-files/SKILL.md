---
name: sync-agent-files
description: >
  Synchronize agent-specific copies after any change to agent-related files. Triggered when ANY file is edited in: agent/, any agent skill-copy directory (for
  example .agents/skills/, .claude/skills/, .cursor/rules/, .windsurf/rules/, .gemini/), or agent-specific configs (AGENTS.md, CLAUDE.md, .cursorrules,
  .windsurfrules, CONVENTIONS.md, GEMINI.md, .clinerules, .roomodes, copilot-instructions.md). Must run after every such edit, not only on explicit request.
user-invocable: true
disable-model-invocation: false
---

# Sync agent files

Universal sources live in `agent/` (committed). Each agent keeps its own copies (gitignored). After any change to either side, bring them back in sync.

## What to sync

| Source (committed)      | Agent copy (gitignored)                                                                         |
| ----------------------- | ----------------------------------------------------------------------------------------------- |
| `agent/INSTRUCTIONS.md` | `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `.windsurfrules`, `CONVENTIONS.md`, `GEMINI.md`, etc. |
| `agent/skills/`         | `.agents/skills/`, `.claude/skills/`, `.cursor/rules/`, `.windsurf/rules/`, `.gemini/`          |

For agents without native skills support, do not create a skills directory. Inline each relevant skill into the agent config file instead.

## Procedure

1. **Identify the agent.** Use `agent/SETUP.md` to determine the correct config filename and skill location for the current agent.
2. **Determine what changed.** Compare the committed source with the agent copy — diff content, check timestamps, or just re-read both.
3. **Direction of sync:**
   - `agent/INSTRUCTIONS.md` changed → update the agent config file.
   - `agent/skills/` changed → update the native skills copy, or refresh inlined skill sections for agents without native skills support.
   - Agent copy changed (for example `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `.agents/skills/`) → propagate back to `agent/INSTRUCTIONS.md` or
     `agent/skills/`, then update all other copies.
   - Both changed → merge carefully, committed source wins on conflict.
4. **Apply changes.** Overwrite or merge the target. For native skills support, copy the entire directory — don't cherry-pick individual files. For inline-only
   agents, update the embedded skill sections inside the config file.
5. **Verify.** Confirm the agent copy matches the committed source. No silent drift.
