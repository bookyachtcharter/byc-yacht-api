# byc-yacht-api

Book Yacht Charter partner API for accessing yacht listings, search, and destination data for external website integrations.

---

# Book Yacht Charter — Yacht Listings API

![API Version](https://img.shields.io/badge/version-v1-blue)
![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-proprietary-lightgrey)

---

## Overview

The **Book Yacht Charter (BYC) Yacht Listings API** enables approved partners to display curated yacht charter listings within external websites and applications.

The API provides structured access to yacht data, destinations, and search functionality to support discovery experiences, listing integrations, and charter research tools.

Typical integrations include:

- Yacht listing grids and search interfaces  
- Yacht detail pages  
- CMS or WordPress synchronization  
- Destination-based browsing experiences  

> The API is versioned. Backwards-incompatible changes will be introduced under new versions.

---

## Base URLs

**Production**  
`https://api.bookyachtcharter.com/v1`

**Sandbox**  
`https://api-sandbox.bookyachtcharter.com/v1`

---

## Authentication

Requests require an API key issued to approved partners.

**Header**

```http
Authorization: Bearer <API_KEY>
```

API keys enable access control, usage monitoring, and rate limiting.

To request early access, contact: **api@bookyachtcharter.com**

---

## Rate Limits

Planned default limits (subject to agreement):

- 60 requests per minute  
- 10,000 requests per day  

Limits may vary depending on integration requirements.

---

## Common Integration Patterns

### Yacht Listing Pages

Use `GET /yachts` with filters and pagination to render searchable listing grids including:

- yacht name  
- guest capacity  
- cabins  
- length  
- primary imagery  
- indicative pricing (if enabled)  
- destination coverage  

---

### Yacht Detail Pages

Use `GET /yachts/{id}` to retrieve detailed yacht information including specifications, imagery, and amenities.

---

### CMS Synchronization (Optional)

Typical workflow:

1. Create a custom content type (e.g. `yacht`)
2. Import yachts via scheduled sync
3. Update records periodically
4. Render templates using stored data

Recommended refresh intervals:

- Weekly for catalog data
- Daily when pricing or availability data is used

---

## Endpoints (Planned)

### `GET /yachts` — Search & Filter Yachts

Search BYC yacht listings using filters and pagination.

#### Example Query Parameters

| Parameter | Type | Description |
|---|---|---|
| `q` | string | Full-text search |
| `destination` | string | Destination slug or ID |
| `guests_min` | int | Minimum guest capacity |
| `cabins_min` | int | Minimum cabins |
| `length_min_m` | number | Minimum yacht length |
| `length_max_m` | number | Maximum yacht length |
| `yacht_type` | string | Motor Yacht, Sailing Yacht, Catamaran, etc. |
| `price_min` | int | Minimum price (minor units) |
| `price_max` | int | Maximum price (minor units) |
| `currency` | string | USD, EUR, GBP |
| `page` | int | Default 1 |
| `page_size` | int | Default 24 (max 100) |
| `sort` | string | relevance, price_asc, price_desc, length_desc |

---

### Example Request

```bash
curl -H "Authorization: Bearer $BYC_API_KEY" \
"https://api.bookyachtcharter.com/v1/yachts?destination=mediterranean&guests_min=8&page=1&page_size=24"
```

---

### Example Response (structure)

```json
{
  "page": 1,
  "page_size": 24,
  "total": 3985,
  "results": [
    {
      "id": "victorious",
      "name": "Victorious",
      "yacht_type": "Superyacht",
      "length_m": 85.0,
      "guests": 12,
      "cabins": 6,
      "primary_image": "https://example.com/victorious.jpg",
      "price_from": {
        "amount": 950000,
        "currency": "EUR",
        "period": "week"
      },
      "destinations": ["middle-east", "mediterranean"]
    }
  ]
}
```

---

### `GET /yachts/{id}` — Yacht Details

```bash
curl -H "Authorization: Bearer $BYC_API_KEY" \
"https://api.bookyachtcharter.com/v1/yachts/victorious"
```

Returns detailed yacht specifications, imagery, amenities, and supported destinations.

---

## Caching Recommendations

- Cache destination lists for **24 hours**
- Cache search queries for **5–30 minutes**
- Cache yacht detail responses for **1–24 hours**

---

## Status

This API is currently under development. Documentation reflects intended functionality and may evolve as the platform expands.

---

## Support

API access & partnerships: **api@bookyachtcharter.com**  
Integration assistance: **partners@bookyachtcharter.com**

---

## About Book Yacht Charter

Book Yacht Charter is an independent platform designed to simplify luxury yacht charter research through structured destination insights, yacht data, and transparent industry guidance.

🌍 https://bookyachtcharter.com
