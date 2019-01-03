# Exploring the GraphQL Schema


## Obtain an Authentication token

Prior to connecting to the GraphQL endpoint to browse the schema, you must first obtain an authentication token using your client id and client secret. Follow the instructions in [Get an access token](#get-an-access-token) before proceeding.

## GraphQL Playground

GraphQL Playground provides an interactive method for exploring the RTA API.

```json
{
  "Authorization":"Bearer YOUR AUTH TOKEN HERE"
}
```

1. Download and install the appropriate GraphQL Playground app for your operating system from https://github.com/prisma/graphql-playground/releases. 
2. Run the GraphQL Playground app.
3. Select **URL ENDPOINT** and enter the Endpoint url for the RTA API: `https://api.rtafleet.com`.
4. In the bottom left of the GraphQL Playground, click the **HTTP HEADERS** tab and enter the JSON at the right, using the authentication token received in the previous step.

At this point you should now be authorized to browse the schema and view the docs from within GraphQL Playground.

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