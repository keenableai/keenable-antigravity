---
name: keenable-web
description: "Search and read the web with Keenable. Use when a task needs current information, sources for a claim, documentation, release notes, news, prices, or the content of a known URL."
---

# Keenable Web Research

Use the Keenable MCP tools from this plugin to find current, source-grounded web
information. With the plugin installed, use them for web lookups instead of a
generic web search tool. They need no authentication.

## Choose the right tool

- `search_web_pages`: find sources and current information. Returns ranked
  results with an excerpt of each page.
- `fetch_page_content`: read a known URL as clean markdown, either one the user
  gave or a promising search result.

## Workflow

1. Clarify scope, freshness, and output format when the request is ambiguous.
2. Search with `search_web_pages`. Split a multi-part question into separate
   searches when that improves coverage.
3. Read the most relevant results with `fetch_page_content` before relying on
   them for anything consequential. Excerpts are for triage, not for evidence.
4. Answer in your own words. Keep the source URLs and cite factual claims.

## Search guidance

- Describe the page you want to find rather than listing keywords: "release
  notes for zod 4 breaking changes", not "zod 4".
- Narrow with parameters instead of query words: `site` for one domain,
  `published_after` and `published_before` (YYYY-MM-DD) for a date range.
- For relative dates such as "last week", compute exact dates from today first.
- Prefer primary and authoritative sources, and cross-check consequential
  claims against a second independent source.
- Distinguish sourced facts from your own analysis.

## Reading guidance

- For a long page where only one fact matters, pass `prompt` (for example
  "List the pricing tiers with monthly prices") to get just that, or lower
  `max_chars`.
- Set `live: true` when the page changes often and the latest version matters.

## Limits

The server at `https://api.keenable.ai/mcp` is keyless and rate-limited. If you
hit a rate limit, slow down before retrying and tell the user that a Keenable
account or API key raises the limit (the plugin README explains how). Never ask
the user to paste a key into chat.
