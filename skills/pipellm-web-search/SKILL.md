---
name: pipellm-web-search
description: "Use when you need to search the web, read web pages, or find current news. Provides 4 search tools via PipeLLM API with scenario-based selection guidance."
allowed-tools: ["Bash", "Read", "fetch", "curl"]
---

# PipeLLM Web Search

You have access to PipeLLM's web search capabilities through HTTP API calls. This skill teaches you **when** and **how** to use each search type effectively.

## When to Search

You SHOULD use web search when:
- The user asks about **current events, news, or recent developments**
- You need to **verify facts** or check if your knowledge is up to date
- The task requires **real-time data** (prices, stock, weather, scores)
- The user asks you to **research a topic** you're not confident about
- You need to read **specific documentation or articles** from URLs
- The user explicitly asks you to search

You should NOT search when:
- You are confident in your answer and it doesn't depend on recency
- The question is about well-established facts, math, or coding syntax
- The user is asking for help with code that is already in front of you

## Choosing the Right Search Type

### Decision Flow

```
Is this about CURRENT NEWS or BREAKING EVENTS?
  → Yes → News Search (/v1/websearch/search-news)

Do you have a SPECIFIC URL to read?
  → Yes → Web Reader (/v1/websearch/reader)

Do you just need QUICK FACTS or a list of URLs?
  → Yes → Simple Search (/v1/websearch/simple-search)

Do you need DEEP, THOROUGH content?
  → Yes → RAG Search (/v1/websearch/search)
```

### Scenario Guide

| Scenario | Best Tool | Why |
|----------|-----------|-----|
| "What happened with OpenAI today?" | **News Search** | Current events need news-specific sources |
| "Read this article: https://..." | **Web Reader** | User gave a specific URL |
| "What's the latest version of React?" | **Simple Search** | Quick fact lookup, speed matters |
| "Find the official docs for X library" | **Simple Search** | Just need URLs, not deep content |
| "Research how companies use RAG in production" | **RAG Search** | Deep research needs extracted content |
| "Is this API claim accurate?" | **RAG Search** | Fact-checking needs thorough analysis |
| "What are people saying about Rust vs Go?" | **RAG Search** | Multi-source analysis |
| "Summarize this blog post at URL" | **Web Reader** | Reading a known page |
| "Find recent CVEs for log4j" | **News Search** | Security advisories are time-sensitive |
| "What's the stock price of AAPL?" | **Simple Search** | Real-time data, speed matters |

### Speed vs Depth Trade-off

| Tool | Speed | Depth | Cost |
|------|-------|-------|------|
| Simple Search | ~1s ⚡ | Snippets only | $0.05 |
| RAG Search | ~5-15s | Full page content, reranked | $0.05 |
| Web Reader | ~3-10s | Full single page | $0.05 |
| News Search | ~5-15s | News articles, reranked | $0.05 |

**Rule of thumb**: Start with **Simple Search** when speed matters. Use **RAG Search** when you need thorough, reliable content. Use **News Search** for anything time-sensitive.

## How to Call the API

All endpoints use the same authentication pattern:

```bash
curl -H "Authorization: Bearer ${PIPELLM_API_KEY}" \
     "https://api.pipellm.ai/v1/websearch/<endpoint>?q=<query>"
```

The API key starts with `pipe-` and can be obtained at [console.pipellm.com](https://console.pipellm.com).

### Endpoints

#### 1. RAG Search — Deep content extraction
```
GET /v1/websearch/search?q={query}
```
Google Search → Page Crawling → Cohere Embedding → Vector Retrieval → Reranking.
Returns extracted, relevant passages from crawled pages.

#### 2. Simple Search — Fast snippets
```
GET /v1/websearch/simple-search?q={query}
```
Google Search via Serper. Returns search snippets and URLs directly. No crawling.

#### 3. Web Reader — Read a URL
```
GET /v1/websearch/reader?url={url}
```
Fetches a web page and converts to clean Markdown. Handles JavaScript-rendered pages.

#### 4. News Search — Current events
```
GET /v1/websearch/search-news?q={query}
```
Google News via Serper → Page Crawling → RAG pipeline. Optimized for news articles.

### Response Format

Search endpoints return:
```json
{
  "code": 200,
  "message": "success",
  "took_ms": 3200,
  "data": {
    "organic": [
      {
        "title": "Article Title",
        "link": "https://example.com/article",
        "snippet": "Brief description...",
        "contexts": [
          { "idx": 0, "text": "Extracted relevant passage..." }
        ]
      }
    ]
  }
}
```

Web Reader returns:
```json
{
  "code": 200,
  "message": "success",
  "content": "# Page Title\n\nFull page content in Markdown..."
}
```

### Error Handling

| HTTP Status | Meaning | Action |
|-------------|---------|--------|
| 401 / 403 | Invalid or expired API key | Ask user to check key at console.pipellm.com |
| 429 | Rate limited | Wait and retry |
| 500+ | Server error | Retry once, then inform user |
| Timeout | Search took too long | Try a more specific query |

## Writing Effective Queries

- **Be specific**: `"React Server Components streaming SSR"` not `"React"`
- **Include context**: `"Python asyncio timeout handling best practices 2025"`
- **Use natural language**: `"How to deploy Go service to Kubernetes with zero downtime"`
- **For news, name entities**: `"OpenAI GPT-5 release date announcement"`

## Combining Tools for Deep Research

For thorough research tasks, combine tools in stages:

1. **Simple Search** to survey the landscape and find key URLs
2. **Web Reader** on the most authoritative sources for full content
3. Or use **RAG Search** to do steps 1+2 automatically

## Setup (for users)

If the API key is not configured and calls fail, guide the user:

1. Register at [console.pipellm.com](https://console.pipellm.com) — new accounts get **$5 free credit**
2. Go to **API Keys** → **Create Key** (key starts with `pipe-`)
3. Set the key as an environment variable: `export PIPELLM_API_KEY=pipe-your-key`
