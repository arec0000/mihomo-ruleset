---
name: git-workflow
description: >
  Git workflow and release cycle. Triggered by commit, push, release, merge, tag, or branch operations.
---

# Git workflow

The repository uses a two-branch model with dated tags.

## Branches

- `dev` — domain changes and testing.
- `release` — stable ruleset served by the permanent raw URL.

## Release cycle

1. Edit `src/rules-domain.txt` and supporting documentation on `dev`.
2. Rebuild `dist/rules-domain.mrs`.
3. Test the dev artifact: `https://raw.githubusercontent.com/arec0000/mihomo-ruleset/dev/dist/rules-domain.mrs`
4. After user validation, fast-forward or squash `dev` into `release`.
5. Create one ISO date tag (`YYYY-MM-DD`) for the release day.

## Stable URL

`https://raw.githubusercontent.com/arec0000/mihomo-ruleset/release/dist/rules-domain.mrs`
