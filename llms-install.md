# Installing the Chat33 MCP server

Chat33 is a hosted (remote) MCP server. Do not clone, build or run anything:
register the URL with the client and sign in.

- URL: `https://chat33.io/api/mcp/mcp`
- Transport: Streamable HTTP
- Auth: OAuth in the browser, or an `x-api-key` header

## Steps

1. Add a remote server named `chat33` with the URL above. For Cline, in
   `cline_mcp_settings.json`:

   ```json
   {
     "mcpServers": {
       "chat33": {
         "type": "streamableHttp",
         "url": "https://chat33.io/api/mcp/mcp",
         "headers": { "x-api-key": "<CHAT33_API_KEY>" }
       }
     }
   }
   ```

2. Auth. If the client supports MCP OAuth, leave out `headers` and let the user
   sign in when the client asks. Otherwise ask the user for an API key: they
   create it at https://chat33.io (Settings → API Keys). Never invent a key.

3. Check the connection by calling `whoami`. It returns the workspace, plan,
   granted scopes and connected social accounts.

4. If `list_accounts` is empty, tell the user to connect Instagram, Facebook,
   Threads, TikTok, YouTube, X, LinkedIn or Bluesky at https://chat33.io/channels.

## Notes

- Tools that message a real person (`reply_to_conversation`,
  `reply_to_comment`) must be confirmed with the user before calling.
- A 403 "Insufficient scope" means the API key lacks a scope; the user can
  create a key with the missing scope.
- Docs: https://chat33.io/mcp
