# Route Mobile

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Route Mobile Limited is a Mumbai-headquartered cloud communications platform (CPaaS) provider and one of India's largest A2P messaging aggregators, listed on the BSE and NSE and now majority-owned by Belgium's Proximus Group, where it sits alongside BICS and Telesign inside Proximus Global. It sells enterprise messaging (SMS, WhatsApp Business Platform, RCS, Viber, Google Business Messages, Telegram, Instagram), OTP and identity verification, voice and cloud telephony, transactional email through SendClean, URL shortening through Acculync, and a telecom-operator product line (SMSC-as-a-service, the Route Shield SMS firewall, Route Hub, and Instant Virtual Numbers) that puts it on both sides of the carrier relationship — reselling operator connectivity to enterprises while also selling infrastructure back to operators. Its API posture is genuinely self-serve and public: a ReadMe-hosted developer portal at developer.rmlconnect.net documents roughly 108 REST operations across SMS, WhatsApp, RCS, Viber and email, backed by five downloadable OpenAPI 3.0 definitions that are also mirrored in first-party GitHub repositories with Postman collections and Redoc pages. That places Route Mobile firmly in the CPaaS-aggregator half of telecom rather than the partner-gated operator half. On the sector's defining standards question it is thinner than its marketing suggests: nothing in its public documentation references CAMARA, GSMA Open Gateway, Number Verification, SIM Swap, Device Location or CIBA, and its network-API story lives entirely at the parent level, in Proximus Global's Konera aggregation platform announced as "aligned with GSMA's CAMARA standardization initiative" — a press release, not a callable Route Mobile endpoint. Authentication across its live APIs is legacy-CPaaS rather than telco-standard: username and password query parameters for SMS, JWT bearer tokens minted by product-level login endpoints for WhatsApp, RCS and Viber, and owner_id plus token in the request body for email.

**Areas:** Telecommunications · India · CPaaS · Messaging · SMS · A2P Messaging · WhatsApp Business · RCS · Voice · Email · Identity Verification · OTP

## Route Mobile on APIs.io

