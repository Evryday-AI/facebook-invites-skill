---
name: facebook-invites
description: Use when the user has opened a Facebook post's reactions pop-up and asks to invite eligible reactors to like or follow the managed Page.
---

# Facebook Invites

## Overview

Treat the already-open reactions pop-up as the complete target contract. Reaction totals are informational and must never be used to find, reopen, or distinguish the post.

Load first, scan once, target stable profiles, and finish only when a DOM-wide audit finds zero enabled `Invite` buttons.

**REQUIRED SUB-SKILL:** Use browser:control-in-app-browser.

## Procedure

1. Claim the in-app Facebook tab. Validate exactly one reactions pop-up from its tabs, rows, and close control; otherwise ask the user to open it.
2. Identify the pop-up's scrollable list from DOM state. Never scroll the background feed or use fixed coordinates.
3. Return to the top and make a **load-only sweep** with large downward scrolls. Do not scan or invite yet.
4. At the apparent bottom, wait five seconds. Compare `scrollHeight`, last stable profile, and loaded identity count. If any changed, resume scrolling and repeat at the next bottom.
5. Nudge upward, return to the bottom, and require a second five-second quiet check with the same signature. Then loading is complete.
6. Scan the loaded DOM once. Record profile URL, name, and state: enabled `Invite`, `Invited`, or `Following`. Deduplicate by URL; never act without a stable identity.
7. Under the user's standing authorization, target every enabled `Invite` by a unique profile-URL locator and its nearest row action. Use locator auto-scroll; do not rewalk the list.
8. Before each click, refresh the DOM snapshot; require the profile and action to resolve once and remain enabled `Invite`. Click and verify the same row becomes `Invited`. If already `Invited` or `Following`, mark `skipped`. On failed verification, refresh the scoped locator and retry once.
9. Audit the full DOM for enabled `Invite` actions. Process all remaining stable profiles, including new ones, and repeat until the count is zero with no failed or unprocessed profiles.
10. Close only after that audit passes. If none were eligible, close and report it. On any failure, leave open and report names and URLs.

## Failure Handling

| Condition | Response |
|---|---|
| Pop-up closes or target changes | Stop; do not infer or reopen the post. |
| Facebook error or rate limit | Stop, leave the pop-up open, and report completed and remaining profiles. |
| CAPTCHA or safety interstitial | Stop and hand control to the user. |
| Click does not verify after retry | Mark `failed`. |
| Lazy loading never stabilizes | Stop, leave the pop-up open, and report the unstable list. |

## Common Mistakes

- Selecting a post from a changing reaction count.
- Treating duplicate displayed names as unique identities.
- Scanning or inviting while lazy loading is still in progress.
- Rewalking the list when profile locators can auto-scroll.
- Treating attempted or discovered counts as completion proof.
- Reporting success while a DOM-wide audit still finds an enabled `Invite`.
