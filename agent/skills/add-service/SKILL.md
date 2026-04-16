---
name: add-service
description: >
  Adding a new service to the ruleset. Triggered on requests like: "add service", "add X", "add service", "include in the list", "need a domain for X", or when
  manually editing src/rules-domain.txt or src/rules-ipcidr.txt to add entries.
---

# Add a new service

When the user asks to "add service X":

1. **Check `src/excluded.md`** — the service may be excluded. If so, ask the user to confirm or decline with an explanation.

2. **Check `src/services.md`** — the service may already exist. If so, let the user know and ask whether it needs updating.

3. **Research the current blocking status** via WebSearch / WebFetch:
   - Who blocked it? RKN / self-restriction / sanctions?
   - When (exact date or month/year)?
   - Full block or partial (specific sub-services only)?
   - Do not trust outdated information — verify the date.

4. **Gather domains:**
   - The primary root domain (`service.com`).
   - Alternative root domains (e.g. Telegram: `telegram.org`, `t.me`, `telegra.ph`).
   - Separate CDN domains that are **not** subdomains of the primary (e.g. YouTube: `googlevideo.com`, `ytimg.com`).
   - **Do not list** subdomains like `www.`, `api.`, `cdn.`, `static.` — the suffix match `+.service.com` already covers them.
   - **Exception:** if the root domain cannot be blocked entirely (e.g. `google.com` — search still works), list only the specific subdomains needed
     (`gemini.google.com`, `ai.google.dev`).

5. **Gather IP ranges (if applicable):**
   - Only needed when the service connects **directly by IP** bypassing DNS (Telegram, Discord voice, WhatsApp calls) OR when DPI blocks by IP rather than SNI.
   - Use only the service's **own** BGP prefixes via `bgp.he.net/ASxxxxx#_prefixes` (and `_prefixes6` for IPv6).
   - **Do not add** broad ranges of public clouds (AWS, GCP, Azure, Cloudflare, Akamai) — they will catch unrelated traffic.
   - **Do not add** entire ASNs of multi-tenant hosters (i3D.net, OVH, Hetzner).
   - For new ranges, check for overlaps with existing ones — aggregate into supernets if subnets are already contained.

6. **Add to `src/rules-domain.txt`:**
   - Create a new section `# === Service Name (context, date) ===` in the appropriate thematic location (messengers with messengers, AI with AI).
   - List domains in the `+.domain.tld` format.

7. **Add to `src/rules-ipcidr.txt`** (if IPs were gathered):
   - Section `# === Service Name — ASN ===`.
   - One CIDR per line.

8. **Add to `src/services.md`:**
   - Find the appropriate category or create a new one.
   - Line: `- **Service Name** (+IP) — {who}, {when}`.
   - The `(+IP)` tag only if an entry was added to `rules-ipcidr.txt`.

9. **Rebuild `dist/*.mrs`.**

10. **Report to the user:** what was added, who blocked it, which domains/IPs, and whether `.mrs` was rebuilt.
