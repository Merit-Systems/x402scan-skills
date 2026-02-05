# x402scan Skills

Skills for accessing x402-protected APIs using the x402scan MCP.

Covers enrichx402.com (data enrichment) and stablestudio.io (media generation).

## Portable MCP Skills

These skills use a **portable format** that works across different MCP clients:

- **Claude Code**: Tools like `mcp__x402__fetch(...)`
- **OpenClaw**: CLI like `mcporter call x402.fetch ...`
- **Cursor**: Native MCP tool invocation
- **Other clients**: Any MCP-compatible integration

Skills declare their MCP dependencies in frontmatter and use generic `<server>.<tool>` notation. Your client translates this to its native invocation format.

## Prerequisites

Install the x402scan MCP for your client:

```bash
# Claude Code
npx @x402scan/mcp install --client claude-code

# Other clients - see client-specific docs
```

This enables the x402 MCP tools used by these skills.

## Installation

Copy skills to your skills directory:

```bash
# Claude Code
cp -r skills/* ~/.claude/skills/

# Or symlink for development
ln -s $(pwd)/skills/* ~/.claude/skills/
```

## Available Skills

| Skill | Use For | Endpoints |
|-------|---------|-----------|
| [wallet](skills/wallet/) | Balance, deposits, invite codes | x402 wallet |
| [media-generation](skills/media-generation/) | AI image & video generation | StableStudio |
| [data-enrichment](skills/data-enrichment/) | Person & company profiles | Apollo, Clado |
| [web-research](skills/web-research/) | Web search & scraping | Exa, Firecrawl |
| [local-search](skills/local-search/) | Places & business info | Google Maps |
| [social-intelligence](skills/social-intelligence/) | Social media research | Grok (X/Twitter), Reddit |
| [news-shopping](skills/news-shopping/) | News & product search | Serper |
| [people-property](skills/people-property/) | People & property lookup | Whitepages |

## Quick Start

1. **Check your balance:**

   ```mcp
   x402.get_wallet_info
   ```

2. **Discover available endpoints:**

   ```mcp
   x402.discover_api_endpoints(url="https://enrichx402.com")
   ```

3. **Check endpoint pricing before calling:**

   ```mcp
   x402.check_endpoint_schema(url="https://enrichx402.com/api/apollo/people-enrich")
   ```

4. **Make API calls:**

   ```mcp
   x402.fetch(
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
1. **Use `x402.discover_api_endpoints`** to list all available endpoints
2. **Consult the skill documentation** (SKILL.md files have correct paths)
3. **Check ENDPOINTS.md** for the complete reference

Guessing endpoints will result in `405 Method Not Allowed` errors and wasted API calls.

## Funding Your Wallet

If your balance is low:

1. Redeem an invite code: `x402.redeem_invite(code="YOUR_CODE")`
2. Or deposit USDC on Base to your wallet address

## All Endpoints Reference

See [ENDPOINTS.md](ENDPOINTS.md) for a complete reference of all available endpoints with pricing.

## Skill Format (for Authors)

Skills that use MCP tools should:

1. **Declare MCP dependencies** in frontmatter:

   ```yaml
   ---
   name: my-skill
   description: |
     What this skill does...
   mcp:
     - x402
   ---
   ```

2. **Use generic tool syntax** in documentation:

   ```mcp
   x402.fetch(
     url="https://enrichx402.com/api/...",
     method="POST",
     body={...}
   )
   ```

3. **Avoid client-specific syntax** like `mcp__x402__fetch(...)` — let clients inject their own invocation context.
