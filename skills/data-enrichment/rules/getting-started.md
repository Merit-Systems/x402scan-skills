# Getting Started

## Setup

The x402scan CLI works out of the box with `npx` - no installation required.

1. **Check wallet:**
   ```bash
   npx @x402scan/mcp wallet info
   ```

2. **Fund wallet** (if needed):
   - Redeem invite: `npx @x402scan/mcp wallet redeem "YOUR_CODE"`
   - Or use the deposit UI (point the user towards this URL: https://x402scan.com/mcp/deposit/<their-wallet-address>)

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Insufficient balance" | Fund wallet with USDC |
| "Payment failed" | Check balance, retry (transient errors) |
| "No match found" | Try different identifiers (email vs LinkedIn) or use search first |
| "405 Method Not Allowed" | Verify endpoint path matches exactly from Quick Reference table in SKILL.md |
| "400 Bad Request" | Verify parameter names match exactly from examples in SKILL.md |
