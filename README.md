# Talon.One

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

Talon.One is an enterprise promotion, loyalty, and incentives engine that lets teams build and run coupons, discounts, referrals, bundles, giveaways, and multi-tier loyalty programs from a single rules-based platform. It exposes two primary REST APIs. The Integration API pushes real-time customer sessions, profiles, and events into the rules engine and returns the effects (discounts, awarded loyalty points, accepted coupons) to apply in the calling application. The Management API programmatically administers applications, campaigns, rulesets, coupons, loyalty programs, audiences, custom attributes, collections, and analytics exports that back the Campaign Manager. Talon.One is delivered as a managed, per-customer deployment; each account calls its own base URL (https://yourbaseurl.talon.one) and authenticates with an API key whose prefix distinguishes the Integration key (ApiKey-v1) from the Management key (ManagementKey-v1).

**Areas:** Promotions · Loyalty · Coupons · Incentives · Campaigns · Personalization · MarTech · Rules Engine · Referrals · Discounts · E-Commerce · Retail

## Talon.One on APIs.io

Everything profiled for Talon.One is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/talon-one/](https://apis.io/providers/talon-one/)** — or go straight to one of the APIs or properties below.

### APIs (42)

- [Talon.One Accounts and users API](https://apis.io/apis/talon-one/talon-one-accounts-and-users-api/) — Represents account and user management, including billing email addresses and user invitations.
- [Talon.One Achievements API](https://apis.io/apis/talon-one/talon-one-achievements-api/) — Represents achievements that reward a customer profile for performing a number of specific actions or reaching a transactional milestone within a defined…
- [Talon.One Additional costs API](https://apis.io/apis/talon-one/talon-one-additional-costs-api/) — Represents an extra fee applied to the cart, for example, shipping fees or processing fees. See the…
- [Talon.One Analytics API](https://apis.io/apis/talon-one/talon-one-analytics-api/) — Represents analytics used to retrieve statistical data about the performance of campaigns within an Application.
- [Talon.One Applications API](https://apis.io/apis/talon-one/talon-one-applications-api/) — Represents an Application in the Campaign Manager. An Application is the target of every Integration API request to Talon.One. One Application can hold…
- [Talon.One Attributes API](https://apis.io/apis/talon-one/talon-one-attributes-api/) — Represents a piece of information related to one of the entities available in the Campaign Manager. Use them to create highly customized rules. See the…
- [Talon.One Audiences API](https://apis.io/apis/talon-one/talon-one-audiences-api/) — Represents lists of customer profiles that allow you to target specific groups of customers in your campaigns. Audiences can be synced from customer data…
- [Talon.One Braze API](https://apis.io/apis/talon-one/talon-one-braze-api/) — [Braze](https://www.braze.com/) is a customer engagement platform to manage customer-centric interactions between consumers and brands in real-time. Use…
- [Talon.One Campaign access groups API](https://apis.io/apis/talon-one/talon-one-campaign-access-groups-api/) — Represents the campaign access groups you can create in your Applications to organize your campaigns based on the type of campaign or the team in charge.…
- [Talon.One Campaign notifications API](https://apis.io/apis/talon-one/talon-one-campaign-notifications-api/) — Represents the [notifications](/docs/product/applications/application-notifications/overview) about campaign-related changes. > [!note] The value of the…
- [Talon.One Campaign templates API](https://apis.io/apis/talon-one/talon-one-campaign-templates-api/) — Represents templates used to generate campaigns from.
- [Talon.One Campaigns API](https://apis.io/apis/talon-one/talon-one-campaigns-api/) — Represents the primary resource used to control the behavior of the Talon.One Rule Engine. They combine rulesets, coupons, and limits into a single unit.…
- [Talon.One Catalogs API](https://apis.io/apis/talon-one/talon-one-catalogs-api/) — Represents a catalog of cart items with unique SKUs. Cart item catalogs allow you to synchronize your entire inventory with Talon.One. See the…
- [Talon.One Collections API](https://apis.io/apis/talon-one/talon-one-collections-api/) — Represents a collection of arbitrary values that you can use inside rules. For example, a list of SKUs. See the…
- [Talon.One Coupon notifications API](https://apis.io/apis/talon-one/talon-one-coupon-notifications-api/) — Represents the [notifications](/docs/product/applications/application-notifications/overview) about coupons.
- [Talon.One Coupons API](https://apis.io/apis/talon-one/talon-one-coupons-api/) — Represents unique codes belonging to a particular campaign. Coupons don't define any behavior on their own. Instead the campaign ruleset can include rules…
- [Talon.One Customer data API](https://apis.io/apis/talon-one/talon-one-customer-data-api/) — Represents the data of a customer, including sessions and events used for reporting and debugging in the Campaign Manager.
- [Talon.One Customer data platforms API](https://apis.io/apis/talon-one/talon-one-customer-data-platforms-api/) — You can integrate with any customer data platform, or CDP, using the following endpoints designed for third-party tools, rather than your own integration…
- [Talon.One Customer engagement platforms API](https://apis.io/apis/talon-one/talon-one-customer-engagement-platforms-api/) — You can integrate with any customer engagement platform, or CEP, using the following endpoints designed for third-party tools, rather than your own…
- [Talon.One Customer profiles API](https://apis.io/apis/talon-one/talon-one-customer-profiles-api/) — Represents the customer's information. For instance, their contact information.
- [Talon.One Customer sessions API](https://apis.io/apis/talon-one/talon-one-customer-sessions-api/) — Represents the data related to a customer session. Typically, a customer session is the value and content of the customer's cart. Sessions can be anonymous…
- [Talon.One Emarsys API](https://apis.io/apis/talon-one/talon-one-emarsys-api/) — Emarsys is a customer engagement platform that enables marketers to build, launch, and scale personalized cross-channel promotional campaigns that have…
- [Talon.One Events API](https://apis.io/apis/talon-one/talon-one-events-api/) — Represents a single occurrence of a specific customer action, for example, updating the cart or signing up for a newsletter. There are 2 types of events: -…
- [Talon.One Experiments API](https://apis.io/apis/talon-one/talon-one-experiments-api/) — Represents an A/B testing configuration within a campaign that splits customer sessions across multiple variants to compare rule effects against each other.
- [Talon.One Giveaways API](https://apis.io/apis/talon-one/talon-one-giveaways-api/) — Represents a program that rewards customers with giveaways, such as free gift cards. See the [docs](https://docs.talon.one/docs/product/giveaways/overview).
- [Talon.One Iterable API](https://apis.io/apis/talon-one/talon-one-iterable-api/) — [Iterable](https://iterable.com/) is a cross-channel marketing platform that powers unified customer experiences and empowers you to create, optimize and…
- [Talon.One Logs API](https://apis.io/apis/talon-one/talon-one-logs-api/) — Represents the Talon.One logs, which contain all incoming and outgoing requests.
- [Talon.One Loyalty API](https://apis.io/apis/talon-one/talon-one-loyalty-api/) — Represents loyalty programs or concepts related to them. Loyalty programs can be _profile-based_ or _card-based_, depending on whether loyalty points are…
- [Talon.One Loyalty card notifications API](https://apis.io/apis/talon-one/talon-one-loyalty-card-notifications-api/) — Represents the [notifications](/docs/product/loyalty-programs/loyalty-notifications/overview) about changes to loyalty points in card-based loyalty programs.
- [Talon.One Loyalty cards API](https://apis.io/apis/talon-one/talon-one-loyalty-cards-api/) — Represents loyalty cards. [Loyalty cards](https://docs.talon.one/docs/product/loyalty-programs/card-based/card-based-overview) allow your customers to…
- [Talon.One Loyalty notifications API](https://apis.io/apis/talon-one/talon-one-loyalty-notifications-api/) — Represents the [notifications](/docs/product/loyalty-programs/loyalty-notifications/overview) about changes to loyalty points in profile-based loyalty programs.
- [Talon.One M Particle API](https://apis.io/apis/talon-one/talon-one-mparticle-api/) — [mParticle](https://www.mparticle.com/) is the customer data platform that helps unify data and simplify partner integrations with enterprise-class security…
- [Talon.One Referrals API](https://apis.io/apis/talon-one/talon-one-referrals-api/) — Represents a referral code shared between a customer (advocate) and a prospect (friend). A referral is defined by: - an advocate: person who invited their…
- [Talon.One Roles API](https://apis.io/apis/talon-one/talon-one-roles-api/) — Represents a set of permissions assigned to a user. See the [docs](https://docs.talon.one/docs/product/account/account-settings/managing-roles).
- [Talon.One Segment API](https://apis.io/apis/talon-one/talon-one-segment-api/) — [Segment](https://segment.com/) is a customer data platform that collects events from your web & mobile apps. Use these endpoints to integrate with Talon.One.
- [Talon.One Session API](https://apis.io/apis/talon-one/talon-one-session-api/) — Use the following endpoints to manage customer sessions.
- [Talon.One Sessions API](https://apis.io/apis/talon-one/talon-one-sessions-api/) — Represents a session used for authentication purposes. Create one with the [Create session](#tag/Sessions/operation/createSession) endpoint.
- [Talon.One Store budgets API](https://apis.io/apis/talon-one/talon-one-store-budgets-api/) — Represents store budgets. You can set a store budget to limit the total amount an individual store can spend in a campaign.
- [Talon.One Stores API](https://apis.io/apis/talon-one/talon-one-stores-api/) — Represents physical or digital stores, branches, and franchises.
- [Talon.One Strikethrough pricing notifications API](https://apis.io/apis/talon-one/talon-one-strikethrough-pricing-notifications-api/) — Represents the [notifications](/docs/product/applications/application-notifications/overview) about strikethrough pricing updates.
- [Talon.One Value maps API](https://apis.io/apis/talon-one/talon-one-value-maps-api/) — Represents the value maps that the user can create within a campaign ruleset.
- [Talon.One Webhooks API](https://apis.io/apis/talon-one/talon-one-webhooks-api/) — Represents webhooks, which send information from Talon.One to the URI of your choice. See the [docs](https://docs.talon.one/docs/dev/getting-started/webhooks).

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Talon One Webhooks](https://apis.io/asyncapis/talon-one/talon-one-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Talon.One MCP server](https://apis.io/servers/talon-one/talon-one-mcp-server/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Talon One Agentic Access](https://apis.io/agentic-access/talon-one/talon-one-agentic-access/)

#### Collections (6)

Postman and Open Collection request collections.

- [Talon.One API](https://apis.io/collections/talon-one/open-talon-one/)
- [Integration API](https://apis.io/collections/talon-one/open-talon-one-integration-api/)
- [Management API](https://apis.io/collections/talon-one/open-talon-one-management-api/)
- [Notification schemas](https://apis.io/collections/talon-one/open-talon-one-outbound-notifications/)
- [Shopify Integration API](https://apis.io/collections/talon-one/open-talon-one-shopify-integration-api/)
- [Third-party API](https://apis.io/collections/talon-one/open-talon-one-third-party-api/)

#### Overlays (42)

OpenAPI overlays, including conversational phrasing for each operation.

- [Talon One Accounts And Users Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-accounts-and-users-api-phrasing-overlay/)
- [Talon One Achievements Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-achievements-api-phrasing-overlay/)
- [Talon One Additional Costs Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-additional-costs-api-phrasing-overlay/)
- [Talon One Analytics Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-analytics-api-phrasing-overlay/)
- [Talon One Applications Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-applications-api-phrasing-overlay/)
- [Talon One Attributes Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-attributes-api-phrasing-overlay/)
- [Talon One Audiences Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-audiences-api-phrasing-overlay/)
- [Talon One Braze Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-braze-api-phrasing-overlay/)
- [Talon One Campaign Access Groups Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-campaign-access-groups-api-phrasing-overlay/)
- [Talon One Campaign Templates Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-campaign-templates-api-phrasing-overlay/)
- [Talon One Campaigns Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-campaigns-api-phrasing-overlay/)
- [Talon One Catalogs Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-catalogs-api-phrasing-overlay/)
- [Talon One Collections Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-collections-api-phrasing-overlay/)
- [Talon One Coupons Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-coupons-api-phrasing-overlay/)
- [Talon One Customer Data Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-customer-data-api-phrasing-overlay/)
- [Talon One Customer Data Platforms Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-customer-data-platforms-api-phrasing-overlay/)
- [Talon One Customer Engagement Platforms Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-customer-engagement-platforms-api-phrasing-overlay/)
- [Talon One Customer Profiles Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-customer-profiles-api-phrasing-overlay/)
- [Talon One Customer Sessions Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-customer-sessions-api-phrasing-overlay/)
- [Talon One Emarsys Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-emarsys-api-phrasing-overlay/)
- [Talon One Events Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-events-api-phrasing-overlay/)
- [Talon One Experiments Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-experiments-api-phrasing-overlay/)
- [Talon One Giveaways Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-giveaways-api-phrasing-overlay/)
- [Talon One Integration Api Overlay](https://apis.io/overlays/talon-one/talon-one-integration-api-overlay/)
- [Talon One Iterable Api Phrasing Overlay](https://apis.io/overlays/talon-one/talon-one-iterable-api-phrasing-overlay/)
- …and 17 more published on APIs.io

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Talon One Authentication](https://apis.io/security/talon-one/talon-one-authentication/)
- [Talon One Domain Security](https://apis.io/security/talon-one/talon-one-domain-security/)
- [Talon One Trust Center](https://apis.io/security/talon-one/talon-one-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Talon One Plans Pricing](https://apis.io/plans/talon-one/talon-one-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Talon One Rate Limits](https://apis.io/rate-limits/talon-one/talon-one-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Talon One Finops](https://apis.io/finops/talon-one/talon-one-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.talon.one)
- [Documentation](https://docs.talon.one)
- [Getting started](https://docs.talon.one/docs/dev/quickstart)
- [API reference](https://docs.talon.one/integration-api)
- [Pricing](https://www.talon.one/pricing)
- [Sign up](https://www.talon.one/book-a-demo)
- [Support](https://www.talon.one/contact-us)
- [Changelog](https://docs.talon.one/whats-new)
- [Blog](https://www.talon.one/blog)
- [Terms of service](https://www.talon.one/legal/terms-of-use)
- [Privacy policy](https://www.talon.one/legal/privacy-policy)
- [GitHub](https://github.com/talon-one)
- [Status](https://status.talon.one/)

## API Evangelist rating

**Kin Score 73.9** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.3 |
| Contract quality | 64.0 |
| Contract governance | 4.5 |
| Operational transparency | 81.6 |
| Developer ergonomics | 81.0 |
| Access clarity | 92.1 |

**Agent readiness 47.1** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | templated |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | mostly (partial credit) |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/talon-one/](https://apis.io/providers/talon-one/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Talon.One: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/talon-one/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
