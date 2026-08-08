---
name: Pull Bullish market data and subscribe to the live streams
description: >-
  Read the anonymous Bullish market-data surface over REST — markets, assets, order
  books, ticks, candles, index prices, option ladders, funding rates and auctions —
  then move to the WebSocket feeds for real-time updates.
api: openapi/bullish-trading-api-openapi.yml
operations:
  - getMarkets
  - getMarketBySymbol
  - getMarketOrderBook
  - getMarketTick
  - getMarketCandles
  - getLatestMarketTrades
  - getAssets
  - getAssetBySymbol
  - getIndexPrices
  - getIndexPriceBySymbol
  - getOptionLadder
  - getOptionLadderBySymbol
  - getVolGrids
  - getVolGridByAsset
  - getFundingRateHistory
  - getHistoricalMarketTrades
  - getHistoricalOptionTrades
  - getAuctionBySymbol
  - getAuctionNoii
  - getHistoricalAuctionResults
  - getExchangeTime
generated: '2026-08-08'
method: generated
source: openapi/bullish-trading-api-openapi.yml
---

# Pull Bullish market data and subscribe to the live streams

**No credentials required.** Everything in this skill is anonymous. Do not mint a
JWT to read market data.

## Reference data

- `getMarkets` — `GET /trading-api/v1/markets`. Start here. Carries `marketId`,
  `symbol`, `baseAssetId`, `quoteAssetId`, `feeGroupId`, `auctionEnabled` and
  `auctionPriceCollar`.
- `getMarketBySymbol` — `GET /trading-api/v1/markets/{symbol}`
- `getAssets` / `getAssetBySymbol` — `GET /trading-api/v1/assets[/{symbol}]`
- `getExchangeTime` — `GET /trading-api/v1/time`

Filter out the test instruments — market `DEMOONEDEMOTWO`, assets `DEMOONE` and
`DEMOTWO` exist for internal testing and Bullish tells clients to ignore them.

## Prices and book

- `getMarketOrderBook` — `GET /trading-api/v1/markets/{symbol}/orderbook/hybrid`
- `getMarketTick` — `GET /trading-api/v1/markets/{symbol}/tick`
- `getMarketCandles` — `GET /trading-api/v1/markets/{symbol}/candle` (OHLCV)
- `getLatestMarketTrades` — `GET /trading-api/v1/markets/{symbol}/trades`
- `getIndexPrices` / `getIndexPriceBySymbol` — `GET /trading-api/v1/index-prices[/{assetSymbol}]`

## Derivatives surface

- `getOptionLadder` / `getOptionLadderBySymbol` — `GET /trading-api/v1/option-ladder[/{symbol}]`
- `getVolGrids` / `getVolGridByAsset` — volatility grids
- `getFundingRateHistory` — `GET /trading-api/v1/history/markets/{symbol}/funding-rate`
- `getHistoricalOptionTrades` — `GET /trading-api/v1/history/option-trades`
- `get-expiry-prices--symbol` — `GET /trading-api/v1/expiry-prices/{symbol}`

## Auctions

- `getAuctionBySymbol` — `GET /trading-api/v1/markets/{symbol}/auctions`
- `getAuctionNoii` — `GET /trading-api/v1/markets/{symbol}/auctions/noii`
  (net order imbalance indicator)
- `getHistoricalAuctionResults` — `GET /trading-api/v1/history/markets/{symbol}/auctions`

## History and paging

History endpoints are cursor-paginated. Send `_pageSize` (5, 25, 50 or 100 —
default 25) and `_metaData=true` so the response carries `links.next` and
`links.previous`, then follow `links.next` until it is absent. Do not construct
cursors yourself.

## Move to the streams

Polling the REST book is the wrong shape for anything live. Bullish publishes six
AsyncAPI 3.0.0 documents in this repo under `asyncapi/`:

| Feed | Document |
|---|---|
| L1/L2 multi-order book | `bullish-ws-orderbook-asyncapi.yml` |
| Anonymous trades (batched) | `bullish-ws-trades-asyncapi.yml` |
| Anonymous ticks | `bullish-ws-ticks-asyncapi.yml` |
| Auction feed | `bullish-ws-auction-asyncapi.yml` |
| Index data | `bullish-ws-index-data-asyncapi.yml` |
| Private account data | `bullish-ws-private-data-asyncapi.yml` |

Each declares six named servers — `prod-public`, `prod-registered`, `prod-direct`
and the three SIMNEXT equivalents. Subscribe with the documented subscribe message,
handle the subscribe-ack / subscribe-nack pair, and keep the connection alive with
the keepalive ping/pong operations. Only the private feed needs authentication
(https://docs.exchange.bullish.com/websocket/protocol/authentication).

## Rate limits

Public endpoint limits are not published — Bullish asks clients to contact support.
The per-IP ceiling still applies: 500 requests per 10 seconds, then a 60-second
block. Watch `x-ratelimit-remaining`.
