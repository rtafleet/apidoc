# Errors

> Sample error response (permission)

```json
{
  "statusCode": 403,
  "error": "Forbidden",
  "message": "Missing required permission vehicles:view",
  "requiredPermission": "vehicles:view"
}
```

The RTA API uses standard HTTP status codes to indicate success or failure. Error responses include a JSON body with information about the error.

Common error status codes

* 400 Bad Request: The request is malformed or invalid.  Verify the date you are sending is correct.
* 401 Unauthorized: Missing or invalid Bearer token.
* 403 Forbidden: The token does not grant the required permission.
* 404 Not Found: The requested resource does not exist.  Verify the resource you are trying to access exists, and that your url is correct.
* 409 Conflict: The request conflicts with current state.
* 429 Too Many Requests: Throttling/rate limiting.
* 500 Internal Server Error: An unexpected error occurred.

> Sample error response (validation)

```json
{
  "statusCode": 400,
  "error": "Bad Request",
  "message": "Invalid filter field: vehicleNumbr"
}
```
