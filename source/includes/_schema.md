# Exploring the GraphQL Schema

1. Visit `https://graphqlbin.com`.
2. Select **URL ENDPOINT** and enter the Endpoint url for the RTA API: `https://api.rtafleet.com/graphql`.

### Exploring the Docs

On the right side of GraphQL Playground, you will find a tab called **DOCS** which you an use to explore the queries and mutations available in the RTA API.

### Examples

#### Example 1: Querying basic tenant information

> Request

```javascript
{
  getTenant(input: { id: "RTACAN01" }) {
    id
    name
    entitlements
  }
}
```

This sample demonstrates how to retrieve basic tenant information. Notice how GraphQL allows the developer to specify the exact data required in the response.

> Response

```json
{
  "data": {
    "getTenant": {
      "id": "RTACAN01",
      "name": "RTA Canary 01",
      "entitlements": null
    }
  }
}
```

<!--
#### Example 2: Querying current user information, including the id, name, and RTA desktop username the account is impersonating

> Request

```javascript
{
  getMe {
    id
    email
    firstName
    lastName
    tenants {
      id
      name
      username
    }
  }
}
```

> Response

```json
{
  "data": {
    "getMe": {
      "id": "0wrXTJ5KmgquF7mZA4ZF112LB1PLzOsW",
      "email": null,
      "firstName": null,
      "lastName": null,
      "tenants": [
        {
          "id": "RTACAN01",
          "name": "RTA Canary 01",
          "username": "system"
        }
      ]
    }
  }
}
``` -->
