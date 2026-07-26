---
name: Run a Viber Business Messages campaign and pull reports with Route Mobile
description: >-
  Log in, upload a campaign file, send single or bulk Viber business messages, then generate,
  poll and download the delivery reports.
api: openapi/route-mobile-viber.yml
base_url: https://apis.rmlconnect.net
operations:
  - loginApi2
  - campaignFileUpload
  - singleVideoText
  - campaignVideoText
  - sendBulkMessages
  - listViberTemplates
  - addViberTemplate
  - getSummaryCards
  - getCampaignReport
  - createReport
  - fetchReports
  - downloadReport
  - viberClientCallback
generated: '2026-07-25'
method: generated
---

# Run a Viber Business Messages campaign and pull reports with Route Mobile

## 1. Get a JWT (`loginApi2`)

`POST /auth/v1/login/` on `https://apis.rmlconnect.net` returns the JWT you carry in the
`Authorization` header on every later call.

## 2. Prepare the content

- `GET /viber-reports/api/v2/viber_templates` (`listViberTemplates`) lists templates;
  `POST` the same path (`addViberTemplate`) adds one.
- `POST /vbs/api/v2/upload` (`campaignFileUpload`) uploads the campaign recipient file.

## 3. Send

- `POST /vbs/api/v2/send` (`singleVideoText`) — a single message: text, image, video, file or
  template.
- `POST /vbs/api/v2/manage-campaign` (`campaignVideoText`) — campaign send.
- `POST /vbs/api/v3/send_bulk` (`sendBulkMessages`) — the v3 bulk path. Note that v2 and v3
  run concurrently; pick one and stay on it.

Sends return **202 Accepted**; delivery outcome arrives on the callback.

## 4. Report

Two reporting styles coexist:

*Synchronous cards and graphs*
- `getSummaryCards`, `getMediaCards`, `getGraphReport`, `getCampaignReport`,
  `getDailyTabularReport` — all GET, all paged by date range (with timezone, message-type and
  service-type filters on the tabular report).

*Asynchronous file reports*
1. `POST /viber-report-creator/v1/create_report` (`createReport`) triggers generation.
2. `GET /viber-report-creator/v1/fetch_reports` (`fetchReports`) polls until the record's
   status is `completed`.
3. `GET /viber-report-creator/v1/download/{file_name}` (`downloadReport`) fetches the file
   using the `file_path` from step 2.

Do not poll tightly — 429 is declared on every reporting operation and no numeric limit or
`Retry-After` header is published.

## 5. Consume the callback (`viberClientCallback`)

`POST /callback` delivers two event families, distinguished by `service_type`:

- `two_way/session` — inbound text and image/video messages, carrying `phone_number`, `time`,
  `message.text` or `message.media`/`file_name`, `message.tracking_data`, `request_id`.
- `dlr` — delivery reports with `message_status` of `Sent`, `delivered`, `seen` or `expired`,
  plus `message_time`, `phone_number`, `session_id` and `request_id`.

Correlate on `request_id`; it is the only identifier that spans the send and the receipt.
The callback is unsigned — treat the endpoint URL as a secret.

## Related artifacts

- `asyncapi/route-mobile-webhooks.yml` — the Viber event catalog
- `conventions/route-mobile-conventions.yml` — pagination and versioning per product
- `errors/route-mobile-error-codes.yml` — the shared HTTP status semantics
