---
name: maintain-russian-domains
description: >
  Add, remove, verify, or audit OUR resources in the domain-only mihomo allowlist. Triggered by requests to add a Russian service, update domains, verify
  ownership, refresh the sovereign list, compare with geosite:ru, or remove an entry.
---

# Maintain Russian domains

## Before editing

1. Read `src/services.md` and `src/sources.md`.
2. Check whether the destination is already covered by a Russian TLD suffix.
3. Search existing rules before adding a duplicate or a redundant subdomain.

## Adding an international-zone domain

1. Confirm that the domain belongs to a Russian service using an official site, official documentation, or a reliable community source such as
   `v2fly/domain-list-community`.
2. Gather only root domains and dedicated infrastructure domains.
3. Reject shared clouds, shared CDNs, analytics, advertising, payment processors, and domains used broadly by unrelated foreign services.
4. Add the domain to the matching ecosystem section in `src/rules-domain.txt`.
5. Update `src/services.md` when the service or ecosystem is new.
6. Rebuild `dist/rules-domain.mrs`.

Russian language, a `.com` registration, Russian-speaking founders, or a large Russian audience are not sufficient evidence by themselves.

## Removing or correcting a domain

1. Find all mentions in `src/`, `README.md`, and agent documentation.
2. Remove only the affected rule and registry entry.
3. If the domain is a recurring false-positive candidate, clarify the relevant selection rule in this skill.
4. Rebuild `dist/rules-domain.mrs`.

## Verification and audit

1. Compare the TLD section with IANA and `data/tld-ru`.
2. Compare international-zone ecosystems with `data/category-ru` and its included service files.
3. Verify candidates against first-party sources.
4. A false positive admits a foreign resource. Prefer temporarily rejecting a niche Russian domain.
5. Apply focused changes; do not bulk-copy an upstream geosite category.

## Completion

Run formatting, rebuild the MRS file, verify that only domain artifacts exist, and report which resources were admitted to or removed from the sovereign
internet.
