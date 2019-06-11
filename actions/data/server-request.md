# Server Request Action

This action has the purpose of posting the form data to a different server, you can use the _URL field_ to determine the location for where the data will be posted, in this box you can also use tokens, and there's another useful box, the _Post Data_ box, where you can put key = value pairs on separate lines and you can also add additional _HTTP headers_, in case you need it, and you can specify the HTTP method by selecting it from the _"Choose an HTTP Method"_ drop down list.

The action can be used to make an HTTP request to a different server, optionally sending data.
> For requests made to [API Endpoint](https://www.dnnsharp.com/dnn/modules/custom-dnn-api-endpoint) methods on the same site we recommend using the [Execute API method action](/actions/data/execute-api-method.html) for increased speed(_it eliminates the slow internet connection factor_)
> 
Often, this means invoking a web service. Note that if you don’t run in _Full Trust_, this action requires that the _Application Pool_ identity has _Web Permission_. 


The following fields can be configured:

* **URL** - This represents the URL to make the request to. A common mistake is to forget to include the protocol. For example www.domain.com/webservice is wrong. Instead, use [//www.domain.com/websservice](//www.domain.com/websservice). Optionally, append the query string directly to the URL after the question mark. For example [//www.domain.com/websservice?q=test&p=1](//www.domain.com/websservice?q=test&p=1). This field supports context tokens and My Tokens.
* **Timeout** - you can specify a custom timeout(in seconds) for the request;_(it defaults to 100 seconds)_
* **POST Data** - This is data to send to the URL using POST operation. Put **key=value** pairs, each on a separate line. It’s also possible to post whole messages, for example and **XML** \(that SOAP-like services expect\) by simply putting the XML without any lines. This field supports context tokens and My Tokens.
  > Starting with [Action Form 5.0.583](http://www.dnnsharp.com/download?p=AFORM&v=05.00.583) the POST Data parameters are being automatically passed on in the URL for requests to GET methods; prior to this version, when GET methods are called, the parameters need to be passed on in the URL
* **Headers** - you can specify custom headers to be passed on with the request like Authorization, Content-Type...
* **Output token name** - the name of the token in which the response of the server request action will be stored; it can be referenced in future actions.
* **On Error** - you can define a list of actions to be executed when the Server request action fails
  
![](https://static.dnnsharp.com/documentation/server_request.png)

> The Server Request action supports TLS1.2 requests only starting with Action Form version 5; in order to make TLS1.2 requests with older Action Form versions you will need a [custom built Server Request action](mailto:sales@dnnsharp.com "Request it from our Sales Department").

A basic example of using the Server Request action on a form button would be to convert Celsius degrees to Fahrenheit degrees. For this we'll need to call a web service with which we'll make the conversion and display the result on a Display Message action, here are the steps:

1. Add a form on your page &gt; access **Manage** form option;
2. Add a text box and label it **Celsius**
3. Add a button and on the button add **Server Request** action
4. In **URL** field paste the following: [//www.w3schools.com/webservices/tempconvert.asmx/CelsiusToFahrenheit](//www.w3schools.com/webservices/tempconvert.asmx/CelsiusToFahrenheit);
5. In **Post Data Box** set **Celsius=\[Celsius\]** - meaning that the form field **Celsius** will be used as token to take any value inserted in the form;
6. On Choose an **HTTP Method** drop down select the POST option;
7. Store the answer in a token bu using the **Output Token Name** section - set for example **"test"**;
8. Add a **Display Message** action and on **Message** field put the stored token **\[test\]**;
9. After saving the form and getting back on the page, insert in **Celsius box** a value, and click on **Submit**.

As expected result, the value 10 should be converted and the result should be displayed in the message action.
