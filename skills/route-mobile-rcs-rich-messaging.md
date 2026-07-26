---
name: Launch an RCS rich message campaign with Route Mobile
description: >-
  Authenticate, check handset RCS capability, register a tester, upload media, create a
  template and send single or bulk rich messages, then handle inbound callbacks.
api: openapi/route-mobile-rcs.yml
base_url: https://apis.rmlconnect.net
operations:
  - loginApi2
  - checkBulkCapability
  - getCapabilityDetails
  - ManagementRCS
  - managementRCS
  - fileUploadRCS
  - createTemplateRCS
  - textTemplate
  - bulkCampaignUploadRCS
  - post-callback
generated: '2026-07-25'
method: generated
---

# Launch an RCS rich message campaign with Route Mobile

RCS upgrades SMS with branding, rich cards, carousels and suggested replies — but only for
handsets that actually support it, so capability checking is a first-class step rather than an
optimisation.

## 1. Get a JWT (`loginApi2`)

`POST /auth/v1/login/` returns a JWT carried in the `Authorization` header on every later
call. The RCS spec declares this as an apiKey-in-header scheme; the value is the token from
login.

## 2. Check capability before you spend (`checkBulkCapability`, `getCapabilityDetails`)

- `POST /v1/capabilityCheck/checkBulkCapability` submits numbers for RCS capability checking.
- `GET /v1/capabilityCheck/getCapabilityDetails` retrieves results for a date range, with an
  optional status filter and paging.

Numbers that come back incapable must fall back to SMS — Route Mobile also exposes
`revokeWithSmsFallback` (`DELETE /rcs/v2/revoke_message`) for revoking an undelivered RCS
message with SMS fallback.

## 3. Register a tester before launch (`ManagementRCS`, `managementRCS`)

`POST /rcs/management/v1/add_tester` allowlists a handset so an unlaunched agent can be
exercised end to end; `GET /rcs/management/v1/get_testers` lists them. This is the closest
thing Route Mobile has to a sandbox — there is no test host and no magic test number.

## 4. Upload media and create the template

- `POST /rcs/file_server/v2/uploadfile` (`fileUploadRCS`) puts media on the RCS file server.
- `POST /rcs-template-apis/api/v1/template/template` (`createTemplateRCS`) creates a template;
  `getTemplateRCS`, `updateTemplateRCS`, `deleteTemplateRCS` and `getTemplateStatusRCS` manage
  it. Template listing pages with `page_no` + `limit`.

## 5. Send (`textTemplate`, `bulkCampaignUploadRCS`)

- `POST /rcs/v1/message` sends a single rich message — text, rich card, or carousel, each with
  suggested replies/actions.
- `POST /rcs/v1/bulk_message` uploads a bulk campaign.
- `POST /rcs/v1/typing_event` and `POST /rcs/v1/mark_read` drive the conversational UX.
- `POST /payments/v1/send_bill` sends an RCS bill/payment request (`sendBillToUserRcs`).

Successful submissions return **202 Accepted** — delivery is confirmed on the callback, not in
the response.

## 6. Handle the callback (`post-callback`)

`POST /callback` is the inbound contract. Payloads carry `bot_name`, `event_type`,
`request_id`, `session_id`, `timestamp`, `user_contact` and, for media, `media_uri` /
`media_type` / `media_size`. Event types include `text_message`, `media_message`,
`location_message`, suggested action/reply responses, and sent/delivered/read/failed status
updates. Route Mobile will present an access token in the `Authorization` header if your
endpoint requires one.

## Errors and limits

400 validation, 401 expired JWT, 403 restricted, 404, 429 rate limit, 500 platform error —
retry only with exponential backoff on 429/500, never on 4xx. No numeric RCS rate limit is
published. See `errors/route-mobile-error-codes.yml` and
`rate-limits/route-mobile-rate-limits.yml`.

## Related artifacts

- `sandbox/route-mobile-sandbox.yml` — tester enrolment and capability check as the test path
- `asyncapi/route-mobile-webhooks.yml` — the RCS callback event catalog
