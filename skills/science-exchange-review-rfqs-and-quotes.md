---
name: Review incoming RFQs and their quotes
description: Pull a provider's RFQs from the Science Exchange Providers API, inspect a specific RFQ, and review the quotes and line items attached to it.
api: openapi/science-exchange-providers-openapi.yml
operations:
  - getProvidersV1RFQs
  - getProvidersV1RFQsId
  - getProvidersV1Quotes
  - getProvidersV1QuotesId
  - getProvidersV1LineItems
---

# Review incoming RFQs and their quotes

Use the Science Exchange Providers API (read-only, v1) to triage requests for quote and the quotes attached to them.

## Auth
- Base URL: `https://www.scienceexchange.com/api/providers/v1`
- Send your provider key as the `access_token` query parameter on every request. All responses are `application/json`.

## Steps
1. **List open RFQs** — call `getProvidersV1RFQs` (`GET /rfqs`) to retrieve the RFQs visible to your provider account.
2. **Open one RFQ** — for an RFQ of interest, call `getProvidersV1RFQsId` (`GET /rfqs/{id}`) to read its full detail.
3. **List quotes** — call `getProvidersV1Quotes` (`GET /quotes`) to see quotes, then `getProvidersV1QuotesId` (`GET /quotes/{id}`) for a specific quote.
4. **Inspect line items** — call `getProvidersV1LineItems` (`GET /line_items`) to review the priced line items behind a quote.

## Error handling
- `401` — missing or invalid `access_token`; supply a valid provider key.
- `404` — the RFQ or quote id does not exist or is not visible to your account (client raises `ResourceNotFoundError`).
- Any other non-2xx raises a generic client error carrying the request method, URL, and raw response.

## Notes
- This API is read-only; there are no write operations, so nothing here mutates provider data.
