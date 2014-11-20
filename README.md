#Logging Api
**PRE-RELEASE**
> *NOTE*: This is a prerelease api and is subject to change frequently without notice or versioning while under development.


There are 2 POST calls that are necessary to call in order to send data via API. There execution is independent of each other, so you can call in any order, the most important shared pieces of data are the `bucketName` and the `sessionId`.

Authentication is handled via `clientKey`, don't loose, publish or share. If you do, please delete the key from your account.


##[POST]

`https://api.initialstate.com/api/v1/buckets`

###Headers:
```
Content-Type: application/json
```

###Expected Body:

####Example Body

```
{
	"bucketId": "dc5c3b77-2c9a-4efd-a4ee-68759114e356",
	"bucketName": "The Bucket",
	"clientKey": "YourClientKey"
}
```

####Request Body
JSON request body

|name|type|notes|
|----|----|-----|
|bucketId|`guid`|this is a unique identifier, it should be the same value as what you use when sending logs in `tid`|
|bucketName|`string`|name of the bucket, 200 character limitation|
|clientKey|`string`|secret key you get from the initialstate.com|


###Response Codes:
- `204` Created
- `401` Unauthorized (`clientKey` is either incorrect, or url isn't correct)
- `403` Forbidden (`clientKey` is missing or invalid)
- `404` Check your url
- `500` Internal Server Error (we're still in beta :) )


##[POST]

`https://groker.initialstate.com/batch_logs`

###Headers:
```
Content-Type: application/json
X-IS-ClientKey: YourClientKey
```

###Expected Body:


####Example:

```
[
	{
		"b": "some_bucket_name",
		"sn": "example_signal",
		"v": 1,
		"e": 1416262288.913554,
		"tid": "dc5c3b77-2c9a-4efd-a4ee-68759114e356"
	}
]
```

####Request Body
The request body is an array of JSON objects with the following properties

|name|type|notes	|
|----|----|--------|
|`v`	|`string`, `bool` or `number`|value of data point |
|`b`	|`string`|bucket name; length 200|
|`e`	|`float`|epoc representation of timestamp|
|`sn`	|`string`|signal name, recommended shorter than 50 characters, hard cap at 100|
|`tid`	|`guid`|sessionId to associate to Initial State Bucket|

###Response Codes:
- `204` Created
- `403` Forbidden (`clientKey` is either missing or invalid)