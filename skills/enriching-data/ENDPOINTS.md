# Additional Enrichment Endpoints

## Search APIs

### People Search (Apollo)
```json
POST https://enrichx402.com/api/apollo/people-search
{
  "person_titles": ["CEO", "CTO"],
  "person_locations": ["San Francisco"],
  "organization_num_employees_ranges": ["11,50"],
  "per_page": 10
}
```

### Organization Search (Apollo)
```json
POST https://enrichx402.com/api/apollo/org-search
{
  "organization_locations": ["United States"],
  "organization_num_employees_ranges": ["1001,5000"],
  "per_page": 10
}
```

## Google Maps APIs

### Places Search
```json
POST https://enrichx402.com/api/google/places
{
  "query": "coffee shops near Times Square",
  "location": { "lat": 40.758, "lng": -73.9855 },
  "radius": 1000
}
```

### Place Details
```json
POST https://enrichx402.com/api/google/place-details
{
  "place_id": "ChIJN1t_tDeuEmsRUsoyG83frY4"
}
```

### Geocoding
```json
POST https://enrichx402.com/api/google/geocode
{
  "address": "1600 Amphitheatre Parkway, Mountain View, CA"
}
```

## Social Search APIs

### Grok Twitter Search
```json
POST https://enrichx402.com/api/grok/twitter-search
{
  "query": "AI startups funding announcement",
  "max_results": 20
}
```

### Exa Web Search
```json
POST https://enrichx402.com/api/exa/search
{
  "query": "best practices for API design",
  "num_results": 10,
  "use_autoprompt": true
}
```

## Web Scraping

### Firecrawl Scrape
```json
POST https://enrichx402.com/api/firecrawl/scrape
{
  "url": "https://example.com/page",
  "formats": ["markdown", "html"]
}
```

### Firecrawl Crawl
```json
POST https://enrichx402.com/api/firecrawl/crawl
{
  "url": "https://example.com",
  "maxDepth": 2,
  "limit": 10
}
```

## Discovering Endpoints

To see all available endpoints and their current pricing:

```
x402scan:discover_resources
url: https://enrichx402.com
```

To check pricing and schema for a specific endpoint:

```
x402scan:query_endpoint
url: https://enrichx402.com/api/{endpoint}
```

## Response Structure

All enrichment APIs return structured JSON with:
- `data`: The enriched information
- `match_status`: Whether a match was found
- `confidence`: Confidence score (for contact recovery)

## Error Handling

Common errors:
- `402 Payment Required`: Check balance with `x402scan:check_balance`
- `400 Bad Request`: Verify required parameters
- `404 Not Found`: No match for the query
