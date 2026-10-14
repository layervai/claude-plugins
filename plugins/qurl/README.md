# qURL plugin for Claude Code

Share an app running on your machine privately, straight from Claude Code, with
qURL™: no deploy, no account, no API key, no signup. Install the plugin with two
commands in a Claude Code session:

```text
/plugin marketplace add layervai/claude-plugins
/plugin install qurl@layerv
```

Then ask Claude to share what you're working on ("share my app with
ana@example.com"), or use the commands below. The first time it shares, Claude
installs the `qurl` CLI for you.

## What it adds

| Command | What it does |
|---|---|
| `qurl` skill (`/qurl:qurl`) | The qURL agent skill. Claude uses it on its own whenever you want to share, publish or open something with qURL. |
| `/qurl:share [who]` | Share the app you're working on privately: email invitations, email sign-in, review, approved passkeys or a contract. Asks who it's for. |
| `/qurl:approve [who or what] [CRID]` | Decide a waiting request: a verified email (review), a passkey's approval details, a contract entitlement from your backend, or a six-digit code. Never by name. |
| `/qurl:access [change] [CRID]` | See who is invited and who has access; invite more addresses, resend, remove someone, or change the mode. |

The commands load only when you type them, so they add almost nothing to a
session's context.

### Private access modes

| Mode | Who can open it |
|---|---|
| `invite_only` | Only the email addresses you invite. Strangers can't ask. |
| `email_capture` | Anyone who verifies an email address; you receive each one. |
| `review` | People verify an email and ask; you approve each one. |
| `keys` | Passkeys you approve one by one. |
| `contract` | People your own backend entitles (a purchase, a subscription). |

Email verification proves control of a mailbox, not who someone is. The modes
need a `qurl` CLI whose `qurl publish --help` lists `--access`, and a qURL
service with private access turned on. Where either is missing, Claude says so
and shares nothing; it never falls back to a public share or six-digit codes.

## Updates

Claude Code installs a new copy only when the plugin's version changes. Third-party
marketplaces don't update on their own by default: run
`/plugin marketplace update layerv`, or turn on auto-update for `layerv` under
**Marketplaces** in `/plugin`.

## Keeping the bundled skill current (maintainers)

`skills/qurl/SKILL.md` is a copy of the skill served at
<https://layerv.ai/skills/qurl/SKILL.md>, byte for byte. The served file is the
source of truth: never edit the copy here. The `check` workflow compares the two every day
and fails while they differ. To
update it:

1. Copy the served file over the bundled one:

   ```bash
   curl -fsSL https://layerv.ai/skills/qurl/SKILL.md -o plugins/qurl/skills/qurl/SKILL.md
   ```

2. Raise `version` in `.claude-plugin/plugin.json` in the same PR, or people who
   installed the plugin keep the old copy (the `check` workflow refuses a PR that
   changes the plugin without a higher version). Use a patch version for a new
   copy of the skill or a wording change, a minor version for a new command, and a
   major version when a command is removed or renamed. The version lives only in
   `plugin.json`, never in the marketplace entry.
3. If the skill's rules changed, check that `/qurl:share`, `/qurl:approve` and
   `/qurl:access` (in `skills/share`, `skills/approve` and `skills/access`) still
   agree with them.
4. Run `claude plugin validate --strict .` from the repository root.

Any other change to the plugin's files also needs a new version to reach people.
