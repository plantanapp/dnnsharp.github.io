# Server Request (JSON) Datasource

> The feature is available starting with modules released after 10<sup>th</sup> of May 2019 (Action Form 5.0.540)

This datasource type allows you to use an API:
* either internal (your own) built with [DNN API endpoint](https://www.dnnsharp.com/dnn/modules/custom-dnn-api-endpoint) module
* or external (3rd party) from any webservice you might want to integrate with

as source of data for your multiple choice fields.

![Server Request JSON Datasource for Multiple choice fields](https://static.dnnsharp.com/documentation/server_request_JSON_datasource.png "Server Request JSON Datasource for Multiple choice fields")

The output of the API whould be a valid JSON list (an array of objects) similar to:
* either directly an array
```json
[{
	"UserId": "8",
	"FirstName": "Name1"
}, {
	"UserId": "5",
	"FirstName": "SomeName"
}]
``` 
* or the array is a value of one of the JSON parameters, situation in which you will need to provide the correct JSON path to the array (**_$.results_** or **_results_**)
```json
{
	"timestamp": "19:55",
	"date": "2019-05-20",
	"results": "[{\"UserId\":\"8\",\"FirstName\":\"Name1\"},    {\"UserId\":\"5\",\"FirstName\":\"SomeName\"}]"
}
```
As for all datasources, it is also based on _Text|Value_ and you will have to:
* either name the JSON properties as _Text/Value_
* or specify in the multiple choice field settings which JSON property to be used as _Text_ and which one to be used as _Value_ (see example in the image above)