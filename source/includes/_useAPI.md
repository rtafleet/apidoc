# Use the RTA API
> Example: Get an API token

```http
GET https://api.momentum-prd.rtafleet.com/information-management/{tenantId}/integrations/get-api-token?clientId={clientId}&clientSecret={clientSecret}
```

```json
{
  "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6..."
}
```

> Call an endpoint with the token

```http
POST https://api.momentum-prd.rtafleet.com/asset-management/{tenantId}/vehicles/search-vehicles-enhanced
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json
```

```json
{
  "queryOptions": {
    "pagination": { "offset": 0, "limit": 50 },
    "filters": [
      { "name": "vehicleNumber", "operator": "eq", "values": ["1001"] }
    ],
    "sorts": [
      { "sortBy": "vehicleNumber", "sortOrder": "ASC" }
    ]
  }
}
```

The RTA API is a REST web API. After you register your app and obtain an API token, you can make HTTPS requests to RTA endpoints using a Bearer token in the Authorization header. Your tenant identifier is called tenantId (also known as your Serial Number); see Tenant ID (Serial Number) to find it.

Base URL
- https://api.momentum-prd.rtafleet.com

Authentication

- Obtain a token using the Get API Token endpoint.
- Include the token as a Bearer token in the Authorization header on every request.

A successful response includes the requested data and pagination metadata. See Paging for details on pagination fields.

# Working with IDs
> Example: Find a vehicle ID, then get details

```http
POST https://api.momentum-prd.rtafleet.com/asset-management/{tenantId}/vehicles/search-vehicles-enhanced
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json
```

```json
{
  "queryOptions": {
    "pagination": { "offset": 0, "limit": 1 },
    "filters": [
      { "name": "vehicleNumber", "operator": "eq", "values": ["1001"] }
    ]
  }
}
```

> Sample search response (truncated)

```json
{
  "items": [
    {
      "id": "UUID",
      "vehicleNumber": "1001"
    }
  ],
  "meta": { /* ... */ }
}
```

> Use the ID with detail/update endpoints

```http
# Get details
GET https://api.momentum-prd.rtafleet.com/asset-management/{tenantId}/vehicles/{id}
Authorization: Bearer eyJhbGciOi...

# Update (example)
PUT https://api.momentum-prd.rtafleet.com/asset-management/{tenantId}/vehicles/{id}
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "make": "Ford" }
```

Many endpoints that act on a specific resource (for example: get details, update, delete) require that resource’s unique identifier (id). You typically obtain these IDs from the corresponding search endpoints. Each search response includes an `items` array where each item contains an `id` field.

Typical flow
- Use a search endpoint to find the record and read its `id` from the response
- Call the detail/update/delete endpoint using that `id`



Notes
- IDs are stable unique identifiers (generally UUIDs) and are required for actions on a single resource across domains (Vehicles, Work Orders, Parts, etc.).
- For nested resources (e.g., work order lines, attachments, comments), you may need both the parent ID and the child item ID; obtain each via their respective search/list endpoints.

# Searching (Vehicles example)
> Example request

```http
POST https://api.momentum-prd.rtafleet.com/asset-management/{tenantId}/vehicles/search-vehicles-enhanced
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json
```

> Request body

```json
{
  "queryOptions": {
    "pagination": { "offset": 0, "limit": 25 },
    "filters": [
      { "name": "vehicleNumber", "operator": "eq", "values": ["1001"] },
      { "name": "year", "operator": "gte", "values": [2020] }
    ],
    "sorts": [
      { "sortBy": "vehicleNumber", "sortOrder": "ASC" }
    ]
  }
}
```

> Response

```json
{
  "items": [
    {
      "id": "UUID",
      "vehicleNumber": "1001",
      "serialNumber": "1FT...123",
      "make": "Ford",
      "model": "F-150",
      "year": 2022
    }
  ],
  "meta": {
    "page": 1,
    "totalPages": 1,
    "totalRecords": 1,
    "offset": 0,
    "limit": 25,
    "sorts": [{ "sortBy": "vehicleNumber", "sortOrder": "asc" }],
    "searchMeta": null
  }
}
```

Use the Vehicles search-vehicles-enhanced endpoint to perform flexible searches with filters, sorts, and pagination.

Endpoint
- POST /asset-management/{tenantId}/vehicles/search-vehicles-enhanced

Request body (queryOptions)

- pagination: Controls paging through results
  - offset: Number of records to skip (zero-based; first record is 0)
  - limit: Maximum number of records to return
- filters: Array of filter objects to narrow results
  - name: The field name to filter on (for example, vehicleNumber, year, facility.number)
  - operator: How to compare the field to the provided values. Supported operators include:
      - eq, neq
      - gt, gte, lt, lte
      - contains, beginsWith, endsWith
  - values: Array of one or more values to evaluate against the field (strings, numbers, booleans, or null)
- sorts: Array of sort objects to order results
  - sortBy: The field name to sort on (for example, vehicleNumber, year)
  - sortOrder: ASC or DESC

The sort and filter fields are defined in the API Documentation for each endpoint.
