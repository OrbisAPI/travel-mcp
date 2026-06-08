# Orbis Travel MCP ✈️

> Real airport, flight, hotel, and travel data APIs for AI agents. Pay per call with USDC on Base — no API keys, no accounts, no subscriptions.

[![MCP](https://img.shields.io/badge/MCP-StreamableHTTP-blue)](https://orbisapi.com/api/mcp/travel)
[![x402](https://img.shields.io/badge/payment-x402%20USDC-green)](https://x402.org)

## What's Actually In Here

These are the most-called APIs in this domain on Orbis:

| API | Calls | What it does |
|-----|-------|-------------|
| [Airport Database API](https://orbisapi.com/marketplace/airport-database-api-dc0fd2) | 220 | Full database of airports worldwide with IATA codes |
| [Airport Codes API](https://orbisapi.com/marketplace/airport-codes-api-9f9dc4) | 170 | Look up airports by IATA/ICAO code or city |
| [Airport Code API](https://orbisapi.com/marketplace/airport-code-api-1acd94) | 48 | Resolve airport codes to names and locations |
| [Booking.com Hotels API](https://orbisapi.com/marketplace/booking-com-hotels-api-1295a2) | 46 | Search hotels with availability and pricing |
| [Airline Lookup](https://orbisapi.com/marketplace/airline-lookup-f81514) | 43 | Look up airline details by IATA code |
| [Airport Code Lookup API](https://orbisapi.com/marketplace/airport-code-lookup-api-2292de) | 41 | Detailed airport info from any code |
| [Hotel Availability](https://orbisapi.com/marketplace/hotel-availability-90e467) | 40 | Check hotel availability for dates and location |
| [Airport Info Lookup](https://orbisapi.com/marketplace/airport-info-lookup-52b9e2) | 35 | Full airport details: terminals, gates, facilities |
| [Currency Exchange Reference API](https://orbisapi.com/marketplace/currency-exchange-reference-api-8a0a7d) | 31 | Exchange rates for travel budget planning |
| [Travel Destinations Guide](https://orbisapi.com/marketplace/travel-destinations-guide-89bd6f) | 26 | Destination info, highlights, and travel tips |
| [Flight Search API](https://orbisapi.com/marketplace/flight-search-api-c82323) | 23 | Search available flights between cities |
| [Seat Pitch Comparator API](https://orbisapi.com/marketplace/seat-pitch-comparator-api-38034e) | 21 | Compare legroom across airlines and seat classes |
| [Visa Requirement Lookup](https://orbisapi.com/marketplace/visa-requirement-lookup-87d140) | 19 | Check visa requirements between countries |
| [Baggage Fee Calculator API](https://orbisapi.com/marketplace/baggage-fee-calculator-api-925072) | 19 | Calculate baggage fees for any airline |
| [Flight Carbon API](https://orbisapi.com/marketplace/flight-carbon-api-254095) | 17 | Estimate carbon footprint for a flight route |

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

- *"What's the IATA code for Heathrow and which terminal does British Airways use?"*
- *"Find hotels in Tokyo available August 10–15 under $200/night"*
- *"Do I need a visa to visit Japan if I have a US passport?"*
- *"Search for flights from JFK to LHR next Friday"*
- *"Compare legroom between economy seats on Delta vs United vs American"*
- *"What's the baggage fee for a checked bag on Southwest Airlines?"*
- *"What's the carbon footprint of a round trip from NYC to London?"*
- *"What's the USD to JPY exchange rate for my Tokyo trip budget?"*

## Direct x402 Usage (Node.js)

```javascript
import { wrapFetchWithPayment } from "x402-fetch";
import { privateKeyToAccount } from "viem/accounts";
import { createWalletClient, http } from "viem";
import { base } from "viem/chains";

const account = privateKeyToAccount(process.env.WALLET_PRIVATE_KEY);
const walletClient = createWalletClient({ account, chain: base, transport: http() });
const fetch = wrapFetchWithPayment(globalThis.fetch, walletClient);

// Airport database — 220 real calls on Orbis
const resp = await fetch(
  "https://orbisapi.com/api/proxy/airport-database-api-dc0fd2/lookup",
  { method: "POST", headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ code: "JFK" }) }
);
console.log(await resp.json());
```

See `example.mjs` for a full working script.

## All Orbis Domain MCPs

| Domain | URL |
|--------|-----|
| ₿ Crypto & Blockchain | `https://orbisapi.com/api/mcp/crypto` |
| 🔍 Research & Data | `https://orbisapi.com/api/mcp/research` |
| 🛒 Commerce & Retail | `https://orbisapi.com/api/mcp/commerce` |
| ✈️ Travel | `https://orbisapi.com/api/mcp/travel` |
| 🌐 All 20,000+ APIs | `https://orbisapi.com/api/mcp` |

---

Built by [Orbis](https://orbisapi.com) — the API marketplace for AI agents.
