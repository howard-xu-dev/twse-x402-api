# Taiwan Stock & Semiconductor Supply Chain API (x402)

A pay-per-request M2M API providing clean, English-keyed JSON data for Taiwan listed companies (e.g., TSMC `2330`, Foxconn `2317`, Quanta `2382`), sourced directly from the Taiwan Stock Exchange (TWSE) OpenAPI.

Designed for financial AI agents, supply chain monitors, and autonomous trading bots. No API keys or subscriptions required—pay per call via **x402** on **Base Mainnet**.

## Endpoints & Pricing

- **Base URL:** `https://my-ai-api.zaiwrtin.workers.dev`
- **AI Docs (`llms.txt`):** `https://my-ai-api.zaiwrtin.workers.dev/llms.txt`
- **Protocol:** x402 (HTTP 402 Payment Required)
- **Price:** `$0.005` USDC per request (Base Mainnet)

| Endpoint | Description | Example |
| :--- | :--- | :--- |
| `GET /api/tw-stock/revenue?ticker={CODE}` | Latest monthly revenue, MoM%, YoY%, and YTD revenue | `/api/tw-stock/revenue?ticker=2330` |
| `GET /api/tw-stock/news?ticker={CODE}` | Latest TWSE material filings & announcements (omit `ticker` for top 20 market-wide) | `/api/tw-stock/news?ticker=2330` |

## Quick Start for AI Agents (x402-fetch)

```javascript
import { wrapFetchWithPayment } from 'x402-fetch'
import { createWalletClient, http } from 'viem'
import { privateKeyToAccount } from 'viem/accounts'
import { base } from 'viem/chains'

const account = privateKeyToAccount(process.env.PRIVATE_KEY)
const walletClient = createWalletClient({ account, chain: base, transport: http() })
const fetchWithPay = wrapFetchWithPayment(fetch, walletClient)

const res = await fetchWithPay('[https://my-ai-api.zaiwrtin.workers.dev/api/tw-stock/revenue?ticker=2330](https://my-ai-api.zaiwrtin.workers.dev/api/tw-stock/revenue?ticker=2330)')
const data = await res.json()
console.log(data)
