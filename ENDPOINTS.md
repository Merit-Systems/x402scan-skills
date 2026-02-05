# x402 Endpoints Reference

All endpoints at `https://enrichx402.com`. Prices include 2x markup on base cost.

> **STOP — Do not guess endpoint paths.** All endpoints use the format `https://enrichx402.com/api/{provider}/{action}`. They are NOT the same as each provider's native API paths. Before your first call, run `x402.discover_api_endpoints(url="https://enrichx402.com")` to get the correct paths.

## Common Mistakes (Read First)

**Never guess endpoint paths.** All endpoints require the correct provider prefix under `/api/`.

| Incorrect (guessed) | Correct | Error |
|---------------------|---------|-------|
| `/apollo/organizations/search` | `/api/apollo/org-search` | 405 |
| `/firecrawl/search` | `/api/firecrawl/search` | 404 |
| `/exa/answer` | `/api/exa/answer` | 404 |
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

## Data Enrichment (Apollo + Clado)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `https://enrichx402.com/api/apollo/people-enrich` | POST | $0.0495 | Enrich person by email/LinkedIn/name |
| `https://enrichx402.com/api/apollo/people-enrich/bulk` | POST | $0.495 | Bulk enrich up to 10 people |
| `https://enrichx402.com/api/apollo/org-enrich` | POST | $0.0495 | Enrich company by domain |
| `https://enrichx402.com/api/apollo/org-enrich/bulk` | POST | $0.495 | Bulk enrich up to 10 companies |
| `https://enrichx402.com/api/apollo/people-search` | POST | $0.02 | Search for people by criteria |
| `https://enrichx402.com/api/apollo/org-search` | POST | $0.02 | Search for companies by criteria |
| `https://enrichx402.com/api/clado/linkedin-scrape` | POST | $0.04 | Scrape full LinkedIn profile |
| `https://enrichx402.com/api/clado/contacts-enrich` | POST | $0.20 | Find email/phone for contacts |

## Web Research (Exa + Firecrawl)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `https://enrichx402.com/api/exa/search` | POST | $0.01 | Neural web search |
| `https://enrichx402.com/api/exa/find-similar` | POST | $0.01 | Find similar URLs |
| `https://enrichx402.com/api/exa/contents` | POST | $0.002 | Extract text from URLs |
| `https://enrichx402.com/api/exa/answer` | POST | $0.01 | Get direct answers to queries |
| `https://enrichx402.com/api/firecrawl/scrape` | POST | $0.0126 | Scrape URL to markdown |
| `https://enrichx402.com/api/firecrawl/search` | POST | $0.0252 | Web search with optional scraping |

## Local Search (Google Maps)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `https://enrichx402.com/api/google-maps/text-search/partial` | POST | $0.02 | Text search (basic fields) |
| `https://enrichx402.com/api/google-maps/text-search/full` | POST | $0.08 | Text search (all fields + atmosphere) |
| `https://enrichx402.com/api/google-maps/nearby-search/partial` | POST | $0.02 | Nearby search (basic fields) |
| `https://enrichx402.com/api/google-maps/nearby-search/full` | POST | $0.08 | Nearby search (all fields) |
| `https://enrichx402.com/api/google-maps/place-details/partial` | POST | $0.02 | Place details (basic fields) |
| `https://enrichx402.com/api/google-maps/place-details/full` | POST | $0.05 | Place details (all fields) |

## Social Intelligence (Grok + Reddit)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `https://enrichx402.com/api/grok/x-search` | POST | $0.02 | Search X/Twitter posts |
| `https://enrichx402.com/api/grok/user-search` | POST | $0.02 | Search X/Twitter users |
| `https://enrichx402.com/api/grok/user-posts` | POST | $0.02 | Get user's recent posts |
| `https://enrichx402.com/api/reddit/search` | POST | $0.02 | Search Reddit posts |
| `https://enrichx402.com/api/reddit/post-comments` | POST | $0.02 | Get post comments |

## News & Shopping (Serper)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `https://enrichx402.com/api/serper/news` | POST | $0.04 | Google News search |
| `https://enrichx402.com/api/serper/shopping` | POST | $0.04 | Google Shopping search |

## People & Property (Whitepages)

| Endpoint | Method | Price | Description |
|----------|--------|-------|-------------|
| `https://enrichx402.com/api/whitepages/person-search` | POST | $0.44 | Search people by name/location |
| `https://enrichx402.com/api/whitepages/property-search` | POST | $0.44 | Search properties |

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
