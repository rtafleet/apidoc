# Get access tokens to call the RTA API

To call the RTA API, your app must acquire an access token from Auth0, RTA's cloud identity service. The access token contains information (or claims) about your app and the permissions it has for the resources and APIs available through the RTA API. To get an access token, your app must be able to authenticate with Auth0 and be authorized by either a user or an administrator for access to the the RTA API resources it needs.

This topic provides an overview of access tokens, OAuth and how your app can get access tokens.

## What is an access token and how do I use it?

Access tokens issued by OAuth are base 64 encoded JSON Web Tokens (JWT). They contain information (claims) that the RTA APIs use to validate the caller and to ensure that the caller has the proper permissions to perform the operation they're requesting. When calling the RTA API, you can treat access tokens as opaque. You should always transmit access tokens over a secure channel, such as transport layer security (HTTPS).

Here's an example of an RTA access token:

`eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik9UWTVNVUk1TXpKQk9EWkdSVUU0TXpReVFURTVNRU0zTWpKQ05ESXlOa06T0VVek9URXdOdyJ9.eyJodHRwczovL2FwaS5ydGFmbGVldC5jb20vYXBwX21ldGFkYXRhIjp7InRlbmFudElkIjoiUlRBMDEyNjciLCJpZCI6Ikx1VUxUYU9CcTJhcjJzRlBiaHJMRmVROElQcklVNFoyIiwiaXNNYWNoaW5lMk1hY2hpbmUiOnRydWUsImRlc2t0b3BVc2VybmFtZSI6InN5c3RlbSJ9LCJpc3MiOiJodHRwczovL2Rldi1ydGEuYXV0aDAuY29tLyIsInN1YiI6Ix1VUxUYU9CcTJhcjJzRlBiaHJMRmVROElQcklVNFoyQGNsaWVudHMiLCJhdWQiOiJodHRwczovL3N0Zy5hcGkucnRhaGl2ZS5jb20iLCJpYXQiOjE1NDQ3MTUwNDYsImV4cCI6MTU0NzMwNzA0NiwiYXpwIjoiTHVVTFRhT0JxMmFyMnNGUGJockxGZVE4SVBySVU0WjIiLCJzY29wZSI6InBhcnRzOnZpZXciLCJndHkiOiJjbGllbnQtY3JlZGVudGlhbHMifQ.izNktviwQnmj4yl5mrXLvmdRNyRfJste6fryhmtmEtNacY3ehgEilrrjfpBAgqAhqV8efuB9nkO2x27Bn-P76RHaFYUd5bWHveNCcwRkyLrj51C9_EENpzsjhh1_PU1cDaG15Ruil0LunM_4zSJ_4XIaipHwdDtBx5LatSLqcf5yy2YsKD9pKDfSmIxkYkpiJz_xyUKFW96H45n2cXlgGFoz  2j8skLZITVKQwFp1yJ_CfxmlTkJZ9ZQIQpWUd2PVtzCVCNDq26FJbnJjKX45UhwSw3wb5v-S5sRkDzQl4WYDbRfAf3bCmPmpFrSstp2uvw3_CMvirENT2NE0KPIuGQ`

```http
HTTP/1.1
Authorization: Bearer eyJ0eXAiOiJKV1QiLC ... CMvirENT2NE0KPIuGQ
Host: api.rtafleet.com
POST /graphql HTTP/1.1
{ "query": "{ getMe { id } }"}
```

To call the RTA API, you attach the access token as a Bearer token to the Authorization header in an HTTP request. For example, here's a call that returns the profile information of the signed-in user (the access token has been truncated for readability)

## What are the RTA API permissions?

The RTA API exposes a rich set of granular permissions over the resources it controls. These permissions are expressed as strings and grant apps access to the RTA API resources like vehicles, parts, work orders, purchase orders, etc. For example:

* _vehicles:view_ allows an app to read the vehicles in the RTA system.
* _parts:update_ allows an app to update part details.

There are two types of permissions:

* Delegated permissions are used by apps that run with a user present. The user's privileges are delegated to the app which makes calls on behalf of the user to the RTA API. Many of these permissions can be consented to by a user, but others require administrator consent.
* Application permissions are used by apps that run without a user. These often grant an app broad privileges within an organization and always require the consent of an administrator.

