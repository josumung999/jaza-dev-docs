# Jaza documentation

Official developer docs for [Jaza](https://jaza.dev) — prepaid billing infrastructure for African apps.

**Stack:** Mintlify (`docs.json` + MDX). Deployed automatically when you push to `main`.

## Local preview

```bash
npm i -g mint
mint dev
```

Open [http://localhost:3000](http://localhost:3000).

## Custom domain

Attach `docs.jaza.dev` in the [Mintlify dashboard](https://dashboard.mintlify.com) → Domain settings, then add the DNS records Mintlify provides.

## Content rules

See [AGENTS.md](./AGENTS.md). Docs are **SDK-first** (`@jazadev/node`, `@jazadev/react-native`, `@jazadev/react`). Do not document raw REST as the primary integration path. Jaza handles Mobile Money (PawaPay markets) and merchant settlements — developers do not set up aggregators.

## License

See [LICENSE](./LICENSE).
