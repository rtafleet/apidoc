# Paging

Paging of records is handled as part of the request to any of the plural methods in the RTA Graph API using the `queryOptions.pagination` element in the GraphQL query.

When a response is returned, a set of `meta` data is supplied which provides additional pagination information indicating the current `page`, `totalPages`, `totalRecords`, current `offset` and current `limit`

Terms

Term | Meaning
---- | -------
`offset` | The number of records to skip. This is a zero-based number meaning that the first record is represented by the number 0; the tenth record by the number 9.
`limit` | The maximum number of records to return in the query.
`page` | The current page number.
`totalPages` | The total number of pages given the current `limit`.
`totalRecords` | The total number of records available.

> Paged result request

```javascript
query {
  getParts(input: {
      tenantId: "RTA99999",
      facilityId: "200",
      queryOptions: {
          pagination: {
              offset: 0,
              limit: 50
              }
        }
    }) {
    parts {
      id
      partNumber
      description
      meanCost
      sellingPrice
    }
    meta {
      page
      totalPages
      totalRecords
      offset
      limit
      sort {
        sortBy
        sortOrder
      }
      searchMeta {
        id
        relevancy
      }
    }
  }
}
```

> Response, results truncated for brevity

```json
{
  "data": {
    "getParts": {
      "parts": [
        {
          "id": "00096F4A5EB1A82C67F6BD8DFE9744BB",
          "partNumber": "10W30",
          "description": "10W30 Motor Oil",
          "meanCost": 2.43,
          "sellingPrice": 3.43
        },
        {
          "id": "000A87043FAC8438CDF312974E95CCB2",
          "partNumber": "D1770",
          "description": "Brake Pads - Front",
          "meanCost": 21.5,
          "sellingPrice": 37.99
        }
        ...
      ],
      "meta": {
        "page": 1,
        "totalPages": 74,
        "totalRecords": 3698,
        "offset": 0,
        "limit": 50,
        "sort": {
          "sortBy": "id",
          "sortOrder": "asc"
        },
        "searchMeta": null
      }
    }
  }
}
```