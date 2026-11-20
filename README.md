# Who Got Hacked MCP server

Data breach records, each linked to a US regulator filing or Have I Been Pwned. Search organizations, check a domain or name, list recent incidents.

[Who Got Hacked](https://whogothacked.com) is a public record of data breaches at companies and organizations. Every incident links to a source record a reader can open: a breach notice posted by a US state attorney general or the HHS Office for Civil Rights, a company's SEC Form 8-K Item 1.05 filing, or the Have I Been Pwned catalog. A threat actor's claim is never a source.

**This repository holds configuration only.** The server is hosted at `https://whogothacked.com/mcp`. Its source is not public, and nothing here needs to be built or run.

| | |
|---|---|
| Endpoint | `https://whogothacked.com/mcp` |
| Transport | Streamable HTTP |
| Authentication | None: no account, key or sign-in |
| Tools | 6, all read-only |
| Official MCP Registry | `com.whogothacked/mcp` |
| Documentation | https://whogothacked.com/developers |

## Tools

| Tool | What it does | Input |
|---|---|---|
| `search_breaches` | Search the organizations on record, by name or domain. | `query`, `limit` (optional) |
| `check_organization` | Check one organization by exact domain or name and return its incidents with sources. A looser match comes back as candidates, never as the answer. | `domain` or `name` |
| `get_organization` | Full record for one organization: every incident, figures, dates and source links. | `slug` |
| `get_incident` | One incident with the source records that establish it. | `id` |
| `recent_breaches` | Incidents newest first by the date first on record, optionally within a date range. | `since`, `until`, `limit` (all optional) |
| `about_data` | How records are verified, which sources are read, and when each was last updated. | none |

A miss means there is no record here, not that no breach happened. Counts from different sources are not additive.

## Connect

**Claude (claude.ai and Claude Desktop):** add a custom connector with the URL `https://whogothacked.com/mcp`.

**Claude Code:**

```bash
claude mcp add --transport http whogothacked https://whogothacked.com/mcp
```

**Cursor:** install this repository as a plugin, or add the server to `~/.cursor/mcp.json` or `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "whogothacked": {
      "url": "https://whogothacked.com/mcp"
    }
  }
}
```

**Kiro:** [![Add to Kiro](https://kiro.dev/images/add-to-kiro.svg)](https://kiro.dev/launch/mcp/add?name=whogothacked&config=%7B%22url%22%3A%22https%3A%2F%2Fwhogothacked.com%2Fmcp%22%2C%22disabled%22%3Afalse%2C%22autoApprove%22%3A%5B%5D%7D), or add the server to `.kiro/settings/mcp.json`:

```json
{
  "mcpServers": {
    "whogothacked": {
      "url": "https://whogothacked.com/mcp"
    }
  }
}
```

**VS Code and other clients** that read an `mcpServers` file (for example a workspace `.mcp.json`):

```json
{
  "mcpServers": {
    "whogothacked": {
      "type": "http",
      "url": "https://whogothacked.com/mcp"
    }
  }
}
```

## Terms and limits

Using the server means accepting the terms: https://whogothacked.com/terms. Each IP address can make 300 requests a minute to the MCP server. Over that, the answer is HTTP 429 Too Many Requests: wait 60 seconds before trying again. Privacy policy: https://whogothacked.com/privacy. Support: hello@whogothacked.com. Corrections to a record: https://whogothacked.com/corrections.

The same records are available as a JSON API, with no key: https://whogothacked.com/developers.

## Files

- `mcp.json`: the server entry Cursor plugins and other clients read.
- `.cursor-plugin/plugin.json`: the Cursor plugin manifest.
- `server.json`: a copy of the entry published to the Official MCP Registry.
- `assets/logo.png`: the logo.

The files in this repository are under the MIT License.
