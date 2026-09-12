# Documentation project instructions

## About this project

- Documentation site for **Jaza** (product of Polele SAS) at docs.jaza.dev
- Built on [Mintlify](https://mintlify.com) — MDX pages + `docs.json`
- Source of truth for integration is the **SDKs**, not raw REST

## Product facts (do not contradict)

- Jaza = prepaid billing for African apps (credit wallets, MoMo top-ups, feature metering)
- Developers use `@jazadev/node` (secret key, server) and either `@jazadev/react-native` (Expo) or `@jazadev/react` (web) with a publishable key + client session
- Node constructor is `{ secretKey, publicKey }` — **not** `{ apiKey }`
- Host handshake is `jaza.init({ customerId })` → `InitResult` for `JazaProvider` `getSession` / `authEndpoint`
- Consume uses `featureCode` (or `credits`) + `idempotencyKey` — **not** `feature` / rate-card APIs
- Client UI: `JazaBalance`, `JazaTopUpButton`, `JazaLedger`, `JazaActionButton` — **not** invented names (`TopUpModal`, `FuelBalance`, etc.)
- `JazaBalanceWidget` is a **deprecated alias** of `JazaBalance`
- Top-up JWT is minted by the client SDK from the client session — **not** host `onRequestToken` as the primary path
- Merchant webhooks: dashboard multi-endpoint + `jaza.webhooks.constructEvent(rawBody, signature, secret)`
- Paywall-insufficient client realtime is SDK-internal (`WS /v1/client/realtime`); do not invent a merchant SSE guide
- **Jaza handles** Mobile Money collection (PawaPay African markets and related rails), FX into credits/USD, and **merchant settlements**
- Developers **do not** set up PawaPay or other aggregators, manage multi-currency settlement, or treat the REST API as the primary integration path
- Sandbox (`jz_test_*`) vs live (`jz_live_*`) keys and data are isolated
- Features, bundles, and markets are configured in the **dashboard**, not via a “rate card” HTTP API

## Terminology

| Prefer | Avoid |
|--------|--------|
| credits / wallet | “coins”, vague “balance points” without credits |
| features and bundles (dashboard) | “rate card API”, `jaza.rateCards.*` |
| publishable key / secret key | “public API key” alone without distinguishing |
| client session / `jaza.init` | host `getBalance` + `onRequestToken` as the primary story |
| top-up session (SDK-minted) | “payment link” unless accurate |
| sandbox / live | “prod key” without saying live |
| settlements (Jaza-managed) | “you settle MoMo yourself”, “depends on your PawaPay” |
| `featureCode` | `feature` key tied to a rate-card API |
| `JazaBalance` | `FuelBalance`, `JazaBalanceWidget` as the preferred name |

## Forbid list (never recommend as primary)

- Client-side `consume` / secret key in the mobile binary
- `Fuel*` component or type names
- Fake rate-card HTTP APIs (`jaza.rateCards.*`)
- `onRequestToken` / host-minted top-up JWT as the **default** top-up path (legacy/advanced only)
- Instructing merchants to create PawaPay accounts
- Invented packages or stacks not marked Coming soon (official clients: `@jazadev/node`, `@jazadev/react-native`, `@jazadev/react`)
- OpenAPI playground as the primary integration path in v1

## Style preferences

- Second person (“you”), active voice
- Sentence case headings
- Bold for UI: Click **API keys**
- Code for packages, env vars, methods
- SDK code samples over curl
- Keep examples aligned with package READMEs in `packages/@jaza-node`, `packages/@jaza-react-native`, and `packages/@jaza-react`
- Prefer editing existing pages over inventing new guide titles

## Content boundaries

- **Do** document Expo + Node and React web + Node, handshake, gating actions, top-up, consume, webhooks, concepts, auth, dashboard setup, SDK references
- **Do** document `jaza.webhooks.constructEvent` (it exists on `@jazadev/node`)
- **Do not** add an API Reference / OpenAPI playground as primary nav in v1
- **Do not** invent REST endpoints or packages that do not exist
- **Do not** instruct merchants to create PawaPay accounts
- **Do not** invent unsupported client stacks (mark as Coming soon)
- **Do not** write top-up guides that only show one SDK when both web and mobile apply
- Link dashboard to https://jaza.dev/dashboard and product to https://jaza.dev