Everything profiled for Route Mobile is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/route-mobile/](https://apis.io/providers/route-mobile/)** — or go straight to one of the APIs or properties below.

### APIs (34)

- [Route Mobile Enterprise Voice 2.0 API](https://apis.io/apis/route-mobile/route-mobile-enterprise-voice-api/) — Route Mobile's enterprise voice and cloud telephony surface, documented as narrative guides on the developer portal (send message and template management…
- [Route Mobile Account API](https://apis.io/apis/route-mobile/route-mobile-account-api/) — APIs for account management, credit queries, and authentication tokens.
- [Route Mobile Account Management API](https://apis.io/apis/route-mobile/route-mobile-account-management-api/) — Manage your WhatsApp Business profile settings, account details, and profile photo.
- [Route Mobile Accounts API](https://apis.io/apis/route-mobile/route-mobile-accounts-api/) — Retrieve account/user details
- [Route Mobile Authentication API](https://apis.io/apis/route-mobile/route-mobile-authentication-api/) — Authenticate with the Route Mobile WhatsApp Business API to obtain a JWT token for subsequent API calls.
- [Route Mobile Bulk Campaigns API](https://apis.io/apis/route-mobile/route-mobile-bulk-campaigns-api/) — Upload files, create, start, pause, and resume bulk messaging campaigns to reach large audiences.
- [Route Mobile Bulk Upload Campaign API](https://apis.io/apis/route-mobile/route-mobile-bulk-upload-campaign-api-api/) — Upload campaign files and manage bulk RCS messaging campaigns at scale.
- [Route Mobile Callback API](https://apis.io/apis/route-mobile/route-mobile-callback-api-api/) — Webhook receiver endpoints for real-time RCS message delivery and event notifications.
- [Route Mobile Capability Check API](https://apis.io/apis/route-mobile/route-mobile-capability-check-api-api/) — Check and retrieve RCS capability details for phone numbers in bulk.
- [Route Mobile Catalog Management API](https://apis.io/apis/route-mobile/route-mobile-catalog-management-api/) — Create, update, delete, and fetch product feeds and catalog details for WhatsApp Commerce.
- [Route Mobile File Server API](https://apis.io/apis/route-mobile/route-mobile-file-server-api-api/) — Upload media files (images, videos, PDFs) to the RCS file server for use in messages.
- [Route Mobile Integrations API](https://apis.io/apis/route-mobile/route-mobile-integrations-api/) — APIs for third-party platform integrations.
- [Route Mobile Login API](https://apis.io/apis/route-mobile/route-mobile-login-api/) — Authenticate users and obtain JWT tokens for RCS API access.
- [Route Mobile Management API](https://apis.io/apis/route-mobile/route-mobile-management-api-api/) — APIs for managing RCS bot testers, templates, and account configuration.
- [Route Mobile Message Sending API](https://apis.io/apis/route-mobile/route-mobile-message-sending-api/) — APIs for submitting SMS messages.
- [Route Mobile Messages API](https://apis.io/apis/route-mobile/route-mobile-messages-api/) — Send transactional emails and retrieve message info
- [Route Mobile Messaging API](https://apis.io/apis/route-mobile/route-mobile-messaging-api/) — Send template messages (marketing, utility, authentication) and session messages (text, media, interactive, payments, flows) to individual recipients.
- [Route Mobile Opt-in Management API](https://apis.io/apis/route-mobile/route-mobile-opt-in-management-api/) — Store and verify user opt-in and opt-out consent for WhatsApp messaging compliance.
- [Route Mobile OTP API](https://apis.io/apis/route-mobile/route-mobile-otp-api/) — APIs for OTP generation and verification.
- [Route Mobile Payment API](https://apis.io/apis/route-mobile/route-mobile-payment-api-api/) — Send RCS payment request messages to customers.
- [Route Mobile RCS Messages API](https://apis.io/apis/route-mobile/route-mobile-rcs-messages-api-api/) — Send RCS notification, session, and India template messages including text, media, rich cards, carousels, and interactive suggestions.
- [Route Mobile RCS Messages Request API](https://apis.io/apis/route-mobile/route-mobile-rcs-messages-request-api-api/) — APIs for managing RCS message requests and retrieving request status.
- [Route Mobile RCS Optin API](https://apis.io/apis/route-mobile/route-mobile-rcs-optin-api-api/) — The RCS Optin API API from Route Mobile — 1 operation(s) for rcs optin api.
- [Route Mobile RCS Template API](https://apis.io/apis/route-mobile/route-mobile-rcs-template-api-api/) — The RCS Template API API from Route Mobile — 3 operation(s) for rcs template api.
- [Route Mobile Reports API](https://apis.io/apis/route-mobile/route-mobile-reports-api/) — Generate, download, and query messaging reports including delivery stats, campaign metrics, opt-in data, and template usage counts.
- [Route Mobile Sending Domains API](https://apis.io/apis/route-mobile/route-mobile-sending-domains-api/) — Add, verify, list, and delete sending domains
- [Route Mobile SMTP Users API](https://apis.io/apis/route-mobile/route-mobile-smtp-users-api/) — Manage SMTP sub-users (create, edit, reset password, list)
- [Route Mobile Tracking Domains API](https://apis.io/apis/route-mobile/route-mobile-tracking-domains-api/) — Add, check, list, and delete tracking domains
- [Route Mobile Viber Bulk Messaging API](https://apis.io/apis/route-mobile/route-mobile-viber-bulk-messaging-api-api/) — Send bulk campaign messages to multiple Viber recipients at once using a file_code from the Campaign File Upload API. Supports all message types including…
- [Route Mobile Viber Business Messaging API](https://apis.io/apis/route-mobile/route-mobile-viber-business-messaging-api-api/) — Send single messages to individual Viber users including text, images, videos, files, OTP verification, and interactive buttons. Also manage campaign file…
- [Route Mobile Viber Client Callback API](https://apis.io/apis/route-mobile/route-mobile-viber-client-callback-api-api/) — Receive real-time webhook notifications for incoming messages and delivery reports from the Viber platform. Configure your callback URL in the webhook settings.
- [Route Mobile Viber Login API](https://apis.io/apis/route-mobile/route-mobile-viber-login-api/) — Authenticate and obtain a JWT token to access the Viber Business Messaging APIs. Tokens are valid for one hour by default.
- [Route Mobile Viber Reports API](https://apis.io/apis/route-mobile/route-mobile-viber-reports-api-api/) — Access delivery reports, campaign performance metrics, summary dashboards, and message-level tabular data. Create and download detailed CSV reports. Manage…
- [Route Mobile Webhooks API](https://apis.io/apis/route-mobile/route-mobile-webhooks-api/) — Configure event webhooks for email delivery events

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Route Mobile Webhooks](https://apis.io/asyncapis/route-mobile/route-mobile-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [route-mobile](https://apis.io/servers/route-mobile/route-mobile/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Route Mobile Agentic Access](https://apis.io/agentic-access/route-mobile/route-mobile-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [Route Mobile Rich Communication Services (RCS) API Documentation](https://apis.io/collections/route-mobile/open-route-mobile-rcs/)
- [SendClean Email API](https://apis.io/collections/route-mobile/open-route-mobile-sendclean-email/)
- [Route Mobile SMS APIs](https://apis.io/collections/route-mobile/open-route-mobile-sms/)
- [Route Mobile Viber OpenAPI Specification](https://apis.io/collections/route-mobile/open-route-mobile-viber/)
- [Route Mobile WhatsApp Business API](https://apis.io/collections/route-mobile/open-route-mobile-whatsapp-business/)

#### Overlays (5)

OpenAPI overlays, including conversational phrasing for each operation.

- [Route Mobile Rcs Overlay](https://apis.io/overlays/route-mobile/route-mobile-rcs-overlay/)
- [Route Mobile Sendclean Email Overlay](https://apis.io/overlays/route-mobile/route-mobile-sendclean-email-overlay/)
- [Route Mobile Sms Overlay](https://apis.io/overlays/route-mobile/route-mobile-sms-overlay/)
- [Route Mobile Viber Overlay](https://apis.io/overlays/route-mobile/route-mobile-viber-overlay/)
- [Route Mobile Whatsapp Business Overlay](https://apis.io/overlays/route-mobile/route-mobile-whatsapp-business-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Route Mobile Authentication](https://apis.io/security/route-mobile/route-mobile-authentication/)
- [Route Mobile Domain Security](https://apis.io/security/route-mobile/route-mobile-domain-security/)

#### Rate limits (1)

Published request limits.

- [Route Mobile Rate Limits](https://apis.io/rate-limits/route-mobile/route-mobile-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://routemobile.com/)
- [Documentation](https://developer.rmlconnect.net/)
- [Getting started](https://developer.rmlconnect.net/route-mobile-project/docs/getting-started-on-route-mobile-panel)
- [Sign up](https://routemobile.com/contact-us/)
- [Support](https://routemobile.com/contact-us/)
- [Blog](https://routemobile.com/blogs/)
- [Compliance](https://routemobile.com/company-profile/)
- [Terms of service](https://routemobile.com/terms-condition/)
- [Privacy policy](https://routemobile.com/privacy-policy/)
- [GitHub](https://github.com/routemobile)

## API Evangelist rating

**Kin Score 51.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 59.8 |
| Contract governance | 18.2 |
| Operational transparency | 42.1 |
| Developer ergonomics | 56.5 |
| Access clarity | 42.1 |

**Agent readiness 37.6** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.2** — Telecommunications

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/route-mobile/](https://apis.io/providers/route-mobile/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Route Mobile: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/route-mobile/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
