---
name: verify
description: >
  Checking whether services are still current and performing bulk updates. Triggered on requests like: "check if X is outdated", "is X still blocked", "verify
  CIDR", "update the list", "refresh", "mass update", "go through sections".
---

# Verify currency

## Specific section

If the user asks "check if X is outdated" or suspects a CIDR is incorrect:

1. Via WebFetch, check the current state of the service (`bgp.he.net`, official IP ranges).
2. Via WebFetch, check whether the block has been lifted (OONI, news).
3. If the data has changed, update it, aggregate redundant subnets, and rebuild `.mrs`.

## Bulk update

If the entire list needs refreshing, **do not rewrite it from scratch**. Work section by section: check each one for currency, make targeted updates, and
rebuild `.mrs` once at the end.
