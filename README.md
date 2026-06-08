# Orbis Travel MCP ✈️

> 500+ travel APIs for AI agents. Flights, hotels, destinations — pay per call with USDC on Base.

[![MCP](https://img.shields.io/badge/MCP-StreamableHTTP-blue)](https://orbisapi.com/api/mcp/travel)
[![Payment](https://img.shields.io/badge/payment-x402%20USDC-green)](https://x402.org)

## What's Inside

- **Flights** — search, pricing, availability, routes, airline data
- **Hotels** — search, availability, pricing, reviews
- **Destinations** — country/city info, visa requirements, travel advisories
- **Airports** — IATA codes, schedules, delays, terminal maps
- **Currency** — exchange rates for travel planning

## Quick Start

No API key needed. No account. Paste into your MCP client:

### Claude Desktop / Claude Code
```json
{
  "mcpServers": {
    "orbis-travel": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://orbisapi.com/api/mcp/travel"]
    }
  }
}
```
Config path: `~/Library/Application Support/Claude/claude_desktop_config.json`

### Cursor / Windsurf / Cline
```json
{
  "mcpServers": {
    "orbis-travel": {
      "url": "https://orbisapi.com/api/mcp/travel"
    }
  }
}
```

### OpenAI Codex CLI
```yaml
# ~/.codex/config.yaml
mcpServers:
  orbis-travel:
    type: url
    url: "https://orbisapi.com/api/mcp/travel"
```

## Example Prompts

Once connected, try:

- *"Find flights from NYC to London in July under $800"*
- *"What hotels are available in Tokyo for 3 nights in August?"*
- *"Do I need a visa to visit Japan from the US?"*
- *"What's the current exchange rate from USD to EUR?"*
- *"What are the top tourist attractions in Barcelona?"*

## Direct x402 Usage (Node.js)

```javascript
import { wrapFetchWithPayment } from "x402-fetch";
import { privateKeyToAccount } from "viem/accounts";
import { createWalletClient, http } from "viem";
import { base } from "viem/chains";

const account = privateKeyToAccount(process.env.WALLET_PRIVATE_KEY);
const walletClient = createWalletClient({ account, chain: base, transport: http() });
const fetch = wrapFetchWithPayment(globalThis.fetch, walletClient);

// Search for travel APIs and make a call
const resp = await fetch(
  "https://orbisapi.com/api/proxy/flight-search-api/search",
  {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ origin: "JFK", destination: "LHR", date: "2025-08-15" }),
  }
);
console.log(await resp.json());
```

See `example.mjs` for a full working script.

## MCP Details

| | |
|---|---|
| **MCP URL** | `https://orbisapi.com/api/mcp/travel` |
| **Protocol** | StreamableHTTP + SSE |
| **Payment** | x402 USDC on Base (~$0.02–$0.05/call) |
| **Tools** | `browse_apis`, `call_api` |

## All Orbis Domain MCPs

| Domain | URL |
|--------|-----|
| ₿ Crypto & Blockchain | `https://orbisapi.com/api/mcp/crypto` |
| 🔍 Research & Data | `https://orbisapi.com/api/mcp/research` |
| 🛒 Commerce & Retail | `https://orbisapi.com/api/mcp/commerce` |
| ✈️ Travel | `https://orbisapi.com/api/mcp/travel` |
| 🌐 All 20,200+ APIs | `https://orbisapi.com/api/mcp` |

---

Built by [Orbis](https://orbisapi.com) — the API marketplace for AI agents.
