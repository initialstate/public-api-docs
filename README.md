#Groker Api
**PRE-RELEASE**
> *NOTE*: This is a prerelease api and is subject to change frequently without notice or versioning while under development.

> *NOTE*: This api, while functionaly, doesn't provide a way to consume the data created by it just yet. That is in the works!

##[POST]

`https://groker.initialstate.com/batch_logs`

###Headers:
```
Content-Type: application/json
X-IS-ClientKey: YourClientKey
```

###Expected Body:

####Request Body
The request body is an array of JSON objects with the following properties

|name|notes										|
|----|-----------------------------------------|
|`v`	|value of data point					|
|`b`	|bucket name							|
|`dt`	|ISO 8601 timestamp (redundent, see `e`)|
|`e`	|epoc representation of timestamp		|
|`sn`	|signal name							|
|`tid`	|`guid` of sessionId to associate to Initial State Bucket|


####Example:

```
[
	{
		"v": 1,
		"b": "some_bucket_name",
		"dt": "2014-11-17 16:11:28.913554",
		"sn": "example_signal",
		"e": 1416262288.913554,
		"tid": "dc5c3b77-2c9a-4efd-a4ee-68759114e356"
	}
]
```