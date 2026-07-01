# Furlpay MCP Server

[![CI](https://github.com/FurlPay/furlpay-mcp-server/actions/workflows/ci.yml/badge.svg)](https://github.com/FurlPay/furlpay-mcp-server/actions)
[![license](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

A [Model Context Protocol](https://modelcontextprotocol.io) server that exposes
the [Furlpay](https://furlpay.com) API as tools for AI assistants — Claude Code,
Claude Desktop, Cursor, Windsurf, and any MCP-compatible client.

Single file, zero dependencies, stdio transport.

## Tools

| Tool | Description |
|---|---|
| `get_wallet_balances` | Safe smart-account stablecoin balances & modules |
| `quote_swap` | Cheapest cross-chain stablecoin swap route |
| `place_investment_order` | Fractional stock/ETF order |
| `screen_wallet_risk` | AML risk screening for a wallet address |
| `verify_identity` | KYC identity verification |

## Use with Claude Code

```bash
claude mcp add furlpay -e FURLPAY_BASE_URL=http://localhost:3000 -e FURLPAY_API_KEY=sk_sandbox_demo -- npx -y @furlpay/mcp-server
```

## Use with Claude Desktop / Cursor

```json
{
  "mcpServers": {
    "furlpay": {
      "command": "npx",
      "args": ["-y", "@furlpay/mcp-server"],
      "env": {
        "FURLPAY_BASE_URL": "http://localhost:3000",
        "FURLPAY_API_KEY": "sk_sandbox_demo"
      }
    }
  }
}
```

`FURLPAY_BASE_URL` defaults to `http://localhost:3000` (local sandbox). Point it
at your deployment to drive a live environment.

## License

MIT
