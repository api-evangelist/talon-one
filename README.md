# Talon.One (talon-one)

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

Talon.One is an enterprise promotion, loyalty, and incentives engine. It lets teams build and run coupons, discounts, referrals, bundles, giveaways, and multi-tier loyalty programs from a single rules-based platform, and connect that engine to their own applications in real time. Talon.One exposes two primary REST APIs: an **Integration API** for pushing live customer data into the rules engine and receiving the effects to apply, and a **Management API** for administering the resources behind the Campaign Manager.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/talon-one/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/talon-one/refs/heads/main/apis.yml)

## Access Model (Read This First)

Talon.One is a **commercial, contact-sales enterprise platform** - there is no public free tier and no public self-service signup for the API. API keys are generated inside the Campaign Manager of a provisioned account. Two things follow from that:

- **Per-customer deployment.** Each account runs on its own deployment with its own base URL and deploy region. The host is account-specific - `https://yourbaseurl.talon.one` - rather than a single shared `api.talon.one` origin. Replace `yourbaseurl` with your deployment domain.
- **Two keys, two prefixes.** Both APIs authenticate with the `Authorization` header, but the key prefix distinguishes them:
  - **Integration API** uses an Integration key: `Authorization: ApiKey-v1 <your-key>`
  - **Management API** uses a Management key: `Authorization: ManagementKey-v1 <your-key>` (or a session bearer token from `POST /v1/sessions`)

Everything in this repo is grounded in Talon.One's public documentation and SDKs. Request and response schemas in the OpenAPI are honestly simplified where full schemas were not reproduced.

## Integration API vs Management API

**Integration API** (paths under `/v1` and `/v2`) is the real-time surface. Your application pushes a customer session or event into Talon.One, the rules engine evaluates the Application's active campaigns, and the response carries the **effects** to apply - accepted coupons and referrals, discounts, awarded loyalty points, and triggered messages. Typical calls:

- `PUT /v2/customer_sessions/{customerSessionId}` - update/create a session and get effects
- `POST /v2/events` - submit a custom event that can trigger rules
- `PUT /v2/customer_profiles/{integrationId}` - sync a customer profile
- `POST /v1/coupon_reservations/{couponValue}` - reserve a coupon at redemption time
- `POST /v1/referrals` - create a referral code
- `GET /v1/loyalty_programs/{loyaltyProgramId}/profile/{integrationId}/points` - read loyalty points

**Management API** (paths under `/v1`) is the administrative surface behind the Campaign Manager. Use it to manage Applications, campaigns, rulesets, coupons, loyalty programs, audiences, custom attributes, collections, accounts/users, and analytics/effect exports. Typical calls:

- `GET /v1/applications` and `GET /v1/applications/{applicationId}/campaigns`
- `POST`/`PUT`/`DELETE /v1/applications/{applicationId}/campaigns/{campaignId}`
- `POST /v1/applications/{applicationId}/campaigns/{campaignId}/coupons`
- `GET /v1/loyalty_programs`, `PUT .../profile/{integrationId}/add_points`
- `GET /v1/exports`, `GET /v1/applications/{applicationId}/campaign_analytics/export`

## Tags

- Promotions
- Loyalty
- Coupons
- Incentives
- Campaigns
- Personalization
- MarTech
- Rules Engine

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## APIs

### Talon.One Integration API

Real-time surface that pushes customer sessions, profiles, and custom events into the rules engine and returns the effects to apply. Authenticated with an Integration key prefixed `ApiKey-v1`.

- **Human URL:** [https://docs.talon.one/integration-api](https://docs.talon.one/integration-api)
- **Base URL:** `https://yourbaseurl.talon.one`

### Talon.One Management API

Administrative surface backing the Campaign Manager - Applications, campaigns, rulesets, attributes, audiences, collections, accounts, and exports. Authenticated with a Management key prefixed `ManagementKey-v1`.

- **Human URL:** [https://docs.talon.one/management-api](https://docs.talon.one/management-api)
- **Base URL:** `https://yourbaseurl.talon.one`

### Talon.One Campaigns API

The Management-API resources for building and operating promotion campaigns - create, list, update, copy, and delete campaigns under an Application, manage rulesets, and export campaign analytics.

- **Human URL:** [https://docs.talon.one/docs/product/campaigns/overview](https://docs.talon.one/docs/product/campaigns/overview)
- **Base URL:** `https://yourbaseurl.talon.one`

### Talon.One Coupons API

Coupon lifecycle across both APIs - generate coupons in bulk (including an asynchronous variant), list and update codes, and reserve or release coupons against a customer profile at redemption time. Referral codes are created via the Integration API.

- **Human URL:** [https://docs.talon.one/docs/product/campaigns/coupons/creating-coupons](https://docs.talon.one/docs/product/campaigns/coupons/creating-coupons)
- **Base URL:** `https://yourbaseurl.talon.one`

### Talon.One Loyalty API

Profile-based and card-based loyalty - read balances, points, and transactions, activate pending points, link/unlink cards through the Integration API, and add points, list programs, batch-create cards, and export balances through the Management API. Supports multi-tier programs and subledgers.

- **Human URL:** [https://docs.talon.one/docs/product/loyalty-programs/overview](https://docs.talon.one/docs/product/loyalty-programs/overview)
- **Base URL:** `https://yourbaseurl.talon.one`

## Common Properties

- [GitHub Organization](https://github.com/talon-one)
- [LinkedIn](https://www.linkedin.com/company/talon-one)
- [Website](https://www.talon.one)
- [Documentation](https://docs.talon.one)
- [Sign Up / Demo](https://www.talon.one/demo)
- [Plans](plans/talon-one-plans-pricing.yml)
- [Rate Limits](rate-limits/talon-one-rate-limits.yml)
- [Fin Ops](finops/talon-one-finops.yml)

## Artifacts

- **OpenAPI:** [openapi/talon-one-openapi.yml](openapi/talon-one-openapi.yml)
- **Postman Collection:** [collections/talon-one.postman_collection.json](collections/talon-one.postman_collection.json)
- **Open Collection:** [collections/talon-one.opencollection.json](collections/talon-one.opencollection.json)

## WebSocket

Talon.One does **not** expose a documented public WebSocket API. Both public surfaces are request/response REST over HTTPS; the Integration API returns effects inline in the HTTP response, and outbound notifications are delivered via configured webhooks (server-to-endpoint HTTP), not a client-facing WebSocket. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
