# Properly (properly)

Properly was a Toronto-based Canadian digital real estate brokerage founded in 2018 that began as one of the country's only iBuyers — making algorithmic cash offers on Calgary homes — before pivoting to Sale Assurance, a guaranteed-purchase backstop that let a seller buy their next home before selling the current one, wrapped around an online listing search and a machine-generated home valuation. It sat in the challenger layer of the Canadian value chain alongside HouseSigma, Wahi, and Zolo, competing on visibility into listing data controlled by CREA, the national cooperative that operates REALTOR.ca and the Data Distribution Facility (DDF) syndicating member boards' listings, in a market where land registration is provincially privatised and the public record is itself a commercial product. Properly was acquired by Pine Canada Financial Corporation in October 2023 and the brand has since been absorbed: `properly.ca` and `www.properly.ca` now answer HTTP 301 from an Amazon S3 and CloudFront redirect bucket to `www.pine.ca`, and the word "Properly" no longer appears anywhere on the surviving Pine real estate pages. Its API posture is closed and, as of this profile, non-existent — no developer portal, no API program, no partner or data-licensing page, and no machine-readable contract of any kind.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/properly/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/properly/refs/heads/main/apis.yml)

## Tags

- Real Estate
- Canada
- Property Listings
- MLS
- Valuation
- AVM
- PropTech
- Mortgage

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

No public, documented APIs. The `developer.`, `developers.`, `api.`, `docs.`, `app.` and `blog.` subdomains of `properly.ca` do not resolve in DNS, and every contract path probed — `/openapi.json`, `/swagger.json`, `/api-docs`, `/$metadata`, `/odata`, `/Reso` — is 301-redirected into `www.pine.ca` where it returns HTTP 404. On the successor domain, `https://www.pine.ca/developers`, `/api` and `/openapi.json` return HTTP 200 but are Next.js soft-404s carrying `<title>Page not found</title>`; `/openapi.json` serves 167,549 bytes of HTML, not JSON. The only genuine machine surface found is `https://api.pine.ca/`, an AWS API Gateway that answers every probed path with HTTP 403 and `{"message":"Missing Authentication Token"}` — a private first-party backend with no documentation, no key issuance, and no published contract. It is an implementation detail, not a developer product, and is therefore not listed here.

## RESO Posture

**Not RESO-certified. No RESO reference found.**

RESO's own [Canadian Membership](https://www.reso.org/canadian-membership/) page enumerates the Canadian member organizations — CREA, Centris, Clientime, Falcon Technologies Corporation, Listed, Local Logic, Multi List Platform Limited Partnership, MPAC, Origin Confirmed Ltd, Phoenix Software, Planitar, PropTexx, Prospects Software, the REALTORS® Association of Edmonton, the Real Estate Board of Greater Vancouver, the Saskatchewan REALTORS® Association, Templates 4 Business, the Victoria Real Estate Board, and the Winnipeg Regional Real Estate Board — and neither Properly nor Pine appears on it. No RESO Web API certification, no Data Dictionary certification or version, no certification directory entry (`https://certification.reso.org/` returned HTTP 400 anonymously), no OData `$metadata` document, and no Universal Property Identifier (UPI) usage was observed on any Properly or Pine host. The sole occurrence of the token `RESO` in the surviving real estate page's HTML is inside the i18n key `RESOURCES`. This is the expected Canadian answer: RESO certification is a US industry mandate driven by NAR, while Canadian residential listings flow through CREA's national Data Distribution Facility (DDF).

## Access Gate

