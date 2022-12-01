# Code Samples

Code samples that demonstrate using the RTA API are available in the [RTA Developer Samples GitHub repository](https://github.com/rtafleet/developer-samples).

# Use the RTA API Version 2
There are 2 versions of the RTA API.  The first version is what a majority of these docs pertain to, our graphql api.

Our version 2 api docs can be found [here](https://api.momentum-prd.rtafleet.com/api)

Authentication is handled the same as the version 1 api, though a token CAN be generated through the version 2 api via the following endpoint:
[api](https://api.momentum-prd.rtafleet.com/api/#/Information%20Management%20%3E%20Integrations/getApiToken)

# Use the RTA API Version 1

The RTA API is a [GraphQL](https://graphql.org/) web API that enables you to access RTA API service resources. After you register your app and get authentication tokens for a user or service, you can make requests to the RTA API.

`https://api.rtafleet.com/graphql`

> Request body format

```json
{
  "query": "...",
  "operationName": "...",
  "variables": { "myVariable": "someValue", ... }
}
```

The components of a request include:

- HTTP method - For RTA API, this will always be `POST`
- Content type: `application/json`
- Body: JSON-encoded body of the following form:

After you make a request, a response is returned that includes:

> Response data format

```json
{
  "data": { ... },
  "errors": [ ... ]
}
```

- Status code - An HTTP status code that indicates success or failure. For details about HTTP error codes, see Errors.
- data - The data that you requested or the result of the operation. The response message can be empty for some operations. If your request returns a lot of data, you need to page through it. For details, see [Paging](#paging).
- errors - Any errors that occur will be included.

A query might result in some data and some errors, and those should be returned in a JSON object of the form:

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
