---
name: keenable-deep-research
description: "Run multi-source web research with Keenable and synthesize a cited answer. Use for literature reviews, market and competitor analyses, due diligence, and detailed comparisons that one search can't cover."
---

# Keenable Deep Research

Produce a thorough, well-cited answer to a broad question by iterating over the
Keenable search and fetch tools. Use this for questions a single search can't
cover. For a quick fact, use the `keenable-web` workflow instead.

## Workflow

1. **Decompose.** Break the question into 3-6 concrete sub-questions and state
   them before searching, so the plan can be checked.
2. **Search per sub-question.** Run a focused `search_web_pages` query for each.
   Use `site` and the `published_after` / `published_before` filters where they
   fit. Search again with a different angle when coverage is thin.
3. **Read the strongest sources.** Use `fetch_page_content` on the most relevant
   results instead of trusting excerpts. Pass `prompt` to pull only the facts
   you need from long pages.
4. **Cross-check.** Confirm every claim that affects the conclusion against at
   least one independent source. State disagreements explicitly.
5. **Synthesize.** Write the answer in your own words, grouped by sub-question
   or theme. Cite every factual claim with its source URL. Separate sourced
   facts from your own analysis, and call out gaps and low-confidence areas.

## Guidance

- Track which sub-questions are answered. Keep going until the question is
  covered, not until the first search returns.
- Prefer primary and authoritative sources. Treat aggregators and undated pages
  with caution, and note each source's date when recency matters.
- For relative dates, compute exact dates from today before searching.
- The tools are keyless and rate-limited. If a long run hits the limit, slow
  down before retrying and tell the user that a Keenable account or API key
  raises the limit (the plugin README explains how). Never ask them to paste a
  key into chat.
