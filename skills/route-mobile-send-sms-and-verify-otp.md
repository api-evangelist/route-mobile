---
name: Send SMS and run an OTP verification with Route Mobile
description: >-
  Submit an A2P SMS over the Route Mobile SGN gateway, then generate and verify a one-time
  passcode, handling the platform's plain-text numeric response codes and its no-retry policy.
api: openapi/route-mobile-sms.yml
base_url: https://api.rmlconnect.net
operations:
  - checkCredits
  - sendSmsSecured
  - generateOtp
  - verifyOtp
  - scheduleSms
generated: '2026-07-25'
method: generated
---

# Send SMS and run an OTP verification with Route Mobile

The Route Mobile SMS API is the oldest surface on the platform and behaves unlike the rest of
it. Every operation is an HTTP **GET** against `https://api.rmlconnect.net`, credentials travel
as **query parameters**, and the response is **plain text**, not JSON.

## 1. Authenticate

There is no login call and no token. Every request carries:

- `username` — your Route Mobile account username
- `password` — your account password

over HTTPS on port 443 (the spec also lists port 8443, and a plain-HTTP host marked
"legacy only" — never use it). See `authentication/route-mobile-authentication.yml`.

## 2. Check credit before a run (`checkCredits`)

`GET /CreditCheck/checkcredits` returns the account balance. Do this before any batch:
credit exhaustion aborts a batch mid-flight and there is no idempotency key to make a
re-run safe.

## 3. Submit the message (`sendSmsSecured`)

`GET /bulksms/bulksms` with `username`, `password`, `type`, `dlr`, `destination`, `source`
and `message`. Comma-separate destinations for a batch.

The response is a pipe-delimited string, not JSON:

```
1701|<CELL_NO>|<MESSAGE_ID>
```

For a batch you get one comma-separated tuple per destination. Parse on `|` and `,`.

To schedule instead of sending now, use `scheduleSms` (`GET /bulksms/schedulemsg`), which
takes the send time plus a GMT offset.

## 4. Read the platform code, and obey the retry policy

| Code | Meaning | What to do |
|---|---|---|
| 1701 | Success | continue |
| 1702–1708 | Bad request / invalid parameter, destination or Sender ID | fix and resubmit; do not blind-retry |
| 1709 | User validation failed | **the only code Route Mobile documents as retryable** |
| 1710 | Internal error | do not retry; contact support |
| 1025 | Insufficient credit | top up; the batch aborted at `1025|<last_destination>` |
| 1715 | Response timeout | **do not re-submit the same message** — delivery state is indeterminate |

There is no `Idempotency-Key` on this API. A retry on 1715 risks a duplicate send and a
duplicate charge; record the destination and reconcile from the delivery receipt instead.

## 5. OTP flow (`generateOtp` → `verifyOtp`)

- `GET /OtpApi/otpgenerate` generates and sends the passcode to the destination.
- `GET /OtpApi/checkotp` verifies the code the user typed back.

Both return the same numeric-prefixed plain-text envelope, so reuse the parser and the code
table above. Treat any non-1701 verify response as a failed verification, not as a transport
error.

## Related artifacts

- `errors/route-mobile-error-codes.yml` — the full 17xx registry and retry policy
- `conventions/route-mobile-conventions.yml` — per-product auth, pagination and error shapes
- `rate-limits/route-mobile-rate-limits.yml` — no published numeric SMS limit; 429 semantics
