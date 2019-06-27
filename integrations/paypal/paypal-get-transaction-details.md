# Get Transaction Details

The actions makes a request to Paypal to retrieve details about a provided transaction number; it works for both __*buyer*__ and __*seller*__ transaction number(buyer and seller transaction numer are different).

The action takes a transaction number as input and returns a JSON with various information about the transaction according to Paypal documentation [here](https://developer.paypal.com/docs/classic/api/merchant/GetTransactionDetails-API-Operation-NVP/), like but not limited to:
* fee and settle amount
* currency code
* transaction type
* seller transaction number if buyer transaction number is provided as input

To extract the data from the resulted JSON you can use the [Parse JSON into tokens](/actions/parsing/parse_json_into_tokens.html) action.