---
name: enriching-data
description: Enrich contact and company data using x402-protected APIs. Use when enriching person profiles by email/LinkedIn/phone, enriching companies by domain, finding contact details, scraping LinkedIn profiles, or searching for people/organizations. Also use when the user asks to "enrich", "lookup", "find info about", or "research" a person or company.
---

# Enriching Data with x402 APIs

Use the x402scan MCP tools to access enrichment APIs at enrichx402.com.

## Prerequisites

If you don't have the x402scan MCP installed, run:

```bash
npx @x402scan/mcp install --client claude-code
```

This enables the `x402scan:*` tools used below.

## Quick Reference

| Task | Endpoint | Price |
|------|----------|-------|
| Enrich person | `/api/apollo/people-enrich` | $0.075 |
| Enrich company | `/api/apollo/org-enrich` | $0.06 |
| Enrich contact | `/api/clado/contacts-enrich` | $0.03 |
| Scrape LinkedIn | `/api/clado/linkedin-scrape` | $0.045 |
| Bulk people (1-10) | `/api/apollo/people-enrich/bulk` | $0.45 |
| Bulk orgs (1-10) | `/api/apollo/org-enrich/bulk` | $0.375 |

## Workflow

1. **Check balance first** using `x402scan:check_balance` tool
2. **Query endpoint pricing** (optional) using `x402scan:query_endpoint` to see cost before calling
3. **Call the endpoint** using `x402scan:execute_call` with:

```
url: https://enrichx402.com/api/{endpoint}
method: POST
body: { ...parameters }
```

## Person Enrichment

Enrich a person using any identifier:

```json
POST https://enrichx402.com/api/apollo/people-enrich
{
  "email": "john@company.com",
  "first_name": "John",
  "last_name": "Doe",
  "organization_name": "Acme Inc",
  "domain": "company.com",
  "linkedin_url": "https://linkedin.com/in/johndoe"
}
```

Returns: name, title, company, employment history, location, social profiles.

## Company Enrichment

Enrich a company by domain:

```json
POST https://enrichx402.com/api/apollo/org-enrich
{
  "domain": "stripe.com"
}
```

Returns: company name, industry, employee count, revenue, funding, technologies.

## Contact Recovery (Clado)

Find missing contact details:

```json
POST https://enrichx402.com/api/clado/contacts-enrich
{
  "linkedin_url": "https://linkedin.com/in/johndoe",
  "email": "john@example.com",
  "phone": "+1234567890"
}
```

Returns: validated contact info with confidence scores.

## LinkedIn Scraping

Extract full LinkedIn profile:

```json
POST https://enrichx402.com/api/clado/linkedin-scrape
{
  "linkedin_url": "https://linkedin.com/in/johndoe"
}
```

Returns: experience, education, skills, certifications, recommendations.

## Bulk Operations

Process multiple records in one request:

```json
POST https://enrichx402.com/api/apollo/people-enrich/bulk
{
  "people": [
    { "email": "person1@company.com" },
    { "email": "person2@company.com" }
  ]
}
```

## Field Filtering

Reduce costs and response size by excluding fields:

```json
{
  "email": "john@company.com",
  "excludeFields": ["employment_history", "photos"]
}
```

## Additional APIs

For search, mapping, and web scraping endpoints, see [ENDPOINTS.md](ENDPOINTS.md).
