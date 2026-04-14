# Ashley Jackson

Full-Stack Developer

Building web applications with a focus on serverless architecture, real-time data pipelines, and developer tooling.

---

## Projects

### [bomweather.com](https://bomweather.com)

Real-time Australian weather observations, forecasts, and radar imagery sourced from the Bureau of Meteorology.

- **Framework**: SvelteKit (Svelte 5) + TypeScript
- **Styling**: Tailwind CSS 4
- **Database**: Neon (serverless PostgreSQL) via Prisma + Kysely
- **Cache**: Upstash Redis
- **Maps**: Leaflet interactive radar
- **AI**: Vercel AI SDK for weather insights
- **Analytics**: [mytart](https://www.npmjs.com/package/mytart)
- **Deployment**: Vercel Edge Runtime (syd1 region)

Architecture: Cron jobs fetch BOM observation, warning, and forecast data, cache it in Redis, and serve it through API endpoints. The frontend renders a region-switchable dashboard with live observations, 7-day forecasts, 3-hour forecasts, rain probability, and radar. Region selection persists via `localStorage`, defaulting to QLD/Brisbane.

API surface:
- `/api/observations/{region}/{city}` — current weather observations
- `/api/warnings/{region}` — active weather warnings
- `/api/forecasts/{region}/daily` — 7-day forecast
- `/api/forecasts/{region}/threehour` — 3-hour hourly forecast
- `/api/forecasts/{region}/rain` — rain probability forecast

---

### [aitrackerstats.com](https://aitrackerstats.com)

AI-powered web analytics platform providing traffic analysis, insights, and team collaboration.

- **Framework**: SvelteKit 2 (Svelte 5) + TypeScript
- **Styling**: TailwindCSS
- **Database**: Neon PostgreSQL via Prisma + Kysely
- **Cache**: Upstash Redis
- **Auth**: Lucia Auth with OAuth (Google, GitHub)
- **Email**: Resend
- **Error Tracking**: Sentry
- **Visualizations**: Chart.js
- **Analytics**: [mytart](https://www.npmjs.com/package/mytart)
- **Deployment**: Vercel

Features: analytics dashboard with charts, historical data archives, custom domain verification, multi-user team management, subscription billing, AI-powered traffic recommendations, and privacy/compliance tooling.


---

### [mytart](https://www.npmjs.com/package/mytart)

Multi-Yield Tracking & Analytics Relay Tool — a framework-agnostic analytics library that fans out events to 17 providers simultaneously via direct HTTP calls.

- **Language**: TypeScript (strict)
- **Build**: tsup (dual ESM/CJS output + DTS)
- **HTTP**: axios with retry interceptor + exponential backoff
- **Fingerprinting**: ThumbmarkJS (lazy-loaded, browser-only)
- **Parsing**: ua-parser-js (bot detection)
- **Package**: [`npm install mytart`](https://www.npmjs.com/package/mytart)

**Providers**: Google Analytics 4, Google Ads, Mixpanel, Segment, Amplitude, Plausible, PostHog, Meta Pixel, Microsoft Clarity, Hotjar, Heap, TikTok, Snapchat, Twitter/X, Reddit, Pinterest, Microsoft Ads — each supporting browser and/or server modes.

Key architecture decisions:
- **No SDK wrappers**: direct HTTP via axios across all server-mode providers
- **Parallel dispatch**: all providers called concurrently via `Promise.all`
- **Per-provider `enabled` flag**: providers off by default
- **Provider groups**: route events to `marketing`, `product`, `infrastructure`, or `physical` subsets
- **Standardized event taxonomy**: 36 standard event names auto-mapped to each provider's native conventions (36+ mappings per provider)
- **Cross-provider linking**: auto-captures click IDs (`gclid`, `fbclid`, `ttclid`, `twclid`, `msclkid`, `li_fat_id`) and cookies (`_fbp`, `_fbc`, `_ga`) for unified attribution
- **Browser fingerprint**: ThumbmarkJS generates a stable cookieless device identifier as `anonymousId`
- **Retry + DLQ**: configurable exponential backoff with in-memory dead-letter queue and replay
- **Global consent**: single `consent: true/false` flag configures GA Consent Mode v2 + Meta Pixel grant/revoke
- **Never throws**: errors returned as `TrackResult` with `success: false`


---

### [whoistld](https://www.npmjs.com/package/whoistld)

TypeScript package for parsing domain names and extracting TLD characteristics — WHOIS privacy support, registration restrictions, DNSSEC, IDN, and category classification. All data embedded locally, zero network requests.

- **Language**: TypeScript (strict)
- **Validation**: Zod schemas for all input/output types
- **Build**: `tsc` (CJS output + DTS)
- **Dependencies**: `zod`, `axios`
- **Package**: [`npm install whoistld`](https://www.npmjs.com/package/whoistld)

API surface:
- `parseDomain(input)` — parse a domain into TLD, domain, subdomain, and TLD characteristics
- `supportsWhoisPrivacy(tld)` — check if a TLD supports WHOIS privacy
- `getTldData(tld)` — get full characteristics for a TLD
- `getAllTlds()` — list all known TLDs
- `isKnownTld(tld)` — check if a TLD exists in the database

TLD characteristics tracked: `whoisPrivacySupport`, `registrationRestrictions` (none/governmental/educational/organizational/geographic/reserved), `dnssecSupport`, `idn`, `category` (generic/country-code/sponsored/infrastructure/test/generic-restricted), and `description`.


---

## Tech Stack Summary

| Area | Technologies |
|---|---|
| Frameworks | SvelteKit, Svelte 5, TypeScript |
| Databases | Neon PostgreSQL (Prisma + Kysely) |
| Caching | Upstash Redis |
| Deployment | Vercel (Edge + Serverless) |
| Auth | Lucia Auth, OAuth 2.0 |
| Payments | Polar.sh |
| Analytics | mytart (custom-built, 17 providers) |
| AI | Vercel AI SDK |
| Maps | Leaflet |
| Charts | Chart.js |
| Email | Resend |
| Validation | Zod |
| Monitoring | Sentry |