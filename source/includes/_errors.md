# Errors

```json
{
  "data": { ... },
  "errors": [ ... ]
}
```

The RTA API returns error information as part of the response. A query might result in some data and some errors, and those should be returned in a JSON object of the form shown at the right.

> Sample invalid request

```javascript
query {
  getParts(input: {tenantId: "INVALID_ID", facilityId: "200"}) {
    parts {
      id
      partNumber
    }
  }
}
```

If there were no errors returned, the "errors" field will not be present on the response.

Field | Description
----- | -----------
`message` | The error message.
`extensions` | Additional information about the error.
`exception` | Exception/Error details.
`requiredPermission` | The permission required to execute the requested operation.

> Sample error response

```json
{
  "data": null,
  "errors": [
    {
      "message": "Missing required \"parts:view\" permission.",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "getParts"
      ],
      "extensions": {
        "code": "API.MISSING_PERMISSION_PARTS_VIEW",
        "exception": {
          "code": "API.MISSING_PERMISSION_PARTS_VIEW",
          "type": "MISSING_REQUIRED_PERMISSION",
          "description": "Missing required \"parts:view\" permission.",
          "tokens": {
            "requiredPermission": "parts:view"
          },
          "ctx": {
            "awsRequestId": "a1772866-ffbe-11e8-bd7e-b91d02e81301",
            "correlationId": "a15b14c4-ffbe-11e8-bc70-19caf995b12d",
            "info": {
              "getPartsGraphql": "2018-12-14T16:38:05+00:00",
              "fetchPartsApi": "2018-12-14T16:38:05+00:00"
            }
          }
        }
      }
    }
  ]
}
```