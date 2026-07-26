---
name: Send a WhatsApp template or session message with Route Mobile
description: >-
  Log in for a JWT, confirm or create an approved template, check opt-in, send the template or
  session message, and receive delivery and template-status events on the client callback.
api: openapi/route-mobile-whatsapp-business.yml
base_url: https://apis.rmlconnect.net
operations:
  - loginApi
  - checkOptin
  - createOptin
  - viewTemplateMessage
  - createTemplate
  - sendSessionMessageApi
  - whatsappClientCallback
generated: '2026-07-25'
method: generated
---

# Send a WhatsApp template or session message with Route Mobile

Route Mobile is a Meta Business Solution Provider; this API mirrors WhatsApp Business Platform
semantics (approved templates, the 24-hour session window, Meta error codes) behind Route
Mobile's own endpoints on `https://apis.rmlconnect.net`.

## 1. Get a JWT (`loginApi`)

`POST /auth/v1/login/` with your account credentials returns a JWT. Send it as
`Authorization: Bearer <token>` on every later call. **Tokens expire after one hour by
default** — refresh on 401 rather than on a timer, and never cache a token across processes
without an expiry check.

## 2. Respect opt-in (`checkOptin`, `createOptin`)

- `GET /wbo/v2/optin/check` tells you whether the number is opted in.
- `POST /wbo/v2/optin/store` records an opt-in (`POST /wbo/v2/optinout/store` records both
  opt-in and opt-out).

Do not send to a number that has not opted in — WhatsApp policy enforcement arrives back as a
callback strike, and repeated abuse returns HTTP 403 ("account restricted due to Direct Send
abuse strikes").

## 3. Have an approved template (`viewTemplateMessage`, `createTemplate`)

- `GET /wba/templates` lists templates and their approval status.
- `POST /wba/template/create` submits a new one; `PATCH /wba/template/update` edits and
  `DELETE /wba/template/` removes.

Approval is asynchronous and lives with Meta. Template lifecycle transitions (Approved,
Paused, Disabled, Deleted) arrive on the callback channel, not as an API response — see
`asyncapi/route-mobile-webhooks.yml`.

## 4. Send (`sendSessionMessageApi`)

`POST /wba/v1/messages` sends both template messages and free-form session messages. Outside
the 24-hour customer-service window only an approved template will go through; a session
attempt returns a re-engagement error (code 470 / Meta 131047).

Watch the payload constraints the docs publish — text over 1024 chars, button title over 20
chars, more than 3 buttons, or header/footer over 60 chars all return HTTP 400. Semantically
invalid content (unsupported media type, malformed phone number) returns 422.

Media messages need an id first: `POST /wba/media/v1/get-media-id` or
`POST /wba/templates/media-id`.

## 5. Consume the callback (`whatsappClientCallback`)

`POST /callbacks` is the client callback contract: incoming messages, commerce/cart events,
sent/delivered/read/failed reports, and template status logs. **Route Mobile does not sign
these callbacks** — treat the URL as a secret, require your own bearer token on the endpoint,
and never trust the payload as authenticated input.

## Error handling

Route Mobile codes (400–1026, 2000–2013) and raw Meta Graph codes (0, 3, 4, 10, 190, 80007,
13xxxx) both appear on the callback channel. Key ones: 429/130429 rate limit, 131048 spam
rate limit, 131056 business/consumer pair limit, 190 expired access token, 2001 template
missing, 2000 template parameter count mismatch. Full table:
`errors/route-mobile-error-codes.yml`.

## Related artifacts

- `conventions/route-mobile-conventions.yml` — auth, versioning, error envelopes
- `asyncapi/route-mobile-webhooks.yml` — the full event catalog
- `sandbox/route-mobile-sandbox.yml` — there is no test mode; sends are live
