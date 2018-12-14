# Use the RTA Graph API

RTA Graph is a [GraphQL](https://graphql.org/) web API that enables you to access RTA Graph service resources. After you register your app and get authentication tokens for a user or service, you can make requests to the RTA Graph API.

`https://api.rtafleet.com/graphql`

The components of a request include:

* HTTP method - For RTA Graph, this will always be `POST`
* Content type: `application/json`
* Body: JSON-encoded body of the following form:

> Request body format

```json
{
  "query": "...",
  "operationName": "...",
  "variables": { "myVariable": "someValue", ... }
}
```

After you make a request, a response is returned that includes:

* Status code - An HTTP status code that indicates success or failure. For details about HTTP error codes, see Errors.
* Response message - The data that you requested or the result of the operation. The response message can be empty for some operations.
* Next link - If your request returns a lot of data, you need to page through it by choosing Next. For details, see [Paging](#paging).

A query might result in some data and some errors, and those should be returned in a JSON object of the form:

> Response data format

```json
{
  "data": { ... },
  "errors": [ ... ]
}
```

If there were no errors returned, the "errors" field should not be present on the response.

> Sample request and response to retrieve user profile and permissions

> Request

```javascript
query fetchMe {
  getMe {
    id
    status{
      code
      state
    }
    permissions {
      tenantId
      facilityId
      permission
    }
    tenants {
      id
      name
      roles {
        id
      }
    }
  }
}
```

> Response

```json
{
  "data": {
    "getMe": {
      "id": "LuULTaOBq2ar2rLFeQ8IPrIU4Z2",
      "status": null,
      "permissions": [],
      "tenants": [
        {
          "id": "RTA99999",
          "name": "RTA Sample Customer",
          "roles": []
        }
      ]
    }
  }
}
```

# GraphQL Schema

