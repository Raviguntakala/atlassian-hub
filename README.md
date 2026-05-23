# MCP Atlassian

![PyPI Version](https://img.shields.io/pypi/v/atlassian-hub)
![PyPI - Downloads](https://img.shields.io/pypi/dm/atlassian-hub)
![PePy - Total Downloads](https://static.pepy.tech/personalized-badge/atlassian-hub?period=total&units=international_system&left_color=grey&right_color=blue&left_text=Total%20Downloads)
[![Run Tests](https://github.com/Raviguntakala/atlassian-hub/actions/workflows/tests.yml/badge.svg)](https://github.com/Raviguntakala/atlassian-hub/actions/workflows/tests.yml)
![License](https://img.shields.io/github/license/Raviguntakala/atlassian-hub)
[![Docs](https://img.shields.io/badge/docs-mintlify-blue)](https://atlassian-hub.soomiles.com)

Model Context Protocol (MCP) server for Atlassian products (Confluence and Jira). Supports both Cloud and Server/Data Center deployments.

https://github.com/user-attachments/assets/35303504-14c6-4ae4-913b-7c25ea511c3e

<details>
<summary>Confluence Demo</summary>

https://github.com/user-attachments/assets/7fe9c488-ad0c-4876-9b54-120b666bb785

</details>

## Quick Start

### 1. Get Your API Token

Go to https://id.atlassian.com/manage-profile/security/api-tokens and create a token.

> For Server/Data Center, use a Personal Access Token instead. See [Authentication](https://atlassian-hub.soomiles.com/docs/authentication).

### 2. Configure Your Client

Add `atlassian-hub` to your MCP client. Pick the tab matching your setup — the env block is the same across all of them, only the surrounding config format differs.

**Claude Desktop / Cursor** (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS, `%APPDATA%\Claude\claude_desktop_config.json` on Windows):

```json
{
  "mcpServers": {
    "atlassian-hub": {
      "command": "uvx",
      "args": ["atlassian-hub"],
      "env": {
        "JIRA_URL": "https://your-company.atlassian.net",
        "JIRA_USERNAME": "your.email@company.com",
        "JIRA_API_TOKEN": "your_api_token",
        "CONFLUENCE_URL": "https://your-company.atlassian.net/wiki",
        "CONFLUENCE_USERNAME": "your.email@company.com",
        "CONFLUENCE_API_TOKEN": "your_api_token"
      }
    }
  }
}
```

<details>
<summary><b>Claude Code</b> (Anthropic CLI)</summary>

One-liner via the `claude mcp` command:

```bash
claude mcp add atlassian-hub uvx atlassian-hub \
  -e JIRA_URL=https://your-company.atlassian.net \
  -e JIRA_USERNAME=your.email@company.com \
  -e JIRA_API_TOKEN=your_api_token \
  -e CONFLUENCE_URL=https://your-company.atlassian.net/wiki \
  -e CONFLUENCE_USERNAME=your.email@company.com \
  -e CONFLUENCE_API_TOKEN=your_api_token
```

Or edit `~/.claude.json` (user-scope) / `.mcp.json` (project-scope) with the same JSON shape as the Claude Desktop example above.

</details>

<details>
<summary><b>Codex</b> (OpenAI CLI)</summary>

Edit `~/.codex/config.toml`:

```toml
[mcp_servers.atlassian-hub]
command = "uvx"
args = ["atlassian-hub"]

[mcp_servers.atlassian-hub.env]
JIRA_URL = "https://your-company.atlassian.net"
JIRA_USERNAME = "your.email@company.com"
JIRA_API_TOKEN = "your_api_token"
CONFLUENCE_URL = "https://your-company.atlassian.net/wiki"
CONFLUENCE_USERNAME = "your.email@company.com"
CONFLUENCE_API_TOKEN = "your_api_token"
```

</details>

<details>
<summary><b>GitHub Copilot</b> (VS Code MCP)</summary>

Create `.vscode/mcp.json` in your workspace (or add under `"mcp.servers"` in VS Code settings):

```json
{
  "servers": {
    "atlassian-hub": {
      "type": "stdio",
      "command": "uvx",
      "args": ["atlassian-hub"],
      "env": {
        "JIRA_URL": "https://your-company.atlassian.net",
        "JIRA_USERNAME": "your.email@company.com",
        "JIRA_API_TOKEN": "your_api_token",
        "CONFLUENCE_URL": "https://your-company.atlassian.net/wiki",
        "CONFLUENCE_USERNAME": "your.email@company.com",
        "CONFLUENCE_API_TOKEN": "your_api_token"
      }
    }
  }
}
```

For secrets, prefer `${input:jira_token}` placeholders with `inputs[].type = "promptString"` rather than committing tokens to the file.

</details>

<details>
<summary><b>opencode</b></summary>

Edit `opencode.json` (project-scope) or `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "atlassian-hub": {
      "type": "local",
      "command": ["uvx", "atlassian-hub"],
      "enabled": true,
      "environment": {
        "JIRA_URL": "https://your-company.atlassian.net",
        "JIRA_USERNAME": "your.email@company.com",
        "JIRA_API_TOKEN": "your_api_token",
        "CONFLUENCE_URL": "https://your-company.atlassian.net/wiki",
        "CONFLUENCE_USERNAME": "your.email@company.com",
        "CONFLUENCE_API_TOKEN": "your_api_token"
      }
    }
  }
}
```

</details>

> **Server/Data Center users**: Use `JIRA_PERSONAL_TOKEN` instead of `JIRA_USERNAME` + `JIRA_API_TOKEN`. See [Authentication](https://atlassian-hub.soomiles.com/docs/authentication) for details.

### 3. Start Using

Ask your AI assistant to:
- **"Find issues assigned to me in PROJ project"**
- **"Search Confluence for onboarding docs"**
- **"Create a bug ticket for the login issue"**
- **"Update the status of PROJ-123 to Done"**

## Documentation

Full documentation is available at **[atlassian-hub.soomiles.com](https://atlassian-hub.soomiles.com)**.

Documentation is also available in [llms.txt format](https://llmstxt.org/), which LLMs can consume easily:
- [`llms.txt`](https://atlassian-hub.soomiles.com/llms.txt) — documentation sitemap
- [`llms-full.txt`](https://atlassian-hub.soomiles.com/llms-full.txt) — complete documentation

| Topic | Description |
|-------|-------------|
| [Installation](https://atlassian-hub.soomiles.com/docs/installation) | uvx, Docker, pip, from source |
| [Authentication](https://atlassian-hub.soomiles.com/docs/authentication) | API tokens, PAT, OAuth 2.0 |
| [Configuration](https://atlassian-hub.soomiles.com/docs/configuration) | IDE setup, environment variables |
| [HTTP Transport](https://atlassian-hub.soomiles.com/docs/http-transport) | SSE, streamable-http, multi-user |
| [Tools Reference](https://atlassian-hub.soomiles.com/docs/tools-reference) | All Jira & Confluence tools |
| [Troubleshooting](https://atlassian-hub.soomiles.com/docs/troubleshooting) | Common issues & debugging |

## Compatibility

| Product | Deployment | Support |
|---------|------------|---------|
| Confluence | Cloud | Fully supported |
| Confluence | Server/Data Center | Supported (v6.0+) |
| Jira | Cloud | Fully supported |
| Jira | Server/Data Center | Supported (v8.14+) |

## Key Tools

| Jira | Confluence |
|------|------------|
| `jira_search` - Search with JQL | `confluence_search` - Search with CQL |
| `jira_get_issue` - Get issue details | `confluence_get_page` - Get page content |
| `jira_create_issue` - Create issues | `confluence_create_page` - Create pages |
| `jira_update_issue` - Update issues | `confluence_update_page` - Update pages |
| `jira_transition_issue` - Change status | `confluence_add_comment` - Add comments |

**72 tools total** — See [Tools Reference](https://atlassian-hub.soomiles.com/docs/tools-reference) for the complete list.

## Security

Never share API tokens. Keep `.env` files secure. See [SECURITY.md](SECURITY.md).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for development setup.

## License

MIT - See [LICENSE](LICENSE). Not an official Atlassian product.
