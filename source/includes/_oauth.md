# Authentication: Get API Token
## Tenant ID (Serial Number)

> Example: Finding your tenantId in the app URL

```http
https://app.rtafleet.com/.../?tenantId=RTACAN01&facilityId=2
```

The tenantId identifies your RTA tenant and is also known as your Serial Number. You can find it by signing in to the RTA web app and looking at the browser URL—it's the value of the tenantId query parameter (for example, RTACAN01 in the example above). Use this value in the API path placeholders like /{tenantId} and when calling the Get API Token endpoint.



## Client ID and Secret
> Example: Get an API token

```http
GET https://api.momentum-prd.rtafleet.com/information-management/{tenantId}/integrations/get-api-token?clientId={clientId}&clientSecret={clientSecret}
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
To call the RTA API, your app must obtain an API token from the Momentum Get API Token endpoint. Tokens are JSON Web Tokens (JWT) used as a Bearer token in the Authorization header.  This will require a Client ID and Secret, which you can obtain by registering your app in Fleet360.

Your app must be registered with RTA. Registering your app establishes a unique application ID and other values that your app uses to authenticate with Auth0 and get tokens. You register your app by [creating an API Key on Fleet360](https://app.rtafleet.com/admin/api-keys). More info can also be found [here](https://docs.rtafleet.com/rta-manual/rta-api-keys/). 
