# Extracting data from RTA

RTA has built a simple REST API for extracting useful data directly from the RTA database. This is useful for customers who need direct access to the raw, unformatted data for use in data warehousing and other utility projects.

The data returned represents the actual physical column names in the database.

The data extract API can be used by first obtaining an access token as descrbed in this documentation. The access token is then used as a bearer token in the `authorization` header.

### Required Permission

A special API permission has been created to allow use of the data extract API. We recommend tighly controlling and securing the client id and client secret when granted this permission because anyone with these credentials will have full read access to all of the data in your database.

Permission Name | Description
--------------- | -----------
api:extractTable | gives full read access to all tables in the customer database

<aside class="notice">

<p><b>A note on etags</b></p>

<p>The data extract API makes extensive use of etags. An etag is simply a text value in a table row that automatically increments whenever any column in the row is updated. The etag is similar to a date/time stamp, without the complexity of dates and times. Using the etag allows you to request only the latest changes since the last time you retrieved the data from the server so that you can periodically request small sets of data from the RTA API.</p>
</aside>

## URL format of the extract API

Use the following URL to access the data extract API.

URL: `https://api.momentum-prd.rtafleet.com/v0/extract/<tablename>?etag=<etag>&limit=<limit>`

Field | Description
----- | -----------
`tablename` | The name of the actual table in the RTA database. To obtain the table names you may request the data dictionary by contacting support@rtafleet.com
`etag` | The first etag value to return
`limit` | limit is not required, has a max of 1000 and defaults to 1000.  If you choose to get your data in increments of 100, you could set limit=100.

## Examples calling the API

See the example at the right for the format of the data returned from the API.

> The resulting object is:

```javascript
{
    "count": 1000,
    "value" : [the rows from the table sorted by etag],
     "nextEtag" : "12344"
}
```

where `nextEtag` would be the very next etag value to use.  nextEtag is not returned if you have received all the rows in the table.

## Retreive the first 1000 records

> Example retrieving records from `vehfile`

```http
curl --request GET \
  --url "https://api.momentum-prd.rtafleet.com/v0/extract/vehfile?etag=0&limit=1000" \
  --header "authorization: Bearer $AUTH_TOKEN"
```

> Sample reponse from `vehfile`

```javascript
{
    "count":"1000",
    "value":[
        {FIRST RECORD IN TABLE},
        ...,
        {1000th RECORD IN TABLE}
    ],
    "nextEtag":"12345"
}
```

See the example CURL request at the right to retrieve the first 1000 records from the vehilces table `vehfile`.

## Retrieve any rows modified since the etag 12345

> Sample request with etag

```http
curl --request GET \
  --url "https://api.momentum-prd.rtafleet.com/v0/extract/vehfile?etag=12345&limit=1000" \
  --header "authorization: Bearer $AUTH_TOKEN"
```

> Sample response without nextEtag

```javascript
{
    "count":"50",
    "value":[
        {1001th RECORD IN TABLE},
        ...,
        {1051th RECORD IN TABLE}
    ]
}
```

See the example CURL request at the right to retrieve anything that has been created or modified since the etag of 12345 has been retrieved.

Because nextEtag was not returned, there are no more rows to retrieve.

## Errors in the data extract API

If you supply an invalid tablename, you will receive a 404 error.
