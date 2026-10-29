# Bullish

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Bullish is an institutional digital-asset exchange and custodian operating a regulated spot, perpetual, dated-futures and options venue with an integrated automated market maker, deterministic central limit order book matching, and qualified custody. It publishes a genuinely machine-readable API estate: a 79-operation OpenAPI 3.0.3 Trading API covering markets, orders, trades, AMM instructions, derivatives positions, portfolio-margin simulation, OTC and inter-dealer-broker booking, custody deposits and withdrawals, and history; six AsyncAPI 3.0.0 WebSocket documents for order book, trades, ticks, auction, index and private account data; and a FIX 4.2/5.0 order-entry and drop-copy surface. Authentication is JWT bearer minted from a client-signed ECDSA R1 or HMAC login rather than OAuth. Bullish is licensed or registered with the Gibraltar Financial Services Commission, BaFin (MiCA CASP and qualified crypto custodian), the Hong Kong SFC, FinCEN and NYDFS, and lists on the NYSE as BLSH.

**Areas:** Digital Assets · Cryptocurrency · Exchange · Trading · Derivatives · Custody · Market Data · Financial Services · Institutional · FIX · Real-Time

## Bullish on APIs.io

Everything profiled for Bullish is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/bullish/](https://apis.io/providers/bullish/)** — or go straight to one of the APIs or properties below.

### APIs (32)

- [Bullish Deprecated Features and APIs](https://apis.io/apis/bullish/deprecated-api/) — A separately published OpenAPI document carrying the 15 operations Bullish has deprecated or decommissioned — the v1 order create/cancel/get surface, v1 AMM…
- [Bullish WebSocket Multi-Order Book API](https://apis.io/apis/bullish/ws-orderbook/) — AsyncAPI 3.0.0 document for simultaneous subscriptions to multiple L1 and L2 order books across different Bullish markets over WebSocket.
- [Bullish WebSocket Anonymous Trades API](https://apis.io/apis/bullish/ws-trades/) — AsyncAPI 3.0.0 document for batched anonymous trade subscriptions across multiple Bullish markets over WebSocket.
- [Bullish WebSocket Anonymous Ticks API](https://apis.io/apis/bullish/ws-ticks/) — AsyncAPI 3.0.0 document for simultaneous tick subscriptions across multiple Bullish markets over WebSocket.
- [Bullish WebSocket Auction Feed API](https://apis.io/apis/bullish/ws-auction/) — AsyncAPI 3.0.0 document for the real-time auction feed, delivering phase and order-imbalance data for Bullish markets with auctions enabled.
- [Bullish WebSocket Index Data API](https://apis.io/apis/bullish/ws-index-data/) — AsyncAPI 3.0.0 document for streaming Bullish index prices, with the subscribed asset set controlled by subscription-message parameters.
- [Bullish WebSocket Private Data API](https://apis.io/apis/bullish/ws-private-data/) — AsyncAPI 3.0.0 document for the authenticated private stream — real-time orders, trades, asset accounts, trading accounts, derivatives positions, AMM…
- [Bullish FIX API](https://apis.io/apis/bullish/fix-api/) — The Bullish FIX order-entry, drop-copy, reference-data and trading-status surface for institutional and high-frequency clients, with session management and…
- [Bullish Aggregator API](https://apis.io/apis/bullish/aggregator-api/) — A small non-authenticated REST surface publishing aggregated public market data — tickers with 24-hour rolling statistics, order books, and the last 100…
- [Bullish Account Assets API](https://apis.io/apis/bullish/bullish-account-assets-api/) — Authenticated APIs for reading account data
- [Bullish Amm Instructions API](https://apis.io/apis/bullish/bullish-amm-instructions-api/) — Authenticated APIs that allow users to Create, View and Terminate AMM instructions. Please refer to the [AMM instruction Overview…
- [Bullish Asset Data API](https://apis.io/apis/bullish/bullish-asset-data-api/) — Non-authenticated APIs for accessing general asset data information
- [Bullish Auction Public API](https://apis.io/apis/bullish/bullish-auction-public-api/) — The auction-public API from Bullish — 2 operation(s) for auction-public.
- [Bullish command entry API](https://apis.io/apis/bullish/bullish-command-entry-api/) — Authenticated API for submitting commands into the exchange.
- [Bullish Custody API](https://apis.io/apis/bullish/bullish-custody-api/) — Authenticated APIs for custody, [Custody Basic Examples](https://github.com/bullish-exchange/api-examples/blob/master/bullish/rest/custody_basics.py)…
- [Bullish deprecated - q3 2024 API](https://apis.io/apis/bullish/bullish-deprecated-q3-2024-api/) — List of deprecated APIs that will be removed towards the end of Q3 2024.
- [Bullish Derivatives API](https://apis.io/apis/bullish/bullish-derivatives-api/) — The derivatives API from Bullish — 1 operation(s) for derivatives.
- [Bullish Derivatives Public API](https://apis.io/apis/bullish/bullish-derivatives-public-api/) — The derivatives-public API from Bullish — 3 operation(s) for derivatives-public.
- [Bullish General API](https://apis.io/apis/bullish/bullish-general-api/) — The general API from Bullish — 2 operation(s) for general.
- [Bullish History API](https://apis.io/apis/bullish/bullish-history-api/) — The history API from Bullish — 5 operation(s) for history.
- [Bullish Idb API](https://apis.io/apis/bullish/bullish-idb-api/) — The Inter-dealer Broker (IDB) API is available to authorized inter-dealer brokers to book OTC trades on Bullish on behalf of their respective end customers.
- [Bullish Index Price Data API](https://apis.io/apis/bullish/bullish-index-price-data-api/) — The index-price-data API from Bullish — 2 operation(s) for index-price-data.
- [Bullish Market Data API](https://apis.io/apis/bullish/bullish-market-data-api/) — Non-authenticated APIs for accessing general market data information
- [Bullish Market History Data API](https://apis.io/apis/bullish/bullish-market-history-data-api/) — The market-history-data API from Bullish — 4 operation(s) for market-history-data.
- [Bullish Market Maker Protection API](https://apis.io/apis/bullish/bullish-market-maker-protection-api/) — The market-maker-protection API from Bullish — 1 operation(s) for market-maker-protection.
- [Bullish Orders API](https://apis.io/apis/bullish/bullish-orders-api/) — Authenticated APIs for interacting with orders
- [Bullish Otc API](https://apis.io/apis/bullish/bullish-otc-api/) — The OTC Clearing Facility API (OTC API) is available to customers to book trades negotiated outside of the Bullish Exchange order book to Bullish's clearing…
- [Bullish Portfolio Margin Simulator API](https://apis.io/apis/bullish/bullish-portfolio-margin-simulator-api/) — The portfolio-margin-simulator API from Bullish — 2 operation(s) for portfolio-margin-simulator.
- [Bullish Session Management API](https://apis.io/apis/bullish/bullish-session-management-api/) — The session-management API from Bullish — 3 operation(s) for session-management.
- [Bullish Trades API](https://apis.io/apis/bullish/bullish-trades-api/) — Authenticated APIs for reading trade data
- [Bullish Trading Accounts API](https://apis.io/apis/bullish/bullish-trading-accounts-api/) — The trading-accounts API from Bullish — 2 operation(s) for trading-accounts.
- [Bullish Transfer API](https://apis.io/apis/bullish/bullish-transfer-api/) — Authenticated API for initiating asset transfers between trading accounts.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (6)

Event-driven and webhook contracts.

- [Auction Feed](https://apis.io/asyncapis/bullish/bullish-ws-auction-asyncapi/)
- [Index Data](https://apis.io/asyncapis/bullish/bullish-ws-index-data-asyncapi/)
- [Multi-Order Book](https://apis.io/asyncapis/bullish/bullish-ws-orderbook-asyncapi/)
- [Private Data](https://apis.io/asyncapis/bullish/bullish-ws-private-data-asyncapi/)
- [Anonymous Ticks](https://apis.io/asyncapis/bullish/bullish-ws-ticks-asyncapi/)
- [Anonymous Trades](https://apis.io/asyncapis/bullish/bullish-ws-trades-asyncapi/)

#### Event channels (6)

Individual events and webhooks the provider emits.

- [/trading-api/v1/index-data](https://apis.io/channels/bullish/trading-api-v1-index-data/)
- [/trading-api/v1/market-data/auction](https://apis.io/channels/bullish/trading-api-v1-market-data-auction/)
- [/trading-api/v1/market-data/orderbook](https://apis.io/channels/bullish/trading-api-v1-market-data-orderbook/)
- [/trading-api/v1/market-data/tick](https://apis.io/channels/bullish/trading-api-v1-market-data-tick/)
- [/trading-api/v1/market-data/trades](https://apis.io/channels/bullish/trading-api-v1-market-data-trades/)
- [/trading-api/v1/private-data](https://apis.io/channels/bullish/trading-api-v1-private-data/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [bullish](https://apis.io/servers/bullish/bullish/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Bullish Agentic Access](https://apis.io/agentic-access/bullish/bullish-agentic-access/)

#### Collections (24)

Postman and Open Collection request collections.

- [Bullish Trading Account Assets API](https://apis.io/collections/bullish/open-bullish-account-assets-api/)
- [Bullish Trading Amm Instructions API](https://apis.io/collections/bullish/open-bullish-amm-instructions-api/)
- [Bullish Trading Asset Data API](https://apis.io/collections/bullish/open-bullish-asset-data-api/)
- [Bullish Trading Auction Public API](https://apis.io/collections/bullish/open-bullish-auction-public-api/)
- [Bullish Trading command entry API](https://apis.io/collections/bullish/open-bullish-command-entry-api/)
- [Bullish Trading Custody API](https://apis.io/collections/bullish/open-bullish-custody-api/)
- [Bullish Features Deprecated API](https://apis.io/collections/bullish/open-bullish-deprecated-api/)
- [Bullish Deprecated Features deprecated - q3 2024 API](https://apis.io/collections/bullish/open-bullish-deprecated-q3-2024-api/)
- [Bullish Trading Derivatives API](https://apis.io/collections/bullish/open-bullish-derivatives-api/)
- [Bullish Trading Derivatives Public API](https://apis.io/collections/bullish/open-bullish-derivatives-public-api/)
- [Bullish Trading General API](https://apis.io/collections/bullish/open-bullish-general-api/)
- [Bullish Trading History API](https://apis.io/collections/bullish/open-bullish-history-api/)
- [Bullish Trading Idb API](https://apis.io/collections/bullish/open-bullish-idb-api/)
- [Bullish Trading Index Price Data API](https://apis.io/collections/bullish/open-bullish-index-price-data-api/)
- [Bullish Trading Market Data API](https://apis.io/collections/bullish/open-bullish-market-data-api/)
- [Bullish Trading Market History Data API](https://apis.io/collections/bullish/open-bullish-market-history-data-api/)
- [Bullish Trading Market Maker Protection API](https://apis.io/collections/bullish/open-bullish-market-maker-protection-api/)
- [Bullish Trading Orders API](https://apis.io/collections/bullish/open-bullish-orders-api/)
- [Bullish Trading Otc API](https://apis.io/collections/bullish/open-bullish-otc-api/)
- [Bullish Trading Portfolio Margin Simulator API](https://apis.io/collections/bullish/open-bullish-portfolio-margin-simulator-api/)
- [Bullish Trading Session Management API](https://apis.io/collections/bullish/open-bullish-session-management-api/)
- [Bullish Trading Trades API](https://apis.io/collections/bullish/open-bullish-trades-api/)
- [Bullish Trading Trading Accounts API](https://apis.io/collections/bullish/open-bullish-trading-accounts-api/)
- [Bullish Trading Transfer API](https://apis.io/collections/bullish/open-bullish-transfer-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Bullish Trading Api Overlay](https://apis.io/overlays/bullish/bullish-trading-api-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Bullish Authentication](https://apis.io/security/bullish/bullish-authentication/)
- [Bullish Domain Security](https://apis.io/security/bullish/bullish-domain-security/)
- [Bullish Trust Center](https://apis.io/security/bullish/bullish-trust-center/)
- [Bullish Vulnerability Disclosure](https://apis.io/security/bullish/bullish-vulnerability-disclosure/)

#### Rate limits (1)

Published request limits.

- [Bullish Rate Limits](https://apis.io/rate-limits/bullish/bullish-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.bullish.com/us/)
- [Documentation](https://docs.exchange.bullish.com/rest/introduction)
- [Getting started](https://docs.exchange.bullish.com/rest/introduction)
- [API reference](https://docs.exchange.bullish.com/rest/api/get-markets)
- [Pricing](https://support.exchange.bullish.com/servicedesk/customer/portal/1/article/9373547)
- [Sign up](https://exchange.bullish.com/register/sign-up)
- [Support](https://support.exchange.bullish.com/servicedesk/customer/portals)
- [Blog](https://www.bullish.com/us/news-insights)
- [Security](https://www.bullish.com/us/bug-bounty-program)
- [Compliance](https://www.bullish.com/us/trust)
- [Trust centre](https://www.bullish.com/us/trust)
- [Terms of service](https://www.bullish.com/us/site-terms-of-use)
- [Privacy policy](https://www.bullish.com/us/legal-us)
- [GitHub](https://github.com/bullish-exchange)
- [Status](https://status.bullish.com/)

## API Evangelist rating

**Kin Score 60.9** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 57.3 |
| Contract governance | 4.5 |
| Operational transparency | 84.2 |
| Developer ergonomics | 73.2 |
| Access clarity | 53.9 |

**Agent readiness 32.1** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 40.7** — Securities & Market Data

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/bullish/](https://apis.io/providers/bullish/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Bullish: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/bullish/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
