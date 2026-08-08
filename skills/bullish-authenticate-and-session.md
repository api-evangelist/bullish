---
name: Authenticate to the Bullish Trading API and hold a session
description: >-
  Mint a Bullish JWT by signing a login request with an ECDSA R1 or HMAC API key,
  keep the nonce sequence valid across the 24-hour token life, and log out cleanly.
  This is the prerequisite for every other Bullish skill.
api: openapi/bullish-trading-api-openapi.yml
operations:
  - getNonce
  - loginUserV2
  - loginUserHmac
  - logoutUser
  - getExchangeTime
  - getTradingAccounts
generated: '2026-08-08'
method: generated
source: https://docs.exchange.bullish.com/rest/authentication
---

# Authenticate to the Bullish Trading API

Bullish does not use OAuth. You sign a login payload with your own key and exchange
it for a 24-hour JWT bearer token. Get this wrong and every other call returns 401.

## Pick the right credential class first

There are two, and they are **not** interchangeable:

| Credential | Login | Reaches |
|---|---|---|
| ECDSA R1 API key (prime256v1 / secp256r1 / P-256, SHA256) | `loginUserV2` — `POST /trading-api/v2/users/login` | trading **and** custody |
| HMAC API key (shared secret) | `loginUserHmac` — `GET /trading-api/v1/users/hmac/login` | trading **only** |

If you plan to touch custody at all, you must use an ECDSA key. A JWT minted from an
HMAC key returns **403** on the custody surface — that 403 is a credential-class
error, not a permissions error, and no amount of retrying fixes it.

The legacy "Bullish API Key" credential was deprecated on 2024-06-28 and no longer works.

## Steps

1. **Sync to exchange time.** Call `getExchangeTime` (`GET /trading-api/v1/time`).
   `BX-TIMESTAMP` is milliseconds since epoch and is validated against a window —
   a skewed clock produces OTC error `9014` and login failures.

2. **Get a nonce.** Call `getNonce` (`GET /trading-api/v1/nonce`). `BX-NONCE` is a
   64-bit unsigned integer that must be **unique and increasing** for your key. The
   exchange tracks the highest nonce it has seen and rejects anything lower
   (`statusReasonCode 2035`, "Invalid nonce"; OTC `9015`).

3. **Sign and log in.** Build the canonical message, sign it, and send:

   - `BX-TIMESTAMP` — milliseconds since epoch
   - `BX-NONCE` — unique increasing integer
   - `BX-PUBLIC-KEY` — your API public key
   - `BX-SIGNATURE` — the signature

   Do not hand-roll the signature. Use the first-party signer for your language —
   `js-signer` on npm, or the Python / Java / C++ signers on
   `github.com/bullish-exchange` (see `packages/bullish-packages.yml`).

   Call `loginUserV2` for ECDSA or `loginUserHmac` for HMAC.

4. **Hold the token.** Send `Authorization: Bearer <JWT_TOKEN>` on every private
   call. The token is valid for **24 hours**. Re-login before expiry rather than
   after a 401 storm.

5. **Confirm the account context.** Call `getTradingAccounts`
   (`GET /trading-api/v1/accounts/trading-accounts`). A valid `tradingAccountId`
   begins with `111`. This response also carries the rate-limit token you can put in
   `BX-RATELIMIT-TOKEN` to move off the default 50 msgs/sec tier.

6. **Log out** with `logoutUser` (`GET /trading-api/v1/users/logout`) when done.

## Nonce ordering — the trap

By default the nonce must be **strictly increasing**, which means you must wait for
each acknowledgement before firing the next request. If you need concurrency, send
`BX-NONCE-WINDOW-ENABLED: true`, which relaxes the rule to *uniqueness within a
window of 100* from the highest nonce used. Uniqueness still forbids replay — see
`conventions/bullish-conventions.yml`.

## Errors to expect

| Code | Meaning | Fix |
|---|---|---|
| 401 | Missing or invalid credentials | Re-mint the JWT |
| 403 | Wrong credential class or wrong account role | Use an ECDSA key for custody |
| 2035 | Invalid nonce | Re-read the nonce; never reuse or go backwards |
| 9011/9012/9013 | Missing `BX-SIGNATURE` / `BX-NONCE` / `BX-TIMESTAMP` | Add the header |
| 9014 | Timestamp unparseable or out of range | Re-sync to `getExchangeTime` |

Full registry: `errors/bullish-error-codes.yml`.
