# Facebook Invites Skill

![Facebook Invites Skill social preview](assets/facebook-invites-social-preview.png)

A Codex skill that works from an already-open Facebook reactions pop-up and invites every eligible reactor to like or follow a Page you manage.

## What it does

The skill:

1. Uses the open reactions pop-up as the target, so changing reaction totals do not cause it to select the wrong post.
2. Scrolls through the pop-up until Facebook's lazy-loaded reaction list has stabilized.
3. Distinguishes `Invite`, `Invited`, and `Following` states using stable profile identities.
4. Clicks each eligible `Invite` action and verifies that it changes to `Invited`.
5. Runs a final full-list audit and closes the pop-up only when no enabled `Invite` actions remain.

It stops and leaves the pop-up open if Facebook shows an error, rate limit, CAPTCHA, or an unstable list.

## Requirements

- Codex with the in-app Browser capability.
- The `browser:control-in-app-browser` skill available to Codex.
- A Facebook account that can manage the target Page.
- A Facebook post's reactions pop-up opened manually before invoking the skill.

No Facebook API key, access token, or other credential is required by this repository. Authentication remains in the user's existing browser session.

## Install

Clone the repository into your Codex skills directory:

```bash
git clone https://github.com/Evryday-AI/facebook-invites-skill.git ~/.codex/skills/facebook-invites
```

On Windows PowerShell:

```powershell
git clone https://github.com/Evryday-AI/facebook-invites-skill.git "$env:USERPROFILE\.codex\skills\facebook-invites"
```

Restart Codex or begin a new task so the skill catalog refreshes.

## How to use it

1. Open Facebook in the Codex in-app browser and sign in.
2. Navigate to a Page you manage and find the post you want to process.
3. Click the post's reaction count so the reactions pop-up is open.
4. Tell Codex:

   > Run the Facebook Invites skill on the open reactions pop-up.

5. Leave the pop-up open while the workflow runs. Codex will report the completed, already-invited, following, failed, and remaining states.

## Example use case

An independent bookstore publishes a post announcing an author-signing event. The post receives reactions from local readers who do not yet follow the store's Page.

The Page manager opens that post's reactions pop-up and asks Codex to run the Facebook Invites skill. The skill loads the complete list, invites every eligible reader, verifies each invitation, audits for missed rows, and closes the pop-up after the remaining invite count reaches zero.

## Important notes

- The skill never chooses a post from its reaction count. You choose the post by opening its reactions pop-up first.
- Facebook can change its interface or impose rate limits. The workflow stops safely when it cannot verify an action.
- Use the skill only on Pages you are authorized to manage and follow Facebook's terms and applicable anti-spam rules.

## Repository contents

- `SKILL.md` — the Codex workflow and failure-handling contract.
- `README.md` — installation and usage documentation.
- `SECURITY.md` — credential and vulnerability guidance.

## License

MIT. See [LICENSE](LICENSE).
