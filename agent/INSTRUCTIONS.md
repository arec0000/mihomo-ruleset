# AI Agent Instructions

Universal instruction file — not tied to any specific agent. Committed to the repo and serves as the source of truth for anyone maintaining the project.

## Role

This is a curated mihomo routing ruleset repository. You maintain it: add/remove services, verify blocking status, rebuild binary files, prepare releases.

User communicates with requests like:

- "add service X"
- "remove Y"
- "check if Z is still blocked"
- "prepare a release"

Before any work, read [`src/excluded.md`](../src/excluded.md) — it lists what we don't add.

## Wording Style

The repository is **public**. This is an abstract routing ruleset with no stated purpose. Never use phrases like "bypass blocking", "unblock", "access
restricted sites", "circumvent sanctions", "circumvent self-restrictions" — that is not the purpose of this list.

- No first person, no addressing the reader (allowed in agent files — `agent/`).
- Blocking categories (RKN / self-restriction / sanctions) — state facts, no opinions.
- IP technical limitations — objective, no euphemisms.

## Principles

- **Accuracy > completeness.** 500 correct rules are better than 50,000 with false positives.
- **One service = one section.** Don't spread domains of one brand across different places.
- **Specific dates.** If you know the day — use the day, not "around 2024".
- **Wildcard `+.` by default.** Exact matches only when truly needed.
- **Keep comments** in `.txt` files.

## Formatting

Don't worry about style manually — run `npm run format` after changes and let it handle formatting per `.editorconfig` and `.prettierrc.json`.

---

## Skills

Detailed instructions are in `skills/`. Auto-triggered by context (for agents with skill support) or read manually.

- **Sync** — [`skills/sync-agent-files/SKILL.md`](skills/sync-agent-files/SKILL.md) — **auto-trigger after ANY edit** to files in `agent/`, agent-specific skill
  copies (for example `.agents/skills/`, `.claude/skills/`, `.cursor/rules/`, `.windsurf/rules/`, `.gemini/`), or agent configs (`AGENTS.md`, `CLAUDE.md`,
  `.cursorrules`, `.windsurfrules`, `CONVENTIONS.md`, `GEMINI.md`, `.clinerules`, `.roomodes`, `copilot-instructions.md`). Read the skill and run the sync
  procedure immediately after such edits — do not wait for explicit request.
- **Project structure** — [`skills/project-structure/SKILL.md`](skills/project-structure/SKILL.md) — **read before editing any file in `src/` or `dist/`**.
  Describes file formats (`rules-domain.txt`, `rules-ipcidr.txt`, `services.md`, `excluded.md`), comment syntax, and how to build `dist/*.mrs`.
- **Add service** — [`skills/add-service/SKILL.md`](skills/add-service/SKILL.md) — full addition process.
- **Remove service** — [`skills/remove-service/SKILL.md`](skills/remove-service/SKILL.md) — removal and adding to exclusions.
- **Verify** — [`skills/verify/SKILL.md`](skills/verify/SKILL.md) — check sections and mass update.
- **Audit** — [`skills/audit/SKILL.md`](skills/audit/SKILL.md) — compare with external sources, find missing entries.
- **Git workflow** — [`skills/git-workflow/SKILL.md`](skills/git-workflow/SKILL.md) — **read before any git operation**. Two-branch model (`dev` → `release`),
  release cycle with ISO-dated tags, commit message conventions.
