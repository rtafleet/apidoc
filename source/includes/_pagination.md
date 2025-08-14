# Paging

Paging is handled using the `queryOptions.pagination` object in the request body for collection endpoints. Responses include a `meta` object with pagination details.

Terms

Term | Meaning
---- | -------
`offset` | Number of records to skip (zero-based; first record is 0).
`limit` | Maximum number of records to return.
`page` | The current page number derived from offset/limit.
`totalPages` | Total number of pages given the current `limit`.
`totalRecords` | Total number of records available.

Example: Vehicles search with pagination
> Request
```http
POST https://api.rtafleet.com/asset-management/{tenantId}/vehicles/search-vehicles-enhanced
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json
```

```json
{
  "queryOptions": {
    "pagination": { "offset": 0, "limit": 50 }
  }
}
```

> Response (truncated)
```json
{
  "items": [
    { "id": "UUID", "vehicleNumber": "1001", "year": 2022 }
  ],
  "meta": {
    "page": 1,
    "totalPages": 74,
    "totalRecords": 3698,
    "offset": 0,
    "limit": 50,
    "sort": { "sortBy": "vehicleNumber", "sortOrder": "asc" },
    "searchMeta": null
  }
}
```
