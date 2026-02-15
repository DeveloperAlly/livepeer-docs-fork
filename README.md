# Livepeer Docs

### 👩‍💻 Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mintlify) to preview
the documentation changes locally. To install, use the following command

```bash
npm i -g mintlify
```

Run the following command at the root of your documentation (where mint.json is)

```bash
mint dev
```

### 🔗 Notion MCP setup (Cursor Cloud, no local clone)

Use this to connect your Notion task database so AI tools can help with
consolidation and planning directly from this workspace.

#### 1) Create a Notion integration and copy token

1. Go to https://developers.notion.com/.
2. Create an internal integration.
3. Copy the API key (`ntn_...`).

#### 2) Share your task database with the integration

In Notion, open your task database/page and share it with the integration you
created. If you skip this step, queries will return empty/unauthorized results.

#### 3) Add the Notion MCP server in Cursor

In Cursor, open Settings and add an MCP server with:

- Name: `notionApi`
- Command: `npx`
- Args: `-y @notionhq/notion-mcp-server`
- Env: `NOTION_TOKEN=<your_notion_api_key>`

File-based alternative (`/workspace/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "notionApi": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "NOTION_TOKEN": "YOUR_NOTION_API_KEY"
      }
    }
  }
}
```

#### 4) Reload Cursor workspace

Reload the window/workspace after adding MCP config.

#### 5) Verify access

- Confirm the MCP server shows as connected.
- Ask your AI assistant to list Notion resources or read from the shared
  database/page.

#### Security notes

- Never paste real Notion tokens into committed files.
- Keep secrets in workspace settings or local-only config files.
