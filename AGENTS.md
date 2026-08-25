# Documentation project instructions

## About this project

- Documentation site for **Jaza** (product of Polele SAS) at docs.jaza.dev
- Built on [Mintlify](https://mintlify.com) — MDX pages + `docs.json`
- Source of truth for integration is the **SDKs**, not raw REST

## Product facts (do not contradict)

- Jaza = prepaid billing for African apps (credit wallets, MoMo top-ups, feature metering)
- Developers use `@jazadev/node` (secret key, server) and `@jazadev/react-native` (publishable key + top-up JWT)
- **Jaza handles** Mobile Money collection (PawaPay African markets and related rails), FX into credits/USD, and **merchant settlements**
- Developers **do not** set up PawaPay or other aggregators, manage multi-currency settlement, or treat the REST API as the primary integration path
- Sandbox (`jz_test_*`) vs live (`jz_live_*`) keys and data are isolated

## Terminology

| Prefer | Avoid |
|--------|--------|
| credits / wallet | “coins”, vague “balance points” without credits |
| publishable key / secret key | “public API key” alone without distinguishing |
| top-up session / top-up JWT | “payment link” unless accurate |
| sandbox / live | “prod key” without saying live |
| settlements (Jaza-managed) | “you settle MoMo yourself” |

## Style preferences

- Second person (“you”), active voice
- Sentence case headings
- Bold for UI: Click **API keys**
- Code for packages, env vars, methods
- SDK code samples over curl
- Keep examples aligned with package READMEs in `packages/@jaza-node` and `packages/@jaza-react-native`

## Content boundaries

- **Do** document Expo + Node quickstart, concepts, auth, SDK references
- **Do not** add an API Reference / OpenAPI playground as primary nav in v1
- **Do not** instruct merchants to create PawaPay accounts
- **Do not** invent unsupported client stacks (mark as Coming soon)
- Link dashboard to https://jaza.dev/dashboard and product to https://jaza.dev
