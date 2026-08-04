# Route Mobile (route-mobile)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Route Mobile Limited is a Mumbai-headquartered cloud communications platform (CPaaS) provider and one of India's largest A2P messaging aggregators, listed on the BSE and NSE and now majority-owned by Belgium's Proximus Group, where it sits alongside BICS and Telesign inside Proximus Global. It sells enterprise messaging (SMS, WhatsApp Business Platform, RCS, Viber, Google Business Messages, Telegram, Instagram), OTP and identity verification, voice and cloud telephony, transactional email through SendClean, URL shortening through Acculync, and a telecom-operator product line (SMSC-as-a-service, the Route Shield SMS firewall, Route Hub, and Instant Virtual Numbers) that puts it on both sides of the carrier relationship.

Its API posture is genuinely self-serve and public. A ReadMe-hosted developer portal at [developer.rmlconnect.net](https://developer.rmlconnect.net/) documents roughly 108 REST operations across five product families, backed by five downloadable OpenAPI 3.0 definitions — all harvested into `openapi/` here — and mirrored with Postman collections in first-party GitHub repositories. That places Route Mobile firmly in the CPaaS-aggregator half of telecom rather than the partner-gated mobile-operator half.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/route-mobile/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/route-mobile/refs/heads/main/apis.yml)

## CAMARA and GSMA Open Gateway

Telecom is the only sector with a live, multi-operator, globally coordinated API standardisation programme — CAMARA under the Linux Foundation, with GSMA Open Gateway as the operator commitment layer. Route Mobile's position on it is worth stating plainly:

- **No CAMARA implementation of its own.** Nothing in the 300-entry index of the developer portal, the five OpenAPI definitions, or the routemobile.com API and Developers pages mentions CAMARA, Open Gateway, Number Verification, Silent Authentication, SIM Swap, Device Location, Quality on Demand, Carrier Billing, KYC Match or CIBA.
- **Alignment claimed only at the parent level.** Proximus Global launched **Konera**, a network API aggregation platform, at Global Fintech Fest 2025 in Mumbai, described as "aligned with the GSMA's CAMARA standardization initiative" and targeting 92% of India by end of 2025. The announcement names no individual CAMARA API and links to no documentation. It is a press release, not an implementation.
- **Not a GSMA Open Gateway participant.** Route Mobile does not appear on GSMA's operator or channel-partner lists; the group's carrier relationships sit with BICS.
- **No TM Forum Open API conformance certification** was found, and no NEF/SCEF, network-slicing or edge/MEC surface is documented.

## Authentication

Legacy CPaaS credentials rather than the OIDC/CIBA authorization CAMARA specifies:

| Product | Scheme |
| --- | --- |
| SMS | `username` + `password` query parameters |
| SMS (MoEngage / WebEngage) | Static `Authorization` header token |
| WhatsApp Business | Bearer JWT from the Login API |
| RCS | JWT in `Authorization`, from `/auth/v1/login/` |
| Viber | JWT in `Authorization`, from `/auth/v1/login/` |
| SendClean Email | `owner_id` + `token` in the JSON request body |

No OAuth or OpenID Connect discovery document is served on `api.rmlconnect.net` or `apis.rmlconnect.net` (both `/.well-known/openid-configuration` probes return 404).

## Tags

- Telecommunications
- India
- CPaaS
- Messaging
- SMS
- A2P Messaging
- WhatsApp Business
- RCS
- Voice
- Email
- Identity Verification
- OTP
- Aggregator

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

### Route Mobile SMS API

Single, bulk, scheduled and personalised SMS submission over HTTPS, credit checks, account details, OTP generation and verification, DND/whitelist management, coverage map download, and pre-built submission endpoints for MoEngage and WebEngage. 14 documented operations.

- **Human URL:** [https://developer.rmlconnect.net/route-mobile-project/docs/sms](https://developer.rmlconnect.net/route-mobile-project/docs/sms)
- **Base URL:** `https://api.rmlconnect.net`

#### Properties

- [OpenAPI](openapi/route-mobile-sms.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer.rmlconnect.net/route-mobile-project/docs/sms)
- [API Reference](https://developer.rmlconnect.net/route-mobile-project/reference/sendsmssecured)

### Route Mobile WhatsApp Business API

JWT login, account management, template and session messaging, bulk campaign upload, catalog and product-feed management for commerce, media ID generation, opt-in management, reporting and client callbacks. 33 documented operations.

- **Human URL:** [https://developer.rmlconnect.net/route-mobile-project/docs/whatsapp](https://developer.rmlconnect.net/route-mobile-project/docs/whatsapp)
- **Base URL:** `https://apis.rmlconnect.net`

#### Properties

- [OpenAPI](openapi/route-mobile-whatsapp-business.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer.rmlconnect.net/route-mobile-project/docs/whatsapp)
- [Source Code](https://github.com/routemobile/WhatsApp-Business-API)

### Route Mobile RCS Business Messaging API

Verified-sender RCS with rich cards, carousels and suggested replies; single and bulk message submission, an RCS bill/payment endpoint, typing events, media file server, tester and agent management, handset capability checks, opt-in management and inbound callbacks. 21 operations across 18 paths.

- **Human URL:** [https://developer.rmlconnect.net/route-mobile-project/docs/rcs](https://developer.rmlconnect.net/route-mobile-project/docs/rcs)
- **Base URL:** `https://apis.rmlconnect.net`

#### Properties

- [OpenAPI](openapi/route-mobile-rcs.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer.rmlconnect.net/route-mobile-project/docs/rcs)
- [Source Code](https://github.com/routemobile/RCS-Business-Messaging-API)

### Route Mobile Viber Business Messages API

Login, single and bulk Viber message submission (text, image, video, file, template), campaign management, media upload, summary and graph reporting, report generation and download, and a client callback channel. 16 operations across 15 paths.

- **Human URL:** [https://developer.rmlconnect.net/route-mobile-project/docs/viber](https://developer.rmlconnect.net/route-mobile-project/docs/viber)
- **Base URL:** `https://apis.rmlconnect.net`

#### Properties

- [OpenAPI](openapi/route-mobile-viber.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer.rmlconnect.net/route-mobile-project/docs/viber)
- [Source Code](https://github.com/routemobile/Viber-Business-Messages-API)

### SendClean Email API

Route Mobile's transactional and bulk email product as a JSON-over-HTTP-POST REST API: SMTP users, sending and tracking domains, webhook registration and key rotation, message send and lookup, error retrieval and account details. 24 documented operations.

- **Human URL:** [https://developer.rmlconnect.net/route-mobile-project/docs/email](https://developer.rmlconnect.net/route-mobile-project/docs/email)
- **Base URL:** `https://api.sendclean.net/v1.0`

#### Properties

- [OpenAPI](openapi/route-mobile-sendclean-email.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer.rmlconnect.net/route-mobile-project/docs/email)
- [Source Code](https://github.com/routemobile/Route-Mailer-API)

### Route Mobile Enterprise Voice 2.0 API

Enterprise voice and cloud telephony, documented as narrative guides on the developer portal and published as a first-party Postman collection. No OpenAPI definition is published for voice.

- **Human URL:** [https://developer.rmlconnect.net/route-mobile-project/docs/voice-apis](https://developer.rmlconnect.net/route-mobile-project/docs/voice-apis)

#### Properties

- [Documentation](https://developer.rmlconnect.net/route-mobile-project/docs/voice-apis)
- [Postman Collection](https://github.com/routemobile/Enterprise-Voice-2.0-APIs)

## Other Protocols

Beyond REST, Route Mobile documents **SMPP** (RouteMobile SMPP Gateway Manual) and a **SOAP** web service (SOAP Access Service v1.0.0) as PDFs on [routemobile.com/api/](https://routemobile.com/api/) — the carrier-era interfaces that still carry a large share of A2P traffic in India. No WebSocket, GraphQL, gRPC or AsyncAPI surface is documented.

## Gaps

Several marketed products have no public API documentation at all: Number Lookup, Brandi5, Verified Messages, Verified Calls, Truecaller Verified Business, VoicEX/CCaaS, OmniCent payments, Route Shield, Route Hub, SMSC as a Service, Instant Virtual Number, and the 365 ECM/Detect/Analytics telecom line. Two cards on the developer portal home page — "OTP & Verify" and "Roubot" — return HTTP 404.

## Links

- [Website](https://routemobile.com/)
- [Developer Portal](https://developer.rmlconnect.net/)
- [Legacy API Documents](https://routemobile.com/api/)
- [GitHub](https://github.com/routemobile)
- [Postman Workspace](https://www.postman.com/routemobile/route-mobile-s-public-workspace)
- [llms.txt](https://developer.rmlconnect.net/llms.txt)
- [Blog](https://routemobile.com/blog/)
- [LinkedIn](https://www.linkedin.com/company/routemobilelimited/)
