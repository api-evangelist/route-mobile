---
name: Send transactional email and wire event webhooks with SendClean
description: >-
  Create an SMTP user, register and verify a sending domain, send a transactional or template
  email with a correlation id, register a signed event webhook, and reconcile delivery.
api: openapi/route-mobile-sendclean-email.yml
base_url: https://api.sendclean.net/v1.0
operations:
  - addSmtpUser
  - addSendingDomain
  - checkSendingDomain
  - verifySendingDomain
  - addTrackingDomain
  - sendMail
  - sendTemplate
  - getMessageInfo
  - addWebhook
  - keyResetWebhook
  - getUserDetails
generated: '2026-07-25'
method: generated
---

# Send transactional email and wire event webhooks with SendClean

SendClean is Route Mobile's email product and does not follow the conventions of the messaging
APIs. Every operation is an HTTP **POST** to `https://api.sendclean.net/v1.0`, and
authentication travels **inside the JSON body**, not in a header.

## 1. Authenticate

Every request body carries:

```json
{ "owner_id": "<your account id>", "token": "<your api token>" }
```

There is no Authorization header and no login/refresh cycle. The one GET operation,
`sendTemplateHTTPGet`, takes the same pair as URL-encoded query parameters — designed for IVR
webhooks that cannot POST JSON.

**Every response is HTTP 200.** Branch on the body's `status` field (`success` / `error`),
never on the HTTP status code. Errors carry `{status, code, name, message}` where `name` is
`ValidationError`, `GeneralError` or `AuthenticationError`.

## 2. Provision sending identity

- `POST /settings/addSmtp` (`addSmtpUser`) creates an SMTP sub-user with `hourly_limit`,
  `total_limit` and status; `editSmtpUser`, `resetSmtpPassword` and `listSmtpUsers` manage it.
- `POST /settings/addSendingDomain` registers the domain you will send from.
- `POST /settings/checkSendingDomain` verifies DKIM and SPF records;
  `verifySendingDomain` runs the email-based verification.
- `POST /settings/addTrackingDomain` + `checkTrackingDomain` set up the click/open tracking
  CNAME.

Do not send until `checkSendingDomain` reports DKIM and SPF valid — this is also the only
pre-send validation available, since there is no sandbox.

## 3. Send (`sendMail`, `sendTemplate`)

- `POST /messages/sendMail` sends a transactional email.
- `POST /messages/sendTemplate` sends from a saved template.

Set the `X-Unique-Id` header to your own correlation id (e.g. `order-12345`). This is the key
you will use later to retrieve delivery and engagement data — SendClean has no other
caller-supplied metadata channel.

## 4. Reconcile (`getMessageInfo`)

`POST /messages/getMessageInfo` returns delivery status, opens and clicks for messages
matching an `X-Unique-Id`, paged with `skip_page` (a record offset, not a cursor).

## 5. Register a signed webhook (`addWebhook`, `keyResetWebhook`)

`POST /settings/addWebhook` registers an HTTPS endpoint for the event set
`send`, `open`, `click`, `soft_bounce`, `hard_bounce`, `spam`, with an optional
`store_log: Enable|Disable`.

Two rules the docs are explicit about:

1. **Validation handshake** — your URL must respond with the exact string
   `God bless you, SendClean` or registration fails.
2. **Signature** — SendClean signs each POST with HMAC-SHA1 in the
   `X-SendCleanTES-SIGNATURE` header. `keyResetWebhook` rotates the key and SendClean starts
   using the new one immediately, so return a non-200 for any batch that fails verification
   (it will be retried after you have picked up the new key) rather than dropping it.

`listWebhooks`, `getWebhookInfo`, `editWebhook` and `deleteWebhook` complete the surface.

## 6. Stay inside the quota (`getUserDetails`)

`POST /accounts/userDetails` returns account state, sending limits and reputation. Published
API defaults are 60 requests/minute, 3,600/hour and 50,000/day per SMTP user; exceeding them
returns HTTP 429 and the docs prescribe exponential backoff. Email volume limits are
configured per SMTP user (`hourly_limit`, `total_limit`).

## Related artifacts

- `rate-limits/route-mobile-rate-limits.yml` — the published SendClean quotas
- `asyncapi/route-mobile-webhooks.yml` — the email event catalog and signature scheme
- `errors/route-mobile-error-codes.yml` — the SendClean error envelope