For a complete list of the RTA API permissions, as well as the differences between delegated and application permissions, see the [Permissions](#permissions) reference.

## Where does my app get an access token?

Your app gets access tokens from Auth0, RTA's cloud identity service. To get an access token, your app exchanges HTTP requests and responses with Auth0 using industry-standard protocols defined in the OAuth 2.0 specification. These protocols describe the Auth0 endpoints and exchanges with them -- or authentication flows -- that your app uses to securely authenticate with Auth0 and get access tokens.

On a very simple level, to get an access token, your app exchanges HTTP requests with the following endpoints:

The /authorize endpoint, where your app can send a user to authenticate with Auth0 and consent to the permissions your app needs.
The /token endpoint where your app can get an access token once user consent has been granted.
(Note: These definitions are not rigid. Depending on the protocol your app uses, it may get access tokens directly from the /authorize endpoint or it may authenticate directly with the /token endpoint.)

Here's an example of one set of the /authorize and /token endpoints exposed by Auth0:

* `https://rtafleet.auth0.com/authorize`
* `https://rtafleet.auth0.com/token`

## Register your app with the RTA API

Your app must be registered with RTA. Registering your app establishes a unique application ID and other values that your app uses to authenticate with Auth0 and get tokens. You register your app by [sending a message to RTA support and providing the app name and required permissions](mailto:support@rtafleet.com?subject=New%20API%20Key%20Request&body=Support%2C%20%0APlease%20generate%20a%20new%20RTA%20Graph%20API%20application%20named%20%5BYOUR%20NAME%20HERE%5D.%0A%0AThe%20following%20permissions%20are%20required%3A%20%0A%0A*%20%5BPERMISSION%201%5D%20%0A*%20%5BPERMISSION%202%5D%20%0A%0ACalls%20to%20the%20API%20will%20use%20the%20following%20RTA%20Desktop%20Username%3A%20%5BDESIRED%20USERNAME%20HERE%5D%0A%0AThanks%21%20%0A). Depending on the type of app you are developing, you will need to copy one or more properties during registration to use when you configure authentication and authorization for your app.

## Get access without a user

Some apps call the RTA API with their own identity and not on behalf of a user. In many cases, these are background services or daemons that run on a server without the presence of a signed-in user. An example of such an app might be an data extraction service that wakes up and runs overnight. In some cases, apps that have a signed-in user present may also need to call the RTA API under their own identity. For example, an app may need to use functionality that requires more elevated privileges in an organization than those carried by the signed-in user.

Apps that call the RTA API with their own identity use the OAuth 2.0 client credentials grant flow to get access tokens from Auth0. In this topic, we will walk through the basic steps to configure a service and use the OAuth client credentials grant flow to get an access token.

### Authentication and authorization steps

The basic steps required to configure a service and get a token from the Azure AD v2.0 endpoint that your service can use to call the RTA API under its own identity are:

1. Register your app.
2. Configure permissions for the RTA API on your app.
3. Get an access token.
4. Use the access token to call the RTA API.

### Get an access token

In the OAuth 2.0 client credentials grant flow, you use the Application ID and Application Secret values that you saved when you registered your app to request an access token directly from the Azure AD v2.0 /token endpoint.

<aside class="notice">
You must replace the values for `client_id` and `client_secret` with your personal Application ID and Application Secret values.
</aside>

> Get access token

```http
POST /oauth/token HTTP/1.1
Host: rta.auth0.com
Content-Type: application/json
cache-control: no-cache
{
  "audience": "https://api.rtahive.com",
  "grant_type": "client_credentials",
  "client_id": "LuULTaO2sFPbhrLFe...PrIU4Z2",
  "client_secret": "jsAt0vbpF3...Gqu-LYMOq0y7tYOrFyKABDovFMuZMMCfgIB"
}
```

You send a POST request to the /token endpoint to acquire an access token.

* `audience`: Must be `https://api.rtahive.com`
* `client_id`: The Application ID that the RTA Support team assigned when you registered your app.
* `client_secret`: The Application Secret that was generated for your app by the support team.
* `grant_type`: Must be `client_credentials`

> A successful response looks like this:

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik9UWTVNVUk1TXpKQk9EWkdSVUU...",
    "scope": "parts:view",
    "expires_in": 2592000,
    "token_type": "Bearer"
}
```

A successful response contains the following:

* `access_token`: The requested access token. Your app can use this token in calls to the RTA API.
* `scope`: This value contains all the application permissions you have configured for your app.
* `token_type`: Indicates the token type value. The only type that Azure AD supports is bearer.
* `expires_in`: How long the access token is valid (in seconds).

### Supported app scenarios and resources

Apps that call the RTA API under their own identity fall into one of two categories:

* Background services (daemons) that run on a server without a signed-in user.
* Apps that have a signed-in user but also call the RTA API with their own identity; for example, to use functionality that requires more elevated privileges than those of the user.
* Apps that call the RTA API with their own identity use the OAuth 2.0 client credentials grant to authenticate with Azure AD and get a token.