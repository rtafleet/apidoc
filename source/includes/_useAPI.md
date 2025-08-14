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

Request body
- queryOptions.pagination: { offset, limit }
- queryOptions.filters: array of { name, operator, values[] } to filter results
- queryOptions.sorts: array of { sortBy, sortOrder } to sort results


