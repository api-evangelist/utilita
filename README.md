# Utilita (utilita)

Utilita Energy is a United Kingdom household electricity and gas supplier founded in 2003 and headquartered in Eastleigh, Hampshire, specialising in smart Pay As You Go (prepayment) energy for roughly 800,000 mostly lower-income homes. It sits at the retail end of the GB energy value chain — buying wholesale, holding an Ofgem supply licence, and acceding to the Smart Energy Code as a DCC user — and it was the first company in Great Britain to install a residential smart electricity meter (2005) and a combined smart gas and electricity system (2008). Its API posture is closed on every axis: Britain mandated the smart-meter infrastructure rather than a consumer data right, and Utilita publishes no developer portal, no API documentation, no machine-readable contract, and no open market data.

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

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

No public, documented APIs were found. Every developer surface probed on 2026-07-27
returned 404 or failed to resolve. See `review.yml` for the full probe log.

## Common Properties

- [Website](https://utilita.co.uk/)
- [About](https://utilita.co.uk/about-us)
- [Customer Portal](https://my.utilita.co.uk/login)
- [Help](https://utilita.co.uk/help)
- [LinkedIn](https://www.linkedin.com/company/utilita-energy)

## Mandate Posture

- **Mandate regime:** `smart-meter-infrastructure` — the GB Smart Energy Code and the
  Smart DCC licensed monopoly. This is an infrastructure obligation on suppliers, **not**
  a consumer data right.
- **Mandate status:** `live-implemented` — Utilita demonstrably operates a smart-meter
  estate at scale and participates in DCC/SEC governance, but the implementation surface
  is the private licensed DCC User Interface, not a public API.
- **Data standard:** SMETS1/SMETS2 metering under the Smart Energy Code. No Green Button /
  ESPI, no CDR Consumer Data Standards, no OpenAPI.
- **Consumer data API:** none. **Open market data:** none.
- **Access gate:** `none-published` — there is no developer programme to apply to.

## Maintainers

- Kin Lane — kin@apievangelist.com
