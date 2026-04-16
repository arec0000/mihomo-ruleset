---
name: git-workflow
description: >
  Git workflow, release cycle, and project principles. Triggered on requests like: "prepare a release", "release", "merge to release", "tag it", "git workflow",
  "commit", "push", and when performing git operations in the project context.
---

# Git workflow

Two-branch model with dated tags.

## Branches

- **`dev`** — working branch. Informal edits: additions, removals, experiments. Commits do not have to be polished.
- **`release`** — stable branch. Only verified releases. URLs pointing to `release` always serve a working, up-to-date list. Updated via fast-forward merge (or
  squash) from `dev`.

## Release cycle

1. Work happens in `dev`: edit `src/*.txt`, rebuild `dist/*.mrs`, commit.
2. Before a release — **test via the dev URL**: `…/mihomo-ruleset/dev/dist/rules-domain.mrs`. The user points mihomo to the dev link and verifies that the rules
   work.
3. **Before publishing, think carefully** whether everything is ready: all edits are covered, `.mrs` files are rebuilt, dev has been tested, changes are agreed
   upon with the user. A release is a deliberate step, not a reflex.
4. Merge `dev` into `release`:
   ```bash
   git checkout release
   git merge --ff-only dev        # or --squash for a flat history
   git push origin release
   ```
5. Create a dated tag:
   ```bash
   DATE=$(date +%Y-%m-%d)
   git tag "$DATE"
   git push origin "$DATE"
   ```

**One release per day, no more.** If a bug is found after tagging, the fix goes into `dev`, users get it via the dev URL, and a proper tagged release only
happens the next calendar day.

## Available URLs

- "always latest stable": `…/mihomo-ruleset/release/dist/rules-domain.mrs`
- "in development / testing": `…/mihomo-ruleset/dev/dist/rules-domain.mrs`
- "pinned to a date": `…/mihomo-ruleset/2026-04-16/dist/rules-domain.mrs`

## How GitHub resolves raw URLs

GitHub's raw server accepts any git ref — branch name, tag, or SHA:

- `…/mihomo-ruleset/release/…` — HEAD of the `release` branch
- `…/mihomo-ruleset/dev/…` — HEAD of the `dev` branch
- `…/mihomo-ruleset/2026-04-16/…` — pinned tag
- `…/mihomo-ruleset/abc1234/…` — specific commit

**Tag format** — ISO date `YYYY-MM-DD` (hyphenated, no time). No `v` / `release-` prefixes.

## Commit messages

- `dev`: short and informal (`add udemy cdn`, `fix discord cidr`, `rm proprietary vpns`)
- merge into `release`: one-line summary of the release contents, details in the body if needed
