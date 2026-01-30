# Getting Started

## Setup

1. **Install the x402scan MCP:**
   ```bash
   npx @x402scan/mcp install --client claude-code -y
   ```

2. **Check wallet:**
   ```
   mcp__x402__get_wallet_info
   ```

3. **Fund wallet** (if needed):
   - Redeem invite: `mcp__x402__redeem_invite(code="YOUR_CODE")`
   - Or use the deposit UI (point the user towards this URL: https://x402scan.com/mcp/deposit/<their-wallet-address>)

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "MCP tool not found" | Run install command, restart Claude Code |
| "Insufficient balance" | Fund wallet with USDC |
| "Payment failed" | Check balance, retry (transient errors) |
| "No match found" | Try different identifiers (email vs LinkedIn) or use search first |
| "405 Method Not Allowed" | Verify endpoint path matches exactly from Quick Reference table in SKILL.md |
| "400 Bad Request" | Verify parameter names match exactly from examples in SKILL.md |
