<p align="center">
  <img src="logo.png" alt="Chat33" width="120">
</p>

# Chat33 MCP Server

Social media MCP server for AI agents. Connect Claude, ChatGPT, Cursor, VS Code or
any MCP client to [Chat33](https://chat33.io) and let your agent publish and
schedule posts to Instagram, Facebook, Threads, TikTok, YouTube, X, LinkedIn and
Bluesky, answer Instagram and Facebook DMs and comments, and build
comment-to-DM automations.

This is a hosted (remote) server. There is nothing to install or run: point your
client at the URL below and sign in.

```
https://chat33.io/api/mcp/mcp
```

- Transport: Streamable HTTP
- Auth: OAuth 2.1 sign-in in the browser (dynamic client registration), or an API key header
- Docs: [chat33.io/mcp](https://chat33.io/mcp)

## Connect your client

Prefer OAuth wherever your client supports it: add the server, choose
**Authenticate** (or the client's login button) and approve in the browser tab
that opens. No API key needed.

### Claude Code

```bash
claude mcp add --transport http --scope user chat33 https://chat33.io/api/mcp/mcp
```

Then run `/mcp`, choose **chat33 → Authenticate** and approve in the browser.

### Claude (claude.ai and Claude Desktop)

Settings → Connectors → **Add custom connector** → URL
`https://chat33.io/api/mcp/mcp` → **Connect**, then approve in the browser.

### ChatGPT

Settings → Apps / Connectors → Advanced → turn on **Developer mode** →
**Create**: name `Chat33`, URL `https://chat33.io/api/mcp/mcp`,
authentication **OAuth**. Sign in to Chat33 and click **Allow**.

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "chat33": {
      "url": "https://chat33.io/api/mcp/mcp"
    }
  }
}
```

### VS Code

`.vscode/mcp.json` in your workspace (or the user MCP config):

```json
{
  "servers": {
    "chat33": {
      "type": "http",
      "url": "https://chat33.io/api/mcp/mcp"
    }
  }
}
```

### Windsurf

`~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "chat33": {
      "serverUrl": "https://chat33.io/api/mcp/mcp"
    }
  }
}
```

### Codex

```bash
codex mcp add chat33 --url https://chat33.io/api/mcp/mcp
codex mcp login chat33
```

### Gemini CLI

```bash
gemini extensions install https://github.com/chat33-io/chat33-mcp
```

### Clients without OAuth (API key)

Create a key in Chat33 → **Settings → API Keys** and send it as an
`x-api-key` header (or `Authorization: Bearer`):

```json
{
  "mcpServers": {
    "chat33": {
      "url": "https://chat33.io/api/mcp/mcp",
      "headers": { "x-api-key": "sk_live_..." }
    }
  }
}
```

## Tools

| Group | Tools |
|-------|-------|
| Account | `list_accounts`, `whoami` |
| Publishing | `create_post`, `validate_post`, `list_posts`, `get_post`, `delete_post`, `get_post_logs`, `request_approval`, `list_approvals`, `add_post_note` |
| Media | `upload_media`, `create_upload_url` |
| Analytics | `get_analytics` |
| Automations | `list_flows`, `get_flow`, `create_flow`, `set_flow_status` |
| Inbox | `list_conversations`, `get_messages`, `reply_to_conversation` |
| Comments | `list_post_comments`, `reply_to_comment` |

Tools that message a real person (`reply_to_conversation`, `reply_to_comment`)
tell the agent to ask for your approval first. New automations are created as
drafts.

## Try asking

- "Schedule this photo to Instagram and Threads for tomorrow at 9am."
- "Which DMs are waiting for a reply? Draft answers for me to approve."
- "Build a flow that DMs the guide link to anyone who comments GUIDE on my last reel."
- "How did my posts do this week?"

## Limits

- Your Chat33 plan's limits on posts and connected accounts apply.
- Instagram and Facebook DM replies only work within 24 hours of the contact's last message.
- Meta allows one private reply per comment, within 7 days.
- LinkedIn: personal profiles only. Bluesky: publishing only (no DMs or comments).

## Links

- Website: [chat33.io](https://chat33.io)
- MCP docs: [chat33.io/mcp](https://chat33.io/mcp)
- REST API: [chat33.io/developers](https://chat33.io/developers)
- n8n node: [n8n-nodes-chat33](https://github.com/chat33-io/n8n-nodes-chat33)
- Support: nemanja@chat33.io

## License

MIT. This repository describes the hosted server; the server itself runs at chat33.io.