**`none-published`.** There is nothing for a developer to sign or join, because nothing is on offer — and the company no longer serves a web application of its own. No self-serve signup, no application form, no partner page, no data-licensing page, no API terms. Beneath the product, the listing data is doubly licensed: the successor operates as a licensed brokerage (`Pine Real Estate Brokerage FSRA Brokerage License ON #13410 | AB #00527319 | SK #511826 | NS #2022-3000465 | NB #230000436 | NL 23-07PI045-1`) and its listing media is delivered from `cdn.repliers.io`, the CDN of the commercial MLS data vendor Repliers — whose [own developer guide](https://repliers.com/a-guide-to-mls-apis-in-canada/) states that "Wahi, Buy.ca, and Pine (formerly Properly), use Repliers as their MLS® API solution." A third party wanting this data must become a member brokerage, sign a CREA DDF or board IDX/VOW data licence, or buy vendor access — none of which is a path Properly offers.

## Open Data

**None.** No open, unlicensed, publicly callable dataset. The only machine-readable public documents are SEO crawl aids — a `sitemapindex` at `https://www.pine.ca/sitemap.xml` pointing at static, blog, partners, listings, and places sitemaps — and `robots.txt` explicitly disallows `/listings` to all user agents. Canada has no counterpart to HM Land Registry Price Paid or Ordnance Survey open data; provincial land registration is largely privatised, with Teranet operating Ontario's registry under long concession, so even the public record is a commercial product.

## Auth Model

**None published.** No API key programme, no OAuth 2.0 or OpenID Connect developer flow, no SAML member portal. `https://properly.ca/.well-known/openid-configuration` redirects into a Pine HTTP 404; `https://www.pine.ca/.well-known/openid-configuration` and `/.well-known/security.txt` both return HTTP 404; `https://api.pine.ca/.well-known/openid-configuration` returns HTTP 403 `MissingAuthenticationTokenException`. That gateway token is the only observable authentication requirement and is documented nowhere, so no scheme is asserted. Consumer sign-in and the separate application host `https://apply.pine.ca/` are end-user flows, not developer authentication.

## Webhooks, Events, SDKs, Postman

None found — the absence is itself the finding. No webhook or event documentation, no AsyncAPI, no GraphQL schema, no published SDK or CLI, and no Postman workspace or collection. No GitHub organization could be attributed: [github.com/properly](https://github.com/properly) is an unrelated org created in 2012 whose declared blog is `properly.com.br`, and `github.com/pinecanada` returns HTTP 404.

## Artifacts

Enrichment round 2026-07-26. Contract discovery was re-run against every Properly and Pine host — `properly.ca`, `www.pine.ca`, `api.pine.ca` — and every probe missed, so the artifacts below record verified absence rather than a captured contract.

- [`security/properly-domain-security.yml`](security/properly-domain-security.yml) — probed. `properly.ca` still presents a valid TLS 1.3 certificate (expires 2027-01-25) with HSTS `max-age=63072000`, SPF and a DMARC `p=reject`, despite serving nothing but a redirect; `pine.ca` matches on TLS/HSTS/SPF but sits at DMARC `p=none`. Neither domain has DNSSEC or CAA records.
- [`well-known/properly-well-known.yml`](well-known/properly-well-known.yml) — probed. Every `/.well-known/` path (security.txt, openid-configuration, oauth-authorization-server, oauth-protected-resource, api-catalog, ai-plugin.json) is HTTP 404 on `properly.ca` and `www.pine.ca`, and HTTP 403 on `api.pine.ca`. Carries the full contract-discovery probe log: `www.pine.ca/openapi.json` returns HTTP 200 but is a 167 KB Next.js soft-404 titled "Page not found", not a spec.
- [`conformance/properly-conformance.yml`](conformance/properly-conformance.yml) — searched. Thirteen verified negatives across the sector standards (RESO Web API, RESO Data Dictionary, UPI, OData, CREA DDF) and the cross-cutting ones (OpenAPI, GraphQL, AsyncAPI, MCP, OAuth 2.0, OIDC, RFC 9457, RFC 9116).
- [`lifecycle/properly-lifecycle.yml`](lifecycle/properly-lifecycle.yml) — searched. Company lifecycle in place of an API lifecycle: founded 2018, acquired by Pine Canada Financial Corporation October 2023, brand absorbed, domain redirect-only. No versioning scheme, deprecation policy, SLA or status page.
- [`llms/properly-llms.txt`](llms/properly-llms.txt) — generated. Agent-readable summary of the retired brand, the absent API surface, and this repository.

No `openapi/`, `packages/`, `mcp/`, `skills/`, `sandbox/`, `changelog/`, `cli/`, `errors/`, `scopes/`, or `authentication/` artifacts exist, and none were fabricated: there is no specification to derive them from and no registry package, MCP server, or documented auth scheme to search for.

## Common Properties

- [Website](https://properly.ca/) — historic Properly home page, HTTP 301 to Pine
- [Pine Real Estate](https://www.pine.ca/real-estate) — the surviving real estate surface
- [Blog](https://www.pine.ca/resources)
- [LinkedIn](https://ca.linkedin.com/company/pine-financial)

## Maintainers

- **Kin Lane** — kin@apievangelist.com
