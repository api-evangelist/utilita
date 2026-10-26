# Utilita (utilita)

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

Utilita Energy is a United Kingdom household electricity and gas supplier founded in 2003 and headquartered in Eastleigh, Hampshire, specialising in smart Pay As You Go (prepayment) energy for roughly 800,000 mostly lower-income homes. It sits at the retail end of the GB energy value chain — buying wholesale, holding an Ofgem supply licence, and acceding to the Smart Energy Code as a DCC user — and it was the first company in Great Britain to install a residential smart electricity meter (2005) and a combined smart gas and electricity system (2008).

Its **energy data** posture is closed on every axis: Britain mandated the smart-meter infrastructure rather than a consumer data right, and Utilita publishes no developer portal, no customer usage API, and no open market data. It does, however, run **one real public API** — an anonymous, documented status API reporting the live health of its smart meters, payment channels, app and portal.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/utilita/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/utilita/refs/heads/main/apis.yml)

## Tags

- Energy
- United Kingdom
- Utilities
- Electricity
- Gas
- Smart Metering
- Prepayment
- Energy Retail
- Status
- Operational Transparency

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Utilita Status API

Public, anonymous, read-only JSON. Eight `GET` endpoints under `https://status.utilita.co.uk/api/v2`,
documented by Utilita at [status.utilita.co.uk/api](https://status.utilita.co.uk/api). No key, no
sign-up, CORS-open, 10-second cache window.

| Operation | Path |
|---|---|
| `getSummary` | `/summary.json` |
| `getStatus` | `/status.json` |
| `getComponents` | `/components.json` |
| `getIncidents` | `/incidents.json` |
| `getUnresolvedIncidents` | `/incidents/unresolved.json` |
| `getScheduledMaintenances` | `/scheduled-maintenances.json` |
| `getUpcomingScheduledMaintenances` | `/scheduled-maintenances/upcoming.json` |
| `getActiveScheduledMaintenances` | `/scheduled-maintenances/active.json` |

It tracks 21 real Utilita components — SMETS1, SMETS1 (DCC Enrolled) and SMETS2 smart meters, Guest
Payments, Open Banking, PayPoint in-store and IVR top-up, PayZone in-store, the My Utilita app and web
portal, Power-up functionality, utilita.co.uk, join.utilita.co.uk, telephone lines, the chatbot, smart
meter installations and the smart metering network — with incident history and self-serve webhook, RSS,
Atom, email and Slack notifications. It carries **no** customer, billing or consumption data.

Utilita publishes no OpenAPI; `openapi/utilita-status-openapi.yml` was generated by API Evangelist
from live observation of all eight endpoints on 2026-07-27, with an `x-evidence` block on every
operation and verbatim response snapshots in `examples/`.

## Artifacts

- `openapi/utilita-status-openapi.yml` — generated OpenAPI 3.1 for the status API
- `examples/` — verbatim live response snapshots
- `asyncapi/utilita-status-webhooks.yml` — webhook / RSS / Atom event surface
- `authentication/utilita-authentication.yml` — no credentials exist; every other surface is a human login
- `conventions/utilita-conventions.yml` — caching, CORS, versioning, error envelope, no pagination/idempotency
- `errors/utilita-problem-types.yml` — `{"errors":[...]}` envelope (not RFC 9457)
- `lifecycle/utilita-lifecycle.yml` — URI-path v2, status page, no deprecation policy, no SLA
- `conformance/utilita-conformance.yml` — including why Green Button and CDR do not apply
- `data-model/utilita-data-model.yml` — page / component / incident entity graph
- `security/utilita-domain-security.yml` — TLS, HSTS, DNSSEC, CAA, SPF, DMARC probes
- `well-known/` — full `/.well-known/` sweep (one document, and it belongs to Atlassian)
- `skills/` — agent skill for reading Utilita service status
- `llms/utilita-llms.txt` — generated llms.txt

## Common Properties

- [Website](https://utilita.co.uk/)
- [About](https://utilita.co.uk/about-us)
- [Status Page](https://status.utilita.co.uk/)
- [API Documentation](https://status.utilita.co.uk/api)
- [Customer Portal](https://my.utilita.co.uk/login)
- [Join / Sign Up](https://join.utilita.co.uk/)
- [Help](https://utilita.co.uk/help)
- [Contact](https://utilita.co.uk/contact)
- [Community](https://community.utilita.co.uk/)
- [Blog](https://utilita.co.uk/blog)
- [Terms](https://utilita.co.uk/terms)
- [Privacy Notice](https://utilita.co.uk/privacy-notice)
- [LinkedIn](https://www.linkedin.com/company/utilita-energy)

## Mandate Posture

- **Mandate regime:** `smart-meter-infrastructure` — the GB Smart Energy Code and the
  Smart DCC licensed monopoly. This is an infrastructure obligation on suppliers, **not**
  a consumer data right.
- **Mandate status:** `live-implemented` — Utilita demonstrably operates a smart-meter
  estate at scale and participates in DCC/SEC governance, but the implementation surface
  is the private licensed DCC User Interface, not a public API.
- **Data standard:** SMETS1/SMETS2 metering under the Smart Energy Code. No Green Button /
  ESPI, no CDR Consumer Data Standards.
- **Consumer data API:** none. **Open market data:** none. **Operational status API:** yes.
- **Access gate:** `none-published` for energy data — there is no developer programme to
  apply to. The status API needs no gate at all.

## Maintainers

- Kin Lane — kin@apievangelist.com
