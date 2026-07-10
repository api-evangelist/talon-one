# Talon.One (talon-one)

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
