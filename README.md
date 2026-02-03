# x402scan Skills

Skills for accessing x402-protected APIs using the x402scan CLI.

Covers enrichx402.com (data enrichment) and stablestudio.io (media generation).

## Prerequisites

The x402scan CLI works out of the box with `npx` - no installation required:

```bash
# Check it works
npx @x402scan/mcp wallet info
```

Your wallet is auto-created at `~/.x402scan-mcp/wallet.json` on first use.

### Optional: Install as MCP Server

If you prefer MCP tool integration (for Claude Desktop, Cursor, etc.):

```bash
npx @x402scan/mcp install --client cursor
```

## Installation

Copy skills to your skills directory:

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
   ```bash
   npx @x402scan/mcp wallet info
   ```

2. **Discover available endpoints:**
   ```bash
   npx @x402scan/mcp discover "https://enrichx402.com"
   ```

3. **Check endpoint pricing before calling:**
   ```bash
   npx @x402scan/mcp check "https://enrichx402.com/api/apollo/people-enrich"
   ```

4. **Make API calls:**
   ```bash
   npx @x402scan/mcp fetch "https://enrichx402.com/api/apollo/people-enrich" \
     --method POST \
     --body '{"email": "user@company.com"}'
   ```

## CLI Commands Reference

| Command | Description |
|---------|-------------|
| `wallet info` | Get wallet address, balance, deposit link |
| `wallet redeem <code>` | Redeem an invite code |
| `discover <url>` | Find x402 endpoints on an origin |
| `check <url>` | Check endpoint pricing/schema (no payment) |
| `fetch <url>` | HTTP fetch with automatic x402 payment |
| `schema <cmd>` | Get JSON schema for a command |

For full command documentation:
```bash
npx @x402scan/mcp --help
npx @x402scan/mcp schema fetch
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
1. **Use `discover`** to list all available endpoints
2. **Consult the skill documentation** (SKILL.md files have correct paths)
3. **Check ENDPOINTS.md** for the complete reference

Guessing endpoints will result in `405 Method Not Allowed` errors and wasted API calls.

## Funding Your Wallet

If your balance is low:

1. Redeem an invite code: `npx @x402scan/mcp wallet redeem YOUR_CODE`
2. Or deposit USDC on Base to your wallet address

## All Endpoints Reference

See [ENDPOINTS.md](ENDPOINTS.md) for a complete reference of all available endpoints with pricing.
