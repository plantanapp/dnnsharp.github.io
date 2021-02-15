# Stripe Get Event Details (ApiEndpoint Only)

## **Introduction**

Parse stripe events dynamically with the help of APIEndpoint and Stripe webhooks. This action doesn't replace the webhook found in (Stripe Checkout)[/stripe/stripe-checkout-sca.html], you will still have to use that way of declaring a webhook in order to fully exploit Stripe Checkout, this action is only meant to expand the possibilities and parse other events as well. This action doesn't automatically parse the JSON received into tokens, it only gives you a simpler version of the input JSON and the event type.

### **Stripe Configuration**

1. In [Stripe Dashboard](https://dashboard.stripe.com/test/dashboard) you need to configure API keys, on [API Keys page](https://dashboard.stripe.com/test/apikeys)

2. A webhook on [Developers > Webhooks](https://dashboard.stripe.com/test/webhooks) page, pointing to ``https://<Your_ApiEndpoint_URL>``.

3. Also, the '**Signing Secret**' of the webhook is required to authenticate the Stripe calls, so note it down because we will add it to DNN web.config file later.

### **DNN Configuration**

Keep in mind that no matter what you do inside the endpoint with the event received, you must return a 200 OK response to Stripe, otherwise it will keep retrying to send the event until such a response was returned from ApiEndpoint.

In order for wehbooks to work, you need to set in DNN web.config the 'Signing Secret' obtained from Stripe > Developers > Webhook > **your_webhook**. Copy your 'Signing Secret' then add it to web.config under
**//configuration/appSettings** the following line:

```xml
     <add " value="Your_Signing_Secret_Here"/>
```

Starting with Stripe 05.11.01 the above mentioned way of declaring the Stripe secret key is obsolete and the new way of declaring the keys allows separate Stripe webhooks for multi-portal use as shown below.

```xml
     <add key="key="DnnSharpStripeEventApiSigningSecretKey_YourPortalIdHere" value="Your_Signing_Secret_Here"/>
```

## **Parameter Details**

1. **Raw Json Input**
   In this parameter, you should pass the whole JSON input that ApiEndpoint receives, you can use the ApiEndpoint `[RawInput]` token.

2. **Event Type Output Token**
   This parameter holds the event type (i.e.: `account.updated`) that was received to make it more convenient for you to condition your actions based on it.
You can check all the event types that you can receive [here](https://stripe.com/docs/api/events/types).

3. **Event JSON Output Token**
   This parameter holds the event JSON that was received. YOu can use both the token that you passed in the Raw Json Input or the one that is output in this token, the only difference is that the Event Json Output Token strips some of the Stripe Metada which might not be useful and will require less JSON parsing in further actions down the action stack.
