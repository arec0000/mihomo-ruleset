---
name: project-structure
description: >
  File format and project structure. Triggered when creating or editing files in src/ (rules-domain.txt, rules-ipcidr.txt, services.md, excluded.md), when
  working with dist/*.mrs, or on requests like: "add service", "remove", "file format", "project structure", "how is the project organized".
---

# Project structure

## `src/rules-domain.txt` (behavior: domain)

```
# === Service Name (context, block date) ===
+.example.com
+.example-cdn.net
```

- `+.example.com` — suffix match: the domain itself plus all subdomains. Used by default.
- `example.com` without `+.` — exact match only. Rarely needed.
- Sections are separated by a comment `# === Name (context) ===`. Comments are ignored by mihomo but are important for navigation and auditing.
- The file is split into two major zones: `RKN-blocked` (blocked from within Russia) and `Outside-blocked` (service self-censorship / sanctions).

## `src/rules-ipcidr.txt` (behavior: ipcidr)

```
# === Service Name — ASN ===
1.2.3.0/24
2001:db8::/32
```

- One CIDR per line, IPv4 or IPv6.
- ASN entries (`AS12345`) are not supported in the `ipcidr` behavior — do not add them.
- Single IPs should be written as `/32` (IPv4) or `/128` (IPv6).

## `src/services.md`

A flat catalog of services organized by category. Each service has a line:

```
- **Service Name** (+IP) — {who blocked}, {when}
```

The `(+IP)` tag means the service also has an entry in `rules-ipcidr.txt`, not just in domains.

"Who blocked":

- **RKN** — blocked from within Russia (Roskomnadzor, courts, prosecutors, TSPU/NSDI)
- **Self-restriction** — the service itself closed access for Russia
- **Sanctions** — withdrawal due to US/EU sanctions
- A combination is possible ("sanctions + RKN")

## `src/excluded.md`

What we do not add to the lists — services, groups, and technical limitations for ipcidr.

## `dist/*.mrs`

Binary files built from `src/rules-*.txt`. Rebuild after every edit:

```bash
MIHOMO="/Applications/Clash Verge.app/Contents/MacOS/verge-mihomo"

"$MIHOMO" convert-ruleset domain text src/rules-domain.txt dist/rules-domain.mrs
"$MIHOMO" convert-ruleset ipcidr text src/rules-ipcidr.txt dist/rules-ipcidr.mrs
```
