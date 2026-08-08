---
name: Place, amend, cancel and reconcile a Bullish order
description: >-
  Create an order on a Bullish market, amend or cancel it, and — critically —
  reconcile the outcome after a timeout or 5xx. Bullish has NO idempotency key, so
  the reconciliation step is the skill, not an afterthought.
api: openapi/bullish-trading-api-openapi.yml
operations:
  - getMarkets
  - getMarketBySymbol
  - getMarketOrderBook
  - getMarketTick
  - createOrderV2
  - getOrdersV2
  - getOrderByIdV2
  - trade-get-order-by-client-order-id-v2
  - submitAmendmentCommand
  - submitCancellationCommands
  - getTrades
generated: '2026-08-08'
method: generated
source: https://docs.exchange.bullish.com/rest/order-processing-create-cancel-request-mechanism
---

# Place, amend, cancel and reconcile a Bullish order

Prerequisite: hold a valid JWT — see `bullish-authenticate-and-session.md`.

## Read the instrument before you trade it

1. `getMarkets` (`GET /trading-api/v1/markets`) or `getMarketBySymbol`
   (`GET /trading-api/v1/markets/{symbol}`) — confirm the market exists, is not
   expiring or expired (`3067`), and read `auctionEnabled` / `auctionPriceCollar`.
2. `getMarketOrderBook` (`GET /trading-api/v1/markets/{symbol}/orderbook/hybrid`)
   and `getMarketTick` (`GET /trading-api/v1/markets/{symbol}/tick`) for pricing.
3. Respect tick size and precision. A price off the tick grid is rejected with
   `6018`; out of range is `3031`. See
   https://docs.exchange.bullish.com/rest/general/price-quantity-precision

## Create the order

`createOrderV2` — `POST /trading-api/v2/orders`.

**Always supply your own `clientOrderId`.** It is the only handle you control, and
it is the only way to answer "did that order land?" after a network failure.

Bullish deduplicates on it — a repeat is *rejected* with `3007` ("Duplicated order
id") or `3023` ("Duplicated order handle"), not replayed. That is at-most-once
protection, not an idempotent retry.

Wait for the acknowledgement carrying the server-generated `orderId` before sending
the next request on the same key. Firing without waiting risks out-of-order
processing and silent failure.

## Reconcile — the step people skip

There is **no `Idempotency-Key` header on this API**, and the nonce is strictly
increasing, so a blind retry either creates a *second* order or fails on the nonce.

On any timeout, 429 or 5xx:

1. Do **not** resend the create.
2. Call `trade-get-order-by-client-order-id-v2`
   (`GET /trading-api/v2/orders/client-order-id/{clientOrderId}`).
3. If it returns an order, the original landed — carry on with that `orderId`.
4. If it 404s, the order did not land. Take a fresh nonce and resubmit with the
   **same** `clientOrderId`.

## Amend and cancel

- `submitAmendmentCommand` — `POST /trading-api/v2/command#amend`
- `submitCancellationCommands` — `POST /trading-api/v2/command#cancellations`

Both are command-entry operations and take the same nonce discipline. `3032` means
the order is already closed or rejected — treat it as terminal, not as a retry.

## Auction markets behave differently

If `auctionEnabled` is true, the phase governs what is allowed:

| Code | Meaning |
|---|---|
| 3083 | Auction order creation disabled in the current phase |
| 3084 | Auction order amendment disabled in the current phase |
| 3085 | Auction order cancellation disabled in the current phase |
| 3086 | GTX order is missing `auctionId` |
| 3087 | `auctionId` not allowed on non-GTX orders |
| 3090 | Auction orders support only MARKET and LIMIT |

Read the phase from `getAuctionBySymbol` before submitting.

## Confirm the fill

`getOrdersV2` for open state, `getOrderByIdV2` for a single order, and `getTrades`
(`GET /trading-api/v1/trades`) for executions. Note the 6xxx codes are lifecycle
states, not errors: `6014` accepted, `6013` partially filled, `6015` filled,
`6005` user cancelled.

## Rate limits

50 requests/second on `/orders` as an independent bucket, 500 requests per 10
seconds per IP, and a 60-second IP block on breach. Watch `x-ratelimit-remaining`
and back off on `x-ratelimit-reset`. See `rate-limits/bullish-rate-limits.yml`.
