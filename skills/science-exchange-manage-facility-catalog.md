---
name: Audit a provider's facilities, services, and ratings
description: Pull a provider's facilities, drill into a facility, enumerate its services, and review ratings using the Science Exchange Providers API.
api: openapi/science-exchange-providers-openapi.yml
operations:
  - getProvidersV1Facilities
  - getProvidersV1FacilitiesId
  - getProvidersV1Services
  - getProvidersV1ServicesId
  - getProvidersV1Ratings
---

# Audit a provider's facilities, services, and ratings

Use the Science Exchange Providers API (read-only, v1) to inventory what a provider offers and how it is rated.

## Auth
- Base URL: `https://www.scienceexchange.com/api/providers/v1`
- Send your provider key as the `access_token` query parameter on every request. All responses are `application/json`.

## Steps
1. **List facilities** — call `getProvidersV1Facilities` (`GET /facilities`) to list the provider's facilities.
2. **Open one facility** — call `getProvidersV1FacilitiesId` (`GET /facilities/{id}`) for a facility's detail.
3. **Enumerate services** — call `getProvidersV1Services` (`GET /services`) and `getProvidersV1ServicesId` (`GET /services/{id}`) to read the scientific services offered.
4. **Review ratings** — call `getProvidersV1Ratings` (`GET /ratings`) to pull the provider's ratings for quality signals.

## Error handling
- `401` — missing or invalid `access_token`.
- `404` — facility or service id not found / not visible (`ResourceNotFoundError`).
- Other non-2xx raises a generic client error with method, URL, and raw response.

## Notes
- Read-only API; use these operations for audit and reporting, not mutation.
