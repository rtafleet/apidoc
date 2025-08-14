# Authentication: Get API Token

To call the RTA API, your app must obtain an API token from the Momentum Get API Token endpoint. Tokens are JSON Web Tokens (JWT) used as a Bearer token in the Authorization header.

Prerequisites
- In the RTA Web App, create an API Key for your integration to obtain a Client ID and Client Secret:
  https://app.rtafleet.com/admin/api-keys
  Additional info: https://docs.rtafleet.com/rta-manual/rta-api-keys/

> Get an API token
>
> ```http
> GET https://api.rtafleet.com/information-management/{tenantId}/integrations/get-api-token?clientId={clientId}&clientSecret={clientSecret}
> ```

> Response
>
> ```json
> {
>   "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIs..."
> }
> ```

> Use the token
>
> ```http
> Authorization: Bearer eyJhbGciOi...
> ```
>
Include the token as a Bearer token on subsequent requests:

Permissions
The RTA API exposes granular permissions over resources (for example, vehicles:view, parts:update). The permissions associated with your API key determine what your integration can access. If an operation requires a permission that your token does not grant, the API returns an HTTP 403 with an error message indicating the missing permission.
