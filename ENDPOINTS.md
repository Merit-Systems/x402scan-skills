# x402 Endpoints Reference

All endpoints at `https://enrichx402.com`. Prices include 2x markup on base cost.

> **IMPORTANT:** Do not guess endpoint paths. All endpoints include a provider prefix (e.g., `/apollo/`, `/grok/`, `/clado/`). See "Common Mistakes" at the end of this document.

## Data Enrichment (Apollo + Clado)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `/api/apollo/people-enrich` | POST | $0.0495 | Enrich person by email/LinkedIn/name |
| `/api/apollo/people-enrich/bulk` | POST | $0.495 | Bulk enrich up to 10 people |
| `/api/apollo/org-enrich` | POST | $0.0495 | Enrich company by domain |
| `/api/apollo/org-enrich/bulk` | POST | $0.495 | Bulk enrich up to 10 companies |
| `/api/apollo/people-search` | POST | $0.02 | Search for people by criteria |
| `/api/apollo/org-search` | POST | $0.02 | Search for companies by criteria |
| `/api/clado/linkedin-scrape` | POST | $0.04 | Scrape full LinkedIn profile |
| `/api/clado/contacts-enrich` | POST | $0.20 | Find email/phone for contacts |

## Web Research (Exa + Firecrawl)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `/api/exa/search` | POST | $0.01 | Neural web search |
| `/api/exa/find-similar` | POST | $0.01 | Find similar URLs |
| `/api/exa/contents` | POST | $0.002 | Extract text from URLs |
| `/api/exa/answer` | POST | $0.01 | Get direct answers to queries |
| `/api/firecrawl/scrape` | POST | $0.0126 | Scrape URL to markdown |
| `/api/firecrawl/search` | POST | $0.0252 | Web search with optional scraping |

## Local Search (Google Maps)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `/api/google-maps/text-search/partial` | POST | $0.02 | Text search (basic fields) |
| `/api/google-maps/text-search/full` | POST | $0.08 | Text search (all fields + atmosphere) |
| `/api/google-maps/nearby-search/partial` | POST | $0.02 | Nearby search (basic fields) |
| `/api/google-maps/nearby-search/full` | POST | $0.08 | Nearby search (all fields) |
| `/api/google-maps/place-details/partial` | POST | $0.02 | Place details (basic fields) |
| `/api/google-maps/place-details/full` | POST | $0.05 | Place details (all fields) |

## Social Intelligence (Grok + Reddit)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `/api/grok/x-search` | POST | $0.02 | Search X/Twitter posts |
| `/api/grok/user-search` | POST | $0.02 | Search X/Twitter users |
| `/api/grok/user-posts` | POST | $0.02 | Get user's recent posts |
| `/api/reddit/search` | POST | $0.02 | Search Reddit posts |
| `/api/reddit/post-comments` | POST | $0.02 | Get post comments |

## News & Shopping (Serper)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `/api/serper/news` | POST | $0.04 | Google News search |
| `/api/serper/shopping` | POST | $0.04 | Google Shopping search |

## People & Property (Whitepages)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `/api/whitepages/person-search` | POST | $0.44 | Search people by name/location |
| `/api/whitepages/property-search` | POST | $0.44 | Search properties |

## Common Parameters

### Field Filtering (Cost Reduction)

Most endpoints support `excludeFields` to reduce response size:

```json
{
  "email": "user@company.com",
  "excludeFields": ["employment_history", "photos"]
}
```

### Bulk Operations

Apollo bulk endpoints accept arrays of up to 10 items:

```json
{
  "people": [
    { "email": "person1@company.com" },
    { "email": "person2@company.com" }
  ]
}
```

## Using the MCP Tools

All endpoints are called via `x402.fetch`:

```mcp
x402.fetch(
  url="https://enrichx402.com/api/{endpoint}",
  method="POST",
  body={ ... }
)
```

The MCP handles wallet authentication and x402 payment automatically.

## Common Mistakes

**Never guess endpoint paths.** All endpoints require the correct provider prefix.

| Incorrect (guessed) | Correct | Error |
|---------------------|---------|-------|
| `/api/people/search` | `/api/apollo/people-search` | 405 |
| `/api/people-enrich` | `/api/apollo/people-enrich` | 405 |
| `/api/org/search` | `/api/apollo/org-search` | 405 |
| `/api/grok/search` | `/api/grok/x-search` | 405 |
| `/api/twitter/search` | `/api/grok/x-search` | 405 |
| `/api/linkedin/scrape` | `/api/clado/linkedin-scrape` | 405 |
| `/api/maps/search` | `/api/google-maps/text-search/partial` | 405 |

**Wrong parameter names will also fail:**

| Incorrect | Correct |
|-----------|---------|
| `{"name": "John Doe"}` | `{"first_name": "John", "last_name": "Doe"}` |
| `{"company": "Acme"}` | `{"organization_name": "Acme"}` |
| `{"url": "..."}` | `{"linkedin_url": "..."}` |

**If unsure:**
1. Use `x402.discover_api_endpoints(url="https://enrichx402.com")` to list all endpoints
2. Use `x402.check_endpoint_schema(url="...")` to see expected parameters
3. Consult the skill documentation (SKILL.md files)
