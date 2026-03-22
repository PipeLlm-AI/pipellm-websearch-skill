# PipeLLM WebSearch API Reference

## Base URL

```
https://api.pipellm.ai
```

## Authentication

All requests require a Bearer token in the Authorization header:

```
Authorization: Bearer pipe-xxxxxxxxxxxxxxxxxxxx
```

## Endpoints

### POST/GET `/v1/websearch/search`

RAG-enhanced web search. Crawls top results, creates vector embeddings, and reranks passages.

**Parameters:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `q` | string | Yes | Search query |

**Response:**
```json
{
  "code": 200,
  "message": "success",
  "took_ms": 5200,
  "data": {
    "organic": [
      {
        "title": "Page Title",
        "link": "https://example.com",
        "snippet": "Search result snippet",
        "contexts": [
          { "idx": 0, "text": "Extracted passage relevant to query" },
          { "idx": 1, "text": "Another relevant passage" }
        ]
      }
    ]
  }
}
```

---

### POST/GET `/v1/websearch/simple-search`

Fast web search returning Google snippets. No page crawling or RAG processing.

**Parameters:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `q` | string | Yes | Search query |

**Response:** Same format as `/v1/websearch/search`, but without `contexts` field.

---

### POST/GET `/v1/websearch/reader`

Fetch and convert a web page to clean Markdown text.

**Parameters:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `url` | string | Yes | Full URL to read |

**Response:**
```json
{
  "code": 200,
  "message": "success",
  "content": "# Page Title\n\nFull extracted content in Markdown format..."
}
```

---

### POST/GET `/v1/websearch/search-news`

Search recent news with RAG-enhanced content extraction.

**Parameters:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `q` | string | Yes | News search query |

**Response:** Same format as `/v1/websearch/search`.

## Error Responses

```json
{
  "code": 401,
  "message": "unauthorized: invalid API key"
}
```

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Bad request (missing query) |
| 401 | Invalid API key |
| 403 | Forbidden (key revoked or insufficient balance) |
| 429 | Rate limited |
| 500 | Internal server error |

## Rate Limits

Standard rate limits apply based on your PipeLLM plan. Check your current limits at [console.pipellm.com](https://console.pipellm.com).

## Pricing

Each request: **$0.05**
