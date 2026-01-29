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
