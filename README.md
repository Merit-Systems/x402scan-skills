# x402scan Skills

Skills for accessing x402-protected APIs using the x402scan MCP.

Covers enrichx402.com (data enrichment) and stablestudio.io (media generation).

> **CRITICAL — Do not guess endpoint paths.** All enrichx402.com endpoints use the format `https://enrichx402.com/api/{provider}/{action}`. They are NOT the same as each provider's native API paths (e.g., Apollo's `/organizations/search` becomes `/api/apollo/org-search`). Before your first call, run `x402.discover_api_endpoints(url="https://enrichx402.com")` or use the exact URLs from SKILL.md Quick Reference tables.

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

2. **Discover endpoints (required before first fetch):**

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
