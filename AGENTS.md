# Documentation project instructions

## About this project

- Documentation site for **Jaza** (product of Polele SAS) at docs.jaza.dev
- Built on [Mintlify](https://mintlify.com) — MDX pages + `docs.json`
- Source of truth for integration is the **SDKs**, not raw REST

## Product facts (do not contradict)

- Jaza = prepaid billing for African apps (credit wallets, MoMo top-ups, feature metering)
- Developers use `@jazadev/node` (secret key, server) and `@jazadev/react-native` (publishable key + top-up JWT)
- Node constructor is `{ secretKey, publicKey }` — **not** `{ apiKey }`
- Consume uses `featureCode` (or `credits`) + `idempotencyKey` — **not** `feature` / rate-card APIs
- Mobile UI: `JazaProvider`, `JazaBalanceWidget`, `JazaTopUpButton` — **not** invented names (`TopUpModal`, `FuelBalance`, etc.)
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
| top-up session / top-up JWT | “payment link” unless accurate |
| sandbox / live | “prod key” without saying live |
| settlements (Jaza-managed) | “you settle MoMo yourself”, “depends on your PawaPay” |
| `featureCode` | `feature` key tied to a rate-card API |

## Style preferences

- Second person (“you”), active voice
- Sentence case headings
- Bold for UI: Click **API keys**
- Code for packages, env vars, methods
- SDK code samples over curl
- Keep examples aligned with package READMEs in `packages/@jaza-node` and `packages/@jaza-react-native`
- Prefer editing existing pages over inventing new guide titles

## Content boundaries

- **Do** document Expo + Node quickstart, concepts, auth, dashboard setup, dual-SDK top-up, consume, SDK references
- **Do not** add an API Reference / OpenAPI playground as primary nav in v1
- **Do not** invent REST endpoints, webhook verify helpers (`jaza.webhooks.constructEvent`), or packages (`@jazadev/react` web) that do not exist
- **Do not** instruct merchants to create PawaPay accounts
- **Do not** invent unsupported client stacks (mark as Coming soon)
- **Do not** write top-up guides that only show one SDK
- Link dashboard to https://jaza.dev/dashboard and product to https://jaza.dev
