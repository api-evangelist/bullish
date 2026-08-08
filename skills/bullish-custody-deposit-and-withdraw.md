---
name: Deposit to and withdraw from Bullish custody
description: >-
  Fetch deposit instructions, check withdrawal limits, and initiate a crypto or
  fiat withdrawal from Bullish qualified custody. Requires an ECDSA credential and
  a whitelisted destination; withdrawals are irreversible.
api: openapi/bullish-trading-api-openapi.yml
operations:
  - getCryptoDepositInstructions
  - getFiatDepositInstructions
  - getCryptoWithdrawalInstructions
  - getFiatWithdrawalInstructions
  - getCustodyWithdrawalLimits
  - createCustodyWithdrawal
  - custody-delete-withdrawal-instructions
  - getCustodyTransactionHistory
  - custody-initiate-self-hosted-verification
  - custody-get-self-hosted-verifications
generated: '2026-08-08'
method: generated
source: openapi/bullish-trading-api-openapi.yml
---

# Deposit to and withdraw from Bullish custody

**This skill moves real assets and the moves are irreversible. A human must approve
every withdrawal. Do not automate `createCustodyWithdrawal` end to end.**

## Credential requirement

Custody is reachable **only** with a JWT minted from an **ECDSA R1** API key. An
HMAC-derived token returns 403 on every operation below. See
`bullish-authenticate-and-session.md`.

## Deposit

1. `getCryptoDepositInstructions` —
   `GET /trading-api/v1/wallets/deposit-instructions/crypto/{symbol}`
2. `getFiatDepositInstructions` —
   `GET /trading-api/v1/wallets/deposit-instructions/fiat/{symbol}`

Use the returned address or bank details verbatim. Allocation can fail with `8316`
("Unable to allocate deposit address"); an unsupported asset is `8313`.

## Withdraw

1. **Check the limit.** `getCustodyWithdrawalLimits` —
   `GET /trading-api/v1/wallets/limits/{symbol}`.
2. **Resolve the destination.** `getCryptoWithdrawalInstructions` —
   `GET /trading-api/v1/wallets/withdrawal-instructions/crypto/{symbol}` (or the
   fiat equivalent). Destinations are **whitelisted** — you cannot invent one.
   - `8336` — destination not whitelisted
   - `8335` — destination does not belong to this user
   - `8310` — cannot find withdrawal destination
   - `8320` — address failed validation
   - `8317` — SWIFT code on the restricted list (fiat)
3. **Get human approval.** Present symbol, amount, destination and network to a
   person and wait for an explicit yes.
4. **Initiate.** `createCustodyWithdrawal` — `POST /trading-api/v1/wallets/withdrawal`.
   - `8322` — bad withdrawal amount
   - `8332` — bad network specified
   - `8319` — custody operation has been disabled
5. **Confirm.** `getCustodyTransactionHistory` —
   `GET /trading-api/v1/wallets/transactions`.

Destinations can be removed with `custody-delete-withdrawal-instructions` —
`DELETE /trading-api/v1/wallets/withdrawal-instructions/{destinationId}`.

## Self-hosted wallet verification

Regulated jurisdictions require proof of control over a self-hosted destination:

- `custody-initiate-self-hosted-verification` —
  `POST /trading-api/v1/wallets/self-hosted/initiate`
- `custody-get-self-hosted-verifications` —
  `GET /trading-api/v1/wallets/self-hosted/verification-attempts`

Run the verification and poll for the result before attempting a withdrawal to that
destination.

## Retry discipline

There is no idempotency key on this API. If `createCustodyWithdrawal` times out, do
**not** resend it. Call `getCustodyTransactionHistory` and establish whether the
withdrawal exists before doing anything else. A duplicated withdrawal is not
recoverable.

Full code registry: `errors/bullish-error-codes.yml` (custody block, 8301–8499).
