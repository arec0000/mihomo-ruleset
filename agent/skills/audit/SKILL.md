---
name: audit
description: >
  Full audit of the ruleset against external sources. Triggered on requests like: "gather suggestions", "go through the lists", "check what's missing", "audit",
  "what to add", "what to remove", "compare with alternatives", "audit".
---

# Audit against external sources

A heavyweight process. Results are saved in `pending-additions.md` (temporary, deleted after review).

Sources for comparison are in [`src/sources.md`](../../src/sources.md).

## 1. Validate current sources

Before using the list from `src/sources.md`, verify each one via WebFetch:

- When was the last commit? If older than 6-12 months, mark as stale.
- How many stars / forks? Is the update frequency changing?
- If the repository has moved, been renamed, or archived, find the successor.

## 2. Search for new sources

Via WebSearch / GitHub search, check whether any **new popular and active** projects of the same kind have appeared in the past year. Criteria: 50+ stars,
commits within the last 3 months, adequate documentation, not a duplicate of an existing source.

## 3. Update `src/sources.md`

If any sources turned out to be stale, replace or flag them. If new active sources were found, add them.

## 4. Compare with our lists

For each active source:

- Via WebFetch, read its structure (README, category list, brands).
- Compare with our sections in `src/rules-domain.txt` (section names `# === ... ===` are sufficient).
- Collect candidates for **addition** (present in theirs, missing in ours) and candidates for **removal** (present in ours, but the block has been lifted /
  domain is dead / service has shut down).

## 5. Search for blocking news

In parallel with analyzing existing lists, run a WebSearch for recent news.

**Search window** — from the last audit to the current date. Determine the start date:

- The latest dated tag via `git tag --sort=-v:refname | head -1` (format `YYYY-MM-DD`).
- Or the date of the last commit in `src/` if there are no tags yet: `git log -1 --format=%ai src/`.
- If there have been no commits in `src/` at all, use the date of the last repo commit.

Queries like: "Russia blocked {month} {year}", "Roskomnadzor news {month} {year}", "RKN blocked {service} {year}", "{service} blocked in Russia",
"self-censorship Russia {year}", "{service} withdrew from Russia {year}". Add date filters to queries if the search engine supports them.

Additionally search by category: new AI services with geo-blocks, SaaS withdrawing from the market, financial services, streaming platforms.

Sources: OONI Explorer timeline, Meduza, Habr news, Wikipedia ("List of websites blocked in Russia").

Discard anything dated **before the start of the window** — it was already accounted for in previous iterations.

## 6. Filter candidates

Strictly through `src/excluded.md`. Anything matching the exclusions — **do not suggest**.

## 7. Write to `pending-additions.md`

```markdown
# Audit from {YYYY-MM-DD}

Sources used:

- list with notes (active / stale / new)

## Suggestions for addition

### Service Name

**Category:** RKN / Outside **Where in rules-domain.txt:** section "..." / new after ... **Where in services.md:** category "..." **Annotation:** RKN /
self-restriction / sanctions, date

#### Domains

+.domain.com

#### IP (if any)

1.2.3.0/24

#### Source

itdoginfo / dartraiden / runetfreedom / other

#### Comment

Why, what exactly was missed. 1-2 lines.

## Suggestions for removal

- **Service Name** — reason (block lifted {date} / service shut down / domain dead). Source: {where verified}.

## Not suggested, but found

List of brands not in our lists that were filtered out by `excluded.md`. So the user can see the check was performed.
```

## 8. Limits

- Target around 30-40 suggestions. If there are more useful candidates, report that and add on request.
- For IPs — only purely owned BGP prefixes, no broad cloud ranges.

## 9. Do not edit source files

**Do NOT edit** `src/rules-*.txt` or `src/services.md` during the audit — only create `pending-additions.md`. Application is a separate iteration at the user's
command.
