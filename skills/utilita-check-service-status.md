---
name: Check Utilita service status
description: >-
  Determine whether Utilita Energy's smart meters, payment channels, My Utilita app/portal, websites
  or contact centre are currently degraded, and report open incidents and upcoming maintenance —
  using Utilita's public, anonymous status API.
api: openapi/utilita-status-openapi.yml
base_url: https://status.utilita.co.uk/api/v2
authentication: none
operations:
  - getStatus
  - getSummary
  - getComponents
  - getUnresolvedIncidents
  - getUpcomingScheduledMaintenances
  - getActiveScheduledMaintenances
generated: '2026-07-27'
method: generated
source: openapi/utilita-status-openapi.yml (all operationIds verified against live endpoints on 2026-07-27)
---

# Check Utilita service status

Utilita Energy publishes exactly one public API: the status API behind
[status.utilita.co.uk](https://status.utilita.co.uk/). It is anonymous, read-only and CORS-open.
There is no key to obtain and no sign-up. Everything else Utilita runs — customer usage, balances,
top-ups — is behind the My Utilita login and has no public API.

## Before you start

- **Auth:** none. Send a plain `GET`. Do not attach credentials.
- **Base URL:** `https://status.utilita.co.uk/api/v2`
- **Polling floor:** responses carry `Cache-Control: max-age=10` and a weak `ETag`. Poll no more than
  once every 10 seconds, and send `If-None-Match` to avoid re-transferring an unchanged body.
- **No pagination, no query parameters.** Filtering is expressed as separate paths.
- **Errors** are `{"errors":["..."]}` with an HTTP status — not RFC 9457 problem+json. See
  `errors/utilita-problem-types.yml`.

## Step 1 — Is anything wrong right now?

Call `getStatus` (`GET /status.json`). Read `status.indicator`:

| indicator | meaning |
|---|---|
| `none` | All systems operational — you can stop here. |
| `minor` / `major` / `critical` | Something is degraded; continue to step 2. |
| `maintenance` | A planned window is running; go to step 4. |

## Step 2 — Get the whole picture in one call

Call `getSummary` (`GET /summary.json`). It returns the page, the indicator, every component with its
status, all unresolved incidents and any upcoming/active maintenance. Prefer this over three separate
calls when you need a full report.

## Step 3 — Which Utilita service is affected?

Call `getComponents` (`GET /components.json`) or read `components[]` from the summary. Components with
`group: true` are containers — join children to parents with `group_id` before reporting. The 21
components observed group as:

- **Payments** — SMETS1 Smart Meters, SMETS1 (DCC Enrolled) Smart Meters, SMETS2 Smart Meters, Guest
  Payments, Open Banking, PayPoint In Store Payments, PayPoint IVR Top-up Phone Line, PayZone In Store
  Payments
- **My Utilita** — App, Web Portal, Power-up Functionality
- **Websites** — Utilita.co.uk, join.utilita.co.uk
- **Contact Centre** — Telephone Lines, Chatbot
- **Ungrouped** — Smart Meter Installations, Smart Metering Network

Report on the component a person actually cares about. "Can I top up?" is answered by the *Payments*
group plus *Power-up Functionality*, not by the page-level indicator.

## Step 4 — Open incidents and planned work

- `getUnresolvedIncidents` (`GET /incidents/unresolved.json`) — currently open incidents. Each carries
  an `incident_updates[]` timeline; the newest entry (`created_at`) is the current statement, and its
  `status` moves `investigating` → `identified` → `monitoring` → `resolved`.
- `getActiveScheduledMaintenances` (`GET /scheduled-maintenances/active.json`) — maintenance running now.
- `getUpcomingScheduledMaintenances` (`GET /scheduled-maintenances/upcoming.json`) — read
  `scheduled_for` / `scheduled_until` (Europe/London) before telling anyone when service returns.

Both incident endpoints return an empty array when there is nothing to report — that is a healthy
result, not an error.

## Step 5 — Stop polling, get pushed instead

For a long-running agent, subscribe rather than poll: the status page offers webhook notifications on
incident create/update/resolve and component status change, plus RSS and Atom feeds
(`/history.rss`, `/history.atom`). See `asyncapi/utilita-status-webhooks.yml`. The webhook subscribe
form is reCAPTCHA-protected, so it is a human, one-time setup step.

## What this API cannot tell you

- Nothing about an individual customer: no balance, no top-up, no meter reading, no tariff. Those
  exist only inside My Utilita behind a customer login, with no public API.
- Nothing about the wider GB grid. Carbon intensity comes from NESO, settlement data from Elexon.
- Third-party access to GB smart-meter data runs through the Smart DCC as a Smart Energy Code
  "Other User" with consumer consent — not through Utilita.
