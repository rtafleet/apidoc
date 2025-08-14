# Authentication: Get API Token

To call the RTA API, your app must obtain an API token from the Momentum Get API Token endpoint. Tokens are JSON Web Tokens (JWT) used as a Bearer token in the Authorization header.

> Example: Get an API token

```http
GET https://api.rtafleet.com/information-management/{tenantId}/integrations/get-api-token?clientId={clientId}&clientSecret={clientSecret}
```

```json
{
  "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIs..."
}
```

> Authorization header

```http
Authorization: Bearer eyJhbGciOi...
```


Permissions
The RTA API exposes granular permissions over resources (for example, vehicles:view, parts:update). The permissions associated with your API key determine what your integration can access. If an operation requires a permission that your token does not grant, the API returns an HTTP 403 with an error message indicating the missing permission.
