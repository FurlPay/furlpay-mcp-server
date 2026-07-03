# @furlpay/mcp-server

[![npm](https://img.shields.io/npm/v/%40furlpay%2Fmcp-server)](https://www.npmjs.com/package/@furlpay/mcp-server)
[![CI](https://github.com/FurlPay/furlpay-mcp-server/actions/workflows/ci.yml/badge.svg)](https://github.com/FurlPay/furlpay-mcp-server/actions)
[![license](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

A [Model Context Protocol](https://modelcontextprotocol.io) server that exposes the [Furlpay](https://furlpay.com) API as tools for AI assistants — drive wallets, swaps, investing, and compliance checks from Claude, Cursor, or any MCP-capable agent.

Zero dependencies, single file, stdio transport. Node 18+.

## Installation

```bash
npm install -g @furlpay/mcp-server
```

This installs the `furlpay-mcp` binary. You can also run it without installing via `npx @furlpay/mcp-server`.

## Configuration

### Claude Desktop / Claude Code

```json
{
  "mcpServers": {
    "furlpay": {
      "command": "furlpay-mcp",
      "env": {
        "FURLPAY_BASE_URL": "http://localhost:3000",
        "FURLPAY_API_KEY": "sk_sandbox_..."
      }
    }
  }
}
```

### Cursor

Add the same block under `mcp.servers` in your Cursor settings.

### Environment variables

| Variable | Default | Description |
|---|---|---|
| `FURLPAY_BASE_URL` | `http://localhost:3000` | Furlpay API origin (hosted or local sandbox). |
| `FURLPAY_API_KEY` | `sk_sandbox_demo` | API key used for tool calls. |

## Tools

| Tool | Description |
|---|---|
| `get_wallet_balances` | Fetch the user's Safe smart-account stablecoin balances and active modules. |
| `quote_swap` | Get the cheapest cross-chain stablecoin swap route with slippage, gas, and ETA. |
| `place_investment_order` | Place a fractional stock/ETF order. |
| `screen_wallet_risk` | AML-screen a wallet address and return a risk verdict. |
| `verify_identity` | Run a KYC identity check. |

Example prompts once connected:

- "What are my Furlpay balances?"
- "Quote swapping 500 USDT on Arbitrum to USDC on Base."
- "Screen 0xabc... for AML risk before I pay them."
- "Buy 50 dollars of VOO."

## Security model

The server is a thin, auditable bridge: every tool call becomes a single HTTP request to the Furlpay API using the key you configured, and the API's own policy engine (limits, AML screening, step-up MFA) still applies. The agent never holds keys with more power than the API key you give it — use a sandbox key for experimentation.

## Related

- [furlpay-node](https://github.com/FurlPay/furlpay-node) — the same API as a typed SDK
- [furlpay-x402](https://github.com/FurlPay/furlpay-x402) — let agents pay per API call instead of holding a key
- [Documentation](https://furlpay.com/docs)

## Contributing and security

See [CONTRIBUTING.md](./CONTRIBUTING.md). Report vulnerabilities privately per [SECURITY.md](./SECURITY.md).

## License

MIT
