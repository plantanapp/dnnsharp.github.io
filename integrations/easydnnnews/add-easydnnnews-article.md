# Add Article

This action takes values from either form fields, context tokens or MyTokens custom tokens _**as input**_
![Inputs for the Add Article action](https://static.dnnsharp.com/documentation/easydnnnews/add-easydnnnews-article_inputs.png "Inputs for the Add Article action")
and based on the data received creates an article for the specified Easy DNN New instance ID
![Select EasyDNNNews module Id](https://static.dnnsharp.com/documentation/easydnnnews/add-easydnnnews-article-ModuleID.png "Select EasyDNNNews module Id")
and then _**outputs**_ the Article Id in a token for whcih you will need to provide a name (_ArticleId Token_ field)
![Specify an Output Token name](http://s3.amazonaws.com/static.dnnsharp.com/documentation/easydnnnews/add-easydnnnews-article-output-token.png "Specify an Output Token name")
which can be referenced in future actions through a token _[article_number]_ (given that _article_number_ is the name you provided for the token)

> The **Tags** feature was added in [EasyDNNnews Add-on 5.0.22](https://www.dnnsharp.com/download?p=EASYDNN&v=05.00.22)