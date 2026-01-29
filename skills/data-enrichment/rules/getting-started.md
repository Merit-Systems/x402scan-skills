# Getting Started

## Setup

1. **Install the x402scan MCP:**
   ```bash
   npx @x402scan/mcp install --client claude-code
   ```

2. **Check wallet:**
   ```
   mcp__x402__get_wallet_info
   ```

3. **Fund wallet** (if needed):
   - Redeem invite: `mcp__x402__redeem_invite(code="YOUR_CODE")`
   - Or send USDC on Base to your wallet address

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "MCP tool not found" | Run install command, restart Claude Code |
| "Insufficient balance" | Fund wallet with USDC |
| "Payment failed" | Check balance, retry (transient errors) |
| "No match found" | Try different identifiers (email vs LinkedIn) or use search first |

## Pricing Reference

| Endpoint | Price |
|----------|-------|
| people-enrich | $0.0495 |
| org-enrich | $0.0495 |
| people-search | $0.02 |
| org-search | $0.02 |
| linkedin-scrape | $0.04 |
| contacts-enrich | $0.20 |
| bulk endpoints | $0.495 (for 10) |
