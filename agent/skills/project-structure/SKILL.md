---
name: project-structure
description: >
  Repository files and MRS build command. Use before editing src/ or dist/.
---

# Project structure

- `src/rules-domain.txt` — text source for a mihomo domain rule-provider.
- `src/services.md` — registry of covered services.
- `src/sources.md` — reference sources.
- `dist/rules-domain.mrs` — generated binary ruleset.

Domain rules use suffix matching:

```text
# === Service ===
+.example.com
```

`+.example.com` matches the domain and its subdomains. Comments are allowed.

Rebuild after changing `src/rules-domain.txt`:

```bash
MIHOMO="/Applications/Clash Verge.app/Contents/MacOS/verge-mihomo"
"$MIHOMO" convert-ruleset domain text src/rules-domain.txt dist/rules-domain.mrs
```
