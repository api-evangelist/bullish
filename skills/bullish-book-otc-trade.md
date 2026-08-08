---
name: Book and settle a Bullish OTC trade
description: >-
  Create a bilateral OTC trade on Bullish, match it against a counterparty using a
  shared match key, approve or cancel it, and handle the interdealer-broker path.
api: openapi/bullish-trading-api-openapi.yml
operations:
  - createOtcTrade
  - getOtcTrades
  - getOtcTradeById
  - getUnconfirmedOtcTrade
  - otc-command-approve
  - otc-command-cancel
  - otc-get-delegated-accounts
  - idb-otc-create-trade
  - idb-otc-get-trades
  - idb-otc-command-cancel
  - idb-otc-command-update-remarks
  - idb-otc-get-delegated-accounts
generated: '2026-08-08'
method: generated
source: openapi/bullish-trading-api-openapi.yml
---

# Book and settle a Bullish OTC trade

OTC on Bullish is a two-sided booking: both counterparties submit their view of the
same trade and the exchange matches them on a **shared match key**. Requires OTC
entitlement — an unentitled account gets `9018`.

Prerequisite: hold a valid JWT — see `bullish-authenticate-and-session.md`.

## Submit your side

`createOtcTrade` — `POST /trading-api/v2/otc-trades`.

Constraints the API enforces, all worth validating client-side first:

| Field | Rule | Violation |
|---|---|---|
| `sharedMatchKey` | alphanumeric, length 12–64 inclusive | 9002 |
| `clientOtcTradeId` | numeric, must not start with `0` | 9004 |
| `tradingAccountId` | begins with `111` | 9010 |
| `side` | `BUY` or `SELL` | 9003 |
| `quantity` | positive, base-asset precision | 9006 |
| `price` | positive, quote-asset precision | 9007 |
| trade legs | at most 25 per OTC trade | 9005 |
| legs per market | at most one leg per market per transaction | 9021 |
| `remarks` | at most 255 characters | 9019 |
| market type | `PERPETUAL`, `DATED_FUTURE` or `OPTION` | 9017 |

The signing headers `BX-SIGNATURE`, `BX-NONCE` and `BX-TIMESTAMP` are mandatory on
this surface and their absence has dedicated codes (`9011`, `9012`, `9013`).

## Match

The counterparty submits the mirror side with the same `sharedMatchKey`. Common
match failures:

- `9025` — shared match key is not unique
- `9026` — not distinct maker/taker role with counterparty
- `9027` — counterparty trade inputs mismatch
- `9031` — cannot match an OTC trade on the same account
- `9028` / `9032` — the trade expired before matching

Poll `getUnconfirmedOtcTrade`
(`GET /trading-api/v2/otc-trades/unconfirmed-trade`) for the pending side, and read
the expiry datetime it carries — OTC trades time out.

## Approve or cancel

- `otc-command-approve` — `POST /trading-api/v2/otc-command#approve`
- `otc-command-cancel` — `POST /trading-api/v2/otc-command#cancel`

`9030` means the trade is no longer eligible for acceptance — terminal, do not
retry. Cancellation attribution is visible in the reason codes: `9037` by user,
`9038` by counterparty, `9039` by broker.

## Confirm

`getOtcTrades` (`GET /trading-api/v2/otc-trades`) and `getOtcTradeById`
(`GET /trading-api/v2/otc-trades/{otcTradeId}`). Either `otcTradeId` or
`clientOtcTradeId` must be supplied on lookups (`9020`).

## Interdealer broker path

If you are an IDB acting for institutions, use the `idb` surface instead:

- `idb-otc-get-delegated-accounts` — `GET /trading-api/v2/idb/delegated-accounts`
- `idb-otc-create-trade` — `POST /trading-api/v2/idb/otc-trades`
- `idb-otc-get-trades` — `GET /trading-api/v2/idb/otc-trades#list`
- `idb-otc-command-cancel` — `POST /trading-api/v2/idb/otc-command#cancel`
- `idb-otc-command-update-remarks` — `POST /trading-api/v2/idb/otc-command#update-remarks`

An IDB cannot match a trade within the same institution (`9040`), and calling a
client-only endpoint as an IDB returns 403. Clients discover which accounts they
have delegated with `otc-get-delegated-accounts`
(`GET /trading-api/v2/otc-trades/delegated-accounts`).

Full code registry: `errors/bullish-error-codes.yml` (OTC block, 9001–9999).
