# Agent Setup

You are setting up your working environment for this repository.

1. Identify which agent you are (Claude Code, Codex, Cursor, Windsurf, Aider, Gemini CLI, etc.). This determines which instruction file you create.

2. Read `agent/INSTRUCTIONS.md` — it contains all instructions for maintaining this project.

3. Create your config file in the repo root using YOUR agent's native format:
   - Claude Code → `CLAUDE.md`
   - OpenAI Codex → `AGENTS.md`
   - Cursor → its native instruction format
   - Windsurf → `AGENTS.md` or native rules format
   - Aider → `CONVENTIONS.md`
   - Gemini CLI → `GEMINI.md`
   - Other/unknown → `AGENTS.md` as a portable default

   Do NOT create config files for agents other than yourself.

4. Write the contents of `INSTRUCTIONS.md` adapted to your format. No meta-triggers or self-referential logic — only working instructions.

5. If your agent has a separate runtime config, keep it separate from the instruction file. Example: Codex uses `.codex/config.toml` for runtime settings, not
   in place of `AGENTS.md`.

6. Make sure your file is in `.gitignore` (check — common formats are already listed).

7. Handle skills according to YOUR agent:

   | Agent         | Skills support | Action                                      |
   | ------------- | -------------- | ------------------------------------------- |
   | Claude Code   | native         | Copy `agent/skills/` → `.claude/skills/`    |
   | Codex         | native         | Copy `agent/skills/` → `.agents/skills/`    |
   | Cursor        | native (rules) | Copy `agent/skills/` → `.cursor/rules/`     |
   | Windsurf      | native (rules) | Copy `agent/skills/` → `.windsurf/rules/`   |
   | Gemini CLI    | native         | Copy `agent/skills/` → `.gemini/`           |
   | Aider         | no             | Inline skill contents into `CONVENTIONS.md` |
   | Other/unknown | no             | Inline skill contents into your config file |

   "Inline" means: append each skill's content as a section inside your config file. Do NOT create a skills directory for agents that don't support it. Do NOT
   create directories for agents other than yourself.

8. After setup, wait for a task.
