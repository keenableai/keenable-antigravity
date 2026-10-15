# Keenable plugin for Antigravity and Gemini CLI

Search the web and read pages as clean markdown from Google Antigravity or Gemini
CLI with [Keenable](https://keenable.ai), a web search engine built for AI agents.
**Keyless:** no signup and no API key.

The plugin connects your agent to Keenable's hosted MCP server and adds two skills:
one for everyday web lookups, one for multi-source research with citations.

## Install

**Antigravity CLI**

```bash
agy plugin install https://github.com/keenableai/keenable-antigravity
```

**Antigravity app and IDE**

Clone the repository into your global plugins folder, or into `.agents/plugins/`
of a workspace to enable it for that project only:

```bash
git clone https://github.com/keenableai/keenable-antigravity ~/.gemini/config/plugins/keenable
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/keenableai/keenable-antigravity
```

**MCP server only**

To connect the tools without the skills, add this to
`~/.gemini/config/mcp_config.json` (Antigravity):

```json
{
  "mcpServers": {
    "keenable": {
      "serverUrl": "https://api.keenable.ai/mcp"
    }
  }
}
```

Then ask something that needs the live web.

## Tools

| Tool | What it does |
|---|---|
| `search_web_pages` | Ranked web results with an excerpt of each page, narrowed by site or publication date when needed. |
| `fetch_page_content` | Any URL as clean markdown, or only the part an extraction prompt asks for. |

## Skills

| Skill | What it does |
|---|---|
| `keenable-web` | Everyday web lookups: when to search, when to read a page, how to cite. |
| `keenable-deep-research` | Breaks a broad question into sub-questions, reads the strongest sources, cross-checks, and writes a cited answer. |

## Example prompts

```text
Find the release notes for the libraries in this project since our pinned
versions and list the breaking changes.
```

```text
Search github.com for reports of this error from the last 30 days and tell me
whether there is a known fix.
```

```text
Research the leading agent observability tools and compare them in a table,
with a source for every claim.
```

## Higher rate limits

The plugin sends no credentials, so it runs on Keenable's shared public tier
([rate limits](https://docs.keenable.ai/rate-limits)). To use your own Keenable
account, get an API key from the [console](https://app.keenable.ai/console) and
add the server with it in `~/.gemini/config/mcp_config.json`:

```json
{
  "mcpServers": {
    "keenable-account": {
      "serverUrl": "https://api.keenable.ai/mcp",
      "headers": {
        "X-API-Key": "keen_<your_key>"
      }
    }
  }
}
```

The skills work with either server.

## Data and security

The plugin talks only to `https://api.keenable.ai/mcp` over HTTPS. Search
queries and requested URLs are sent to Keenable, along with an
`X-Keenable-Title` header (`antigravity` or `gemini-cli`) that identifies the
plugin's traffic. It sends no credentials, runs no local code or shell commands,
and reads no local files. See the [privacy policy](https://keenable.ai/privacy).

## Resources

- [Keenable](https://keenable.ai)
- [Documentation](https://docs.keenable.ai)
- [Support](https://keenable.ai/contact)

## License

MIT
