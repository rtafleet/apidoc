# Errors

The RTA API uses standard HTTP status codes to indicate success or failure. Error responses include a JSON body with information about the error.

Common status codes
- 400 Bad Request: The request is malformed or invalid.
- 401 Unauthorized: Missing or invalid Bearer token.
- 403 Forbidden: The token does not grant the required permission.
- 404 Not Found: The requested resource does not exist.
- 409 Conflict: The request conflicts with current state.
- 429 Too Many Requests: Throttling/rate limiting.
- 500 Internal Server Error: An unexpected error occurred.

> Sample error response (permission)
```json
{
  "statusCode": 403,
  "error": "Forbidden",
  "message": "Missing required permission vehicles:view",
  "requiredPermission": "vehicles:view"
}
```

> Sample error response (validation)
```json
{
  "statusCode": 400,
  "error": "Bad Request",
  "message": "Invalid filter field: vehicleNumbr"
}
```
