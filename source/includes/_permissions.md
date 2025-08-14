# Permissions

The RTA API exposes granular permissions over resources (for example, vehicles:view, parts:update). The permissions associated with your API key determine what your integration can access. If an operation requires a permission that your token does not grant, the API returns an HTTP 403 with an error message indicating the missing permission.
