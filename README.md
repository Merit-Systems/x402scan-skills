# x402scan Skills

Skills for accessing x402-protected APIs at enrichx402.com using the x402scan MCP.

## Prerequisites

Install the x402scan MCP:

```bash
npx @x402scan/mcp install --client claude-code
```

This enables the `mcp__x402__*` tools used by these skills.

## Installation

Copy skills to your Claude Code skills directory:

```bash
cp -r skills/* ~/.claude/skills/
```

Or symlink for development:

```bash
ln -s $(pwd)/skills/* ~/.claude/skills/
```

## Available Skills

| Skill | Use For | Endpoints |
|-------|---------|-----------|
| [data-enrichment](skills/data-enrichment/) | Person & company profiles | Apollo, Clado |
| [web-research](skills/web-research/) | Web search & scraping | Exa, Firecrawl |
| [local-search](skills/local-search/) | Places & business info | Google Maps |
| [social-intelligence](skills/social-intelligence/) | Social media research | Grok (X/Twitter), Reddit |
| [news-shopping](skills/news-shopping/) | News & product search | Serper |
| [people-property](skills/people-property/) | People & property lookup | Whitepages |

## Quick Start

1. **Check your balance:**
   ```
   mcp__x402__get_wallet_info
   ```

2. **Discover available endpoints:**
   ```
   mcp__x402__discover_api_endpoints(url="https://enrichx402.com")
   ```

3. **Check endpoint pricing before calling:**
   ```
   mcp__x402__check_endpoint_schema(url="https://enrichx402.com/api/apollo/people-enrich")
   ```

4. **Make API calls:**
   ```
   mcp__x402__fetch(
     url="https://enrichx402.com/api/apollo/people-enrich",
     method="POST",
     body={"email": "user@company.com"}
   )
   ```

## IMPORTANT: Do Not Guess Endpoints

**Never guess or invent endpoint paths.** All endpoints have specific paths that include a provider prefix:

| Wrong (guessed) | Correct |
|-----------------|---------|
| `/api/people/search` | `/api/apollo/people-search` |
| `/api/people-enrich` | `/api/apollo/people-enrich` |
| `/api/grok/search` | `/api/grok/x-search` |
| `/api/twitter/search` | `/api/grok/x-search` |

If you don't know the exact endpoint path:
1. **Use `discover_api_endpoints`** to list all available endpoints
2. **Consult the skill documentation** (SKILL.md files have correct paths)
3. **Check ENDPOINTS.md** for the complete reference

Guessing endpoints will result in `405 Method Not Allowed` errors and wasted API calls.

## Funding Your Wallet

If your balance is low:

1. Redeem an invite code: `mcp__x402__redeem_invite(code="YOUR_CODE")`
2. Or deposit USDC on Base to your wallet address

## All Endpoints Reference

See [ENDPOINTS.md](ENDPOINTS.md) for a complete reference of all available endpoints with pricing.
