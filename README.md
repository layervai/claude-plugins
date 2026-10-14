# LayerV plugins for Claude Code

A [Claude Code plugin marketplace](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces) from LayerV.

## qURL

Share the app running on your machine privately with qURL™, straight from Claude
Code: no deploy, no account, no API key, no signup. In a Claude Code session:

```text
/plugin marketplace add layervai/claude-plugins
/plugin install qurl@layerv
```

Then ask Claude to share what you're working on ("share my app with
ana@example.com"), or type `/qurl:share`. Claude picks the private access mode
from what you ask for: email invitations, email sign-in, review, approved
passkeys or a contract with your backend. `/qurl:approve` decides a waiting
request and `/qurl:access` invites more people or removes someone. Nobody gets
in by a name.

The plugin ships the [qURL agent skill](https://layerv.ai/skills/qurl/SKILL.md)
on disk, so Claude never works from a summary of it. Details: [plugins/qurl](plugins/qurl).

Using OpenAI Codex? See [layervai/codex-plugins](https://github.com/layervai/codex-plugins).
Using another MCP client? See [@layervai/qurl-mcp](https://www.npmjs.com/package/@layervai/qurl-mcp),
which also needs no account.

## License

MIT
