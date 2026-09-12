# Documentation project instructions

## About this project

- Documentation site for **Jaza** (product of Polele SAS) at docs.jaza.dev
- Built on [Mintlify](https://mintlify.com) — MDX pages + `docs.json`
- Source of truth for integration is the **SDKs**, not raw REST

## Product facts (do not contradict)

- Jaza = prepaid billing for African apps (credit wallets, MoMo top-ups, feature metering)
- Jaza gives developers Mobile Money collection in **19+ African countries**, FX at correct rates, and **USD merchant settlements**
- Tagline: **One integration, unlimited possibilities.**
- Developers use `@jazadev/node` (secret key, server) and either `@jazadev/react-native` or `@jazadev/react` with a publishable key + client session
- Write **stack-agnostic** docs: independent Backend (`Node`) and Frontend (`React Native` | `React`) Tabs — never treat “Expo+Node” as the only story
- Mintlify Tab titles must be stable for in-page sync: `Node`, `React Native`, `React`
- Node constructor is `{ secretKey, publicKey }` — **not** `{ apiKey }`
- Host handshake is `jaza.init({ customerId })` → `InitResult` for `JazaProvider` `getSession` / `authEndpoint`
- Consume: `featureCode` alone uses dashboard `creditsCost`; `credits` alone is a raw debit; **both together** override the debit amount while still attributing `featureCode` on the ledger
- Client UI: `JazaBalance`, `JazaTopUpButton`, `JazaLedger`, `JazaActionButton` — **not** invented names (`TopUpModal`, `FuelBalance`, etc.)
- `JazaBalanceWidget` is a **deprecated alias** of `JazaBalance`
- Top-up JWT is minted by the client SDK from the client session — **not** host `onRequestToken` as the primary path
- Merchant webhooks: dashboard multi-endpoint + `jaza.webhooks.constructEvent(rawBody, signature, secret)`
- Paywall-insufficient client realtime is SDK-internal (`WS /v1/client/realtime`); do not invent a merchant SSE guide
- **Jaza handles** Mobile Money collection, FX into credits/USD (customer-pays local-per-USD rates), a **5% platform fee** on each top-up, and **merchant settlements** (bank payout from **$100** USD, on request or scheduled frequency)
- Developers **do not** set up PawaPay or other aggregators, manage multi-currency settlement, or treat the REST API as the primary integration path
- Sandbox (`jz_test_*`) vs live (`jz_live_*`) keys and data are isolated
- Features and bundles are separate concepts (dashboard); not via a “rate card” HTTP API

## Terminology

| Prefer | Avoid |
|--------|--------|
| credits / wallet | “coins”, vague “balance points” without credits |
| features · bundles (separate pages) | “rate card API”, `jaza.rateCards.*`, conflating features+bundles as one API |
| publishable key / secret key | “public API key” alone without distinguishing |
| client session / `jaza.init` | host `getBalance` + `onRequestToken` as the primary story |
| top-up session (SDK-minted) | “payment link” unless accurate |
| sandbox / live | “prod key” without saying live |
| settlements (Jaza-managed) | “you settle MoMo yourself”, “depends on your PawaPay” |
| `featureCode` (+ optional `credits` override) | `feature` key tied to a rate-card API; XOR-only consume |
| `JazaBalance` | `FuelBalance`, `JazaBalanceWidget` as the preferred name |
| Backend / Frontend stack pickers | “Expo+Node” as the only integration path |

## Forbid list (never recommend as primary)

- Client-side `consume` / secret key in the mobile or web binary
- `Fuel*` component or type names
- Fake rate-card HTTP APIs (`jaza.rateCards.*`)
- `onRequestToken` / host-minted top-up JWT as the **default** top-up path (legacy/advanced only)
- Instructing merchants to create PawaPay accounts
- Invented packages or stacks not marked Coming soon (official clients: `@jazadev/node`, `@jazadev/react-native`, `@jazadev/react`)
- OpenAPI playground as the primary integration path in v1
- Framing Expo+Node as the only supported stack

## Style preferences

- Second person (“you”), active voice
- Sentence case headings
- Bold for UI: Click **API keys**
- Code for packages, env vars, methods
- SDK code samples over curl
- Use Mermaid for architecture / handshake / top-up / consume flows
- Keep examples aligned with package READMEs in `packages/@jaza-node`, `packages/@jaza-react-native`, and `packages/@jaza-react`
- Prefer editing existing pages over inventing new guide titles

## Content boundaries

- **Do** document Node + React Native and Node + React, handshake, gating actions, top-up, consume (including override), webhooks, concepts, auth, dashboard setup, SDK references
- **Do** document `jaza.webhooks.constructEvent` (it exists on `@jazadev/node`)
- **Do not** add an API Reference / OpenAPI playground as primary nav in v1
- **Do not** invent REST endpoints or packages that do not exist
- **Do not** instruct merchants to create PawaPay accounts
- **Do not** invent unsupported client stacks (mark as Coming soon)
- **Do not** write guides that only show one frontend when both apply — use synced Tabs
- Link dashboard to https://jaza.dev/dashboard and product to https://jaza.dev
