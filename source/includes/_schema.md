# API Reference

The RTA API is REST-based and uses standard HTTP methods and JSON payloads. You can explore available endpoints and models via the OpenAPI documentation:

- [Swagger Docs](https://api.momentum-prd.rtafleet.com/api)

As a note, the swagger docs do not currently support testing endpoints.  You will need to test using postman or some other tool.

Key points

- Authenticate using a Bearer token obtained from the Get API Token endpoint.
- Use collection endpoints’ request bodies to provide queryOptions (pagination, filters, sorts).
- Responses include items and meta pagination data.

For a practical example of searching, see the Vehicles “search-vehicles-enhanced” example in this guide.
