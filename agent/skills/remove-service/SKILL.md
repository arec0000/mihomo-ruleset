---
name: remove-service
description: >
  Removing a service from the ruleset. Triggered on requests like: "remove service", "delete X", "remove service", "take it off the list".
---

# Remove a service

1. **Find all mentions** via Grep: `src/rules-domain.txt`, `src/rules-ipcidr.txt`, `src/services.md`.
2. Remove the sections via Edit.
3. If the service is being removed at the user's request (not because the block was lifted), add it to `src/excluded.md` to prevent re-adding during the next
   expansion.
4. **Rebuild `dist/*.mrs`.**
5. Report back.
